# 第4章 Lucene 的分析过程 Lucene’s analysis process #

<div style="background-color:gray;padding:2px;">
<h4>本章要点</h4>
    <ul style="list-style-type:square">
        <li style="font-weight:bold;color:black;">理解分析过程</li>
        <li style="font-weight:bold;color:black;">使用 Lucene 核心分析类</li>
        <li style="font-weight:bold;color:black;">编写自定义分析器</li>
        <li style="font-weight:bold;color:black;">处理非英语语种</li>
    </ul>
</div>

<br/>

**分析（analysis）**，在 Lucene 中，指的是将域的文本转换成最基本的索引表现形式，即词项的过程。这些词项在搜索期间用于确定哪些文档匹配一个查询。例如，如果这句话 "For example, if you indexed this sentence in a field" 被索引到一个域中，那么对应的词项就会从 for 和 example 开始，然后以此类推，按序排列每个切分开的词项。一个**分析器（analyzer）是分析过程的封装**。分析器对文本执行一系列的操作，将其切分成词元（token），包括提取出单词，去除标点符号，从字符上移除重音，转换成小写形式（也称为规范化 normalizing），去除普通词汇，将单词还原到词干形式（词干还原 stemming），还或者将单词转换为其基本形式（词形还原 lemmatization）。这个过程也称为 **词元化过程（tokenization）**，而从文本流中提取出来的文本块（chunk of text）称为 **词元（token）**。词元，和它关联的域名称组合在一起，称为 **词项（term）**。

&emsp;&emsp;开发 Lucene 的主要目的是使 **信息检索（information retrieval）** 更加便捷。强调检索是非常重要的。我们希望向 Lucene 加入大量的文本，并且希望通过文本中的单词完全可以搜索到相关文档。为了让 Lucene 知道什么是 “单词（word）”，它在索引期间分析文本，将它提取成词项，而这些词项就是用于搜索的基础构建块。

&emsp;&emsp;使用 Lucene，选择合适的分析器是至关重要的开发决策，一种选择不会适用于所有场景。语种因素之一，因为每个语种都有其自身独有的特性。影响分析器选择的另一因素是被分析文本所属的领域，不同的行业有不同的术语、缩略词（acronyms）和缩略语（abbreviations），应该值得注意。尽管我们在选择分析器时考虑了很多因素，但是没有单个能够适用于所有情况的分析器。很可能没有内置的分析器能满足我们的需要，这旧的我们自己投入精力来创建一个自定义的分析方案，幸运的是，Lucene 的构建模块使得这一过程非常容易。

&emsp;&emsp;在本章我们将探讨 Lucene 分析过程的方方面面，包括如何和在哪里使用分析器，内置的分析器做了什么，以及如何利用 Lucene 提供的核心 API 构建块编写自定义分析器。自定义分析器很容易构建，很多搜索程序都这么做，因此示例代码将演示的内容包括同义词注入（synonym injection）、近音词搜索（sounds-like searching）、词干还原（stemming）和停用词过滤（stop-word filtering）等内容。








