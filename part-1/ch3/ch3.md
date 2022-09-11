# 第3章 为程序添加搜索功能 Adding search to your application #

<div style="background-color:gray;padding:2px;">
<h4>本章要点</h4>
    <ul style="list-style-type:square">
        <li style="font-weight:bold;color:black;">对索引执行查询</li>
        <li style="font-weight:bold;color:black;">使用 Lucene 内置查询</li>
        <li style="font-weight:bold;color:black;">处理搜索结果</li>
        <li style="font-weight:bold;color:black;">理解 Lucene 评分机制</li>
        <li style="font-weight:bold;color:black;">解析查询表达式</li>
    </ul>
</div>

<br/>
&emsp;&emsp;上一章，展示了非常详细的构建索引的过程，而这一切都是为了搜索。只有在索引之上建立搜索才能体现出它的价值。本章，我们将展示如何充分利用索引过程所付出的努力。作为案例，考虑如下场景：

&emsp;&emsp;*给我一个最近 12 个月出版的有关 "Java" 并且内容包含 "open source" 或 "Jakata" 的所有书籍列表。要求它们都是特价书。哦，要求涉及 "Apache" 的书也包含在内，因为我们显式指定了 "Jakata"。并且为了使其反映迅速，要求毫秒级响应时间*。

&emsp;&emsp;类似这样的场景，利用 Lucene 可以轻松处理，即便内容源由几百万文档组成。而且这个案例会带领我们通过三章的内容，学习必要的 Lucene 搜索功能，完全实现案例的要求。我们从经常用到的搜索 API 开始，这是本章的内容。实际上，大多数应用程序只使用本章的内容，就可以提供非常优秀的搜索功能。但搜索引擎程序是只与其搜索能力表现相当的，而这正是 Lucene 出色的地方。在第 4 章，我们将学习 Lucene 的分析过程，这是很重要的一章，因为在索引过程和搜索操作中都会用到它。之后，再回到关于搜索的第 5 章，深入探讨关于 Lucene 的搜索能力，然后进入第 6 章，详细论述扩展 Lucene 类以实现更强大的自定义搜索能力。

&emsp;&emsp;本章从一个简单的示例程序开始，展示实现搜索的代码一般没有几行。接下来展示 Lucene 评分公式，深入探讨 Lucene 的这个特殊特性。通过示例及较高层次理解 Lucene 对搜索结果进行评分，本章会利用较大篇幅探索 Lucene 内置的各种搜索查询，包括通过匹配指定的词项（term）查询、范围查询（数值的或文本的）、前缀或通配符查询、短语查询、模糊查询等等。展示如何利用强大的布尔查询（BooleanQuery）来将多个子句连接起来构造复合查询。最后将展示，如何利用 Lucene 的 QueryParser 类，从最终用户输入的文本搜索表达式，创建复杂的搜索查询。

&emsp;&emsp;本章是三章有关 Lucene 搜索 API 的第一章，因此目前会限制对这些 API 做深入讨论，表 3.1 列出搜索集成常用的主要类。

<div align=center>表 3.1 Lucene 主要的搜索 API</div>

<table>
    <tr bgcolor=#AA0000>
        <th align=center>类</th>
        <th align=center>目的</th>
    </tr>
    <tr>
        <td>IndexSearcher</td>
        <td>搜索索引库的入口。所有的搜索操作都要通过 IndexSearcher 实例进行，利用其重载的多个 search 方法</td>
    </tr>
    <tr>
        <td>IndexReader</td>
        <td>访问索引库时间点视图的接口，IndexSearcher 通过该类实例只读访问索引库，实现对其搜索</td>
    </tr>
    <tr>
        <td>Query (及其子类)</td>
        <td>具体的子类封装了某一特定类型查询的逻辑。Query 实例传递给 IndexSearcher 的 search 方法，以执行搜索</td>
    </tr>
    <tr>
        <td>QueryParser</td>
        <td>将用户输入的文本（人类可读）表达式解析成一个具体的 Query 对象</td>
    </tr>
    <tr>
        <td>TopDocs</td>
        <td>IndexSearcher.search() 方法返回的搜索结果对象，持有匹配文档的 ScoreDoc 数组</td>
    </tr>
    <tr>
        <td>ScoreDoc</td>
        <td>表示搜索结果每一个匹配文档，持有匹配文档的 docID 和评分值（score），及其分片索引 （shardIndex）</td>
    </tr>
</table>

&emsp;&emsp;对索引库进行查询时，IndexSearcher 会返回一个 TopDocs 实例，其中包含一个已排序的 ScoreDoc 数组，数组默认按文档评分值排序。Lucene 对一个给定的查询，为每一个匹配的文档计算一个评分值（是一个表示相关性的数值），ScoreDoc 本身并不表示实际的匹配文档，而是匹配文档的引用，通过整型的文档 ID，即 docID 指向匹配的文档。大多数程序只显示匹配结果的前几个文档，因此没有必要检索出所有匹配结果的所有文档，因此，我们只需要检索出当前页文档展现给用户就可以了。实际上，对于超大的索引，将索引匹配文档收集到有限的物理内存中也是不大可能的，即便可行，也会耗费太长的时间。




