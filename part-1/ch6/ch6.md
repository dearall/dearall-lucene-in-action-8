# 第6章 扩展搜索 Extending search #

<div style="background-color:gray;padding:2px;">
<h4>本章要点</h4>
    <ul style="list-style-type:square">
        <li style="font-weight:bold;color:black;">创建自定义排序</li>
        <li style="font-weight:bold;color:black;">使用 Collector 接口</li>
        <li style="font-weight:bold;color:black;">自定义查询解析器 QueryParser</li>
        <li style="font-weight:bold;color:black;">使用 positional payloads</li>
    </ul>
</div>

<br/>

第 3 章讨论了 Lucene 内置的基本搜索能力，第 5 章超越基础，深入探究了 Lucene 更高级的搜索特性。在这两章，只是探索了 Lucene 的内置特性。除此之外，Lucene 也提供了多个强大的扩展点，这就是本章要讨论的内容。

&emsp;&emsp;自定义排序在内置的相关性排序或者按域排序不适用的情况下，让我们能够实现通过任意依据排序。通过一个示例展示按地理位置与用户当前位置邻近的次序排序。自定义收集结果，在不想依据一个排序规则排列 top 10 文档时，可以自己任意处理每个匹配的文档，展示两个自定义收集器的示例。QueryParser 有很多的扩展点，以自定义每种类型查询的创建，提供的示例包括防止某种查询类型的创建，处理数值类型和日期类型域。自定义过滤器可以任意限制允许的文档匹配。最后，利用 payload，对同一文档内一个词项出现在特定的位置，给与不同的加权。

&emsp;&emsp;有了对这些强大扩展点的掌握，就可以对 Lucene 的行为，以几乎任意的方式进行自定义。




















