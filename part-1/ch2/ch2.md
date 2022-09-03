## 第二章 构建索引 Building a search index ##

<div style="background-color:gray;padding:2px;">
<h4>本章要点</h4>
    <ul style="list-style-type:square">
        <li style="font-weight:bold;color:black;">理解索引基本概念</li>
        <li style="font-weight:bold;color:black;">执行基本的索引操作</li>
        <li style="font-weight:bold;color:black;">理解 Field 及其子类</li>
        <li style="font-weight:bold;color:black;">高级索引技术</li>
    </ul>
</div>

<br/>
&emsp;&emsp;如果要搜索存储在磁盘上的文件、电子邮件、网页或是数据库中的数据，Lucene 都可以完成。但在进行搜索之前，必须先对搜索内容进行索引（indexing），以建立索引库。搜索和索引是 Lucene 的两大核心任务，有了索引库，Lucene 才能以此为数据基础实现搜索功能。

&emsp;&emsp;搜索程序的最终目的是为了能够快速高效地检索到与查询信息匹配的结果。索引是搜索功能的数据提供者，如何搜索数据，就如何为数据建立索引，怎样能提高搜索的性能，就怎样建立索引数据。索引过程建立和维护索引数据，而搜索则是消费索引库中数据的过程。因此，为了高效地执行数据搜索，Lucene 建立了丰富的数据结构和算法来对不同类型的原始数据建立索引。而对于应用开发者而言，并不需要详细了解这些底层复杂的结构和算法，Lucene 为开发者提供了丰富的用户级 API 接口，用于控制各种类型数据建立索引的细节，屏蔽了底层数据结构和算法的复杂性，同时也屏蔽了因版本迭代而带来的底层结构和算法变化对应用的影响。

&emsp;&emsp;索引是搜索的基础，建立合理且优化的索引数据库，是整个搜索程序效率的关键。本章将详细讨论有关建立高效率索引库的过程及其各方面的细节，以供搜索功能进行高效的全文检索。
