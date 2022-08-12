## 术语详解 terminology ##

实际上Lucene所用的信息信息检索方面的术语基本跟Information Retrieval（《信息检索》原版）保持一致。比如Term、Dictionary、Postings等。

<br/><br/><br/>

<font size=3 color=green>索引（Index）</font>
---
对于初学全文检索的人来说，索引这个词非常具有迷惑性，主要原因是它有两个词性：

- 动词：做动词时，一般英文写为“indexing”，比如“索引一个文件”翻译为“indexing a file”，它指的是我们将原始数据经过一系列的处理，最终形成可以高效全文检索（对于Lucene，就是生成倒排索引）的过程。这个过程就称之为索引（indexing）。
- 名词：做名词时，写为“index”。经过indexing最终形成的结果（一般以文件形式存在）称之为索引（index）。

所以，见到索引这个词，你一定要分清楚是动词还是名词。后面为了清楚，凡是作为动词的时候我使用indexing，作为名词的时候使用index。Index是Lucene中的顶级逻辑结构，它是一个逻辑概念，如果对应到具体的实物，就是一个目录，目录里面所有的文件组成一个index。注意，这个目录里面不会再嵌套目录，只会包含多个文件。具体index的构成细节后面会专门写一篇文章来介绍。对应到代码里面，就是org.apache.lucene.store.Directory这个抽象类。最后要说明一点的是，Lucene中的Index和ElasticSearch里面的Index不是一个概念，ElasticSearch里面的shard对应的才是Lucene的Index。

<br/><br/>
<font size=3 color=green>文档（Document）和字段（Field）</font>
---

一个Index里面会包含若干个文档，文档就像MySQL里面的一行（record）或者HBase里面的一列。文档是Lucene里面索引和搜索的原子单位，就像我们在MySQL里面写数据的时候，肯定是以行为单位的；读的时候也是以行为单位的。当然我们可以指定只读/写行里面某些字段，但仍是以行为单位的，Lucene也是一样，以文档为最小单位。代码里面是这样说明的："Documents are the unit of indexing and search".每个文档都会有一个唯一的文档ID。

文档是一个灵活的概念，不同的业务场景对应的具体含义不同。对于搜索引擎来说，一个文档可能就代表爬虫爬到的一个网页，很多个网页（文档）组成了一个索引。而对于提供检索功能的邮件客户端来说，一个文档可能就代表一封邮件，很多封邮件（文档）组成了一个索引。再比如假设我们要构建一个带全文检索功能的商品管理系统，那一件商品就是一个文档，很多个商品组成了一个索引。对于日志处理，一般是一行日志代表一个文档。

文档里面包含若干个字段，真正的数据是存储在字段里面的。一个字段包含三个要素：名称、类型、值。我们要索引数据，必须将数据以文本形式存储到字段里之后才可以。Lucene的字段由一个key-value组成，就像map一样。value支持多种类型，如果value是一个map类型，那就是嵌套字段了。

最后需要注意的是，不同于传统的关系型数据库，Lucene不要求一个index里面的所有文档的字段要一样，如果你喜欢，每一条文档的结构都可以不一样（当然实际中不建议这样操作），而且不需要事先定义，这个特性一般称之为“flexible schema”。传统的关系型数据库要求一个表里面的所有字段的结构必须一致，而且必事先定义好，一般称之为“strict schema”或者”fixed schema“。比如，有一个名为“mixture”的索引包含3条Document，如下：

```
{
    { "name": "Ni Yanchun", "gender": "male", "age": 28  },
    { "name": "Donald John Trump", "gender": "male", "birthday": "1946.06.14"},
    { "isbn": "978-1-933988-17-7", "price": 60, "publish": "2010", "topic": ["lucene", "search"]}
}
```

可以看到，3 条 Document 的字段并不完全一样，这在 Lucene 中是合法的。

<br/><br/>
<font size=3 color=green> 词元 Token 和 词项 Term</font>
---
Token 是存储在字段中的文本数据经过分词器（Tokenizer）分词后产生的一系列词或者词组，以及这些词或词组本身在原始文本中的一些属性信息，例如可选的词频 TF、位置 postion、字符偏移量 offset、附加数据 payload 等信息，为了表述方便，我们把这些属性统称为 token 的元数据。举例来说，假设有个 "body" 字段的存储的值为 "the quick brown fox jumped over the lazy dog"，这个字段经过 Lucene 的标准分词器分词后的结果是："the" "quick" "brown" "fox" "jumped" "over" "the" "lazy" "dog"。这里的每个词就是一个 token，当然实际上除了词自身外，token 还会包含元数据。

一个 token 加上它原来所属的字段的名称构成了 Term。比如 "body" 和 "quick" 组成一个 Term，"body" 和 "fox" 组成另外一个 Term。我们检索的时候搜的就是 Term，而不是 Token 或者 Document。但搜到 Term 时，会找到包含这个 Term 的文档的 ID 号码，即 DocID，然后通过 DocID 返回整个 Document。注意，Term 通过域的名字 name 和域关联，即 Term 含有域信息，具有不同名字但有相同内容的 Term 是不同的，例如 "title":"fox" 和 "body":"fox" 是不同的 Term 。


<br/><br/>
<font size=3 color=green>索引段 Segment</font>
---

Indexing 的时候，并不是将所有数据写到一起，而是再分了一层，这层就是索引段 segment。索引的时候，会先将 Document 缓存，然后定期刷新到文件。每次刷新就会生成一个索引段。所以一个 Index 包含若干个Segment，每个 Segment 是一个具有完整数据的小型索引，所有的 Segment 组成了整个索引。因此一个索引包含了一个或多个索引段，搜索时，Lucene 检索的就是索引中的每个索引段 Segment，然后将每个段的搜索结果进行合并，得到最终的搜索结果。为了减少文件描述符的使用，这些小的索引段 Segment 会定期的合并为（merge）大的索引段 Segment，数据量不大的时候，合并之后一个 index 可能只有一个 Segment。



