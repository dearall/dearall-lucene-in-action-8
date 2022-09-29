# 第5章 高级搜索技术 Advanced search techniques #

<div style="background-color:gray;padding:2px;">
<h4>本章要点</h4>
    <ul style="list-style-type:square">
        <li style="font-weight:bold;color:black;">为所有文档加载域值</li>
        <li style="font-weight:bold;color:black;">对搜索结果进行过滤和排序</li>
        <li style="font-weight:bold;color:black;">跨度查询和功能查询</li>
        <li style="font-weight:bold;color:black;">利用词向量</li>
        <li style="font-weight:bold;color:black;">停止较慢的搜索</li>
    </ul>
</div>

<br/>

很多使用 Lucene 实现搜索的应用程序，通过第 3 章介绍的 API 就可以完成了。然而，有些项目则需要比基本搜索机制更高级的技术才能实现。比如，或许需要安全过滤器来限制特定的用户哪些文档是他可搜索的，或者更喜欢通过指定的域对搜索结果排序，例如标题，而不是通过相关性进行排序。使用词向量 term vectors，可以找到与现有的某个文档相似的文档，或者自动将文档归类。功能查询（function query）在计算命中评分时可以允许使用任意的逻辑计算，使我们可以根据最近的操作为相关性评分增加权重。本章讨论所有这些应用案例。

&emsp;&emsp;本章探讨的高级主题包括：
- 创建跨度查询（span query），一种高级查询技术，密切关注结果中匹配词项的位置信息。
- 使用 MultiPhraseQuery 查询，在短语查询中应用同义词技术。
- 横跨多个 Lucene 索引库进行搜索。
- 超过指定的时间限定后停止搜索。
- 使用 QueryParser 的变体来一次性搜索多个域。


























