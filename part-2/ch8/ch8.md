# 第8章 Lucene 基本扩展 Essential Lucene extensions #

<div style="background-color:gray;padding:2px;">
<h4>本章要点</h4>
    <ul style="list-style-type:square">
        <li style="font-weight:bold;color:black;">高亮显示搜索结果</li>
        <li style="font-weight:bold;color:black;">纠正搜索文本拼写错误</li>
        <li style="font-weight:bold;color:black;">使用 Luke 工具查看索引细节</li>
        <li style="font-weight:bold;color:black;">使用其它的查询、分析器实现</li>
    </ul>
</div>

<br/>

已将构建了索引库，但不通过写代码就能浏览或查询其内容吗？绝对没问题！本章将探讨的 Luke 工具，就可以完全做到。有超出内置分析器能力的需要吗？Lucene 为多语言的分析提供了多个分析器模块。如何为搜索结果提供词项高亮显示？对此有两个选择。还将探索如何为拼写错误提供建议。

本章考察基本的、最一般性的 Lucene 扩展。












