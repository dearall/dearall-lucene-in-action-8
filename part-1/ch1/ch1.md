# 第1章 初识 Lucene #

<div style="background-color:gray;padding:2px;">
<h4>本章要点</h4>
    <ul style="list-style-type:square">
        <li style="font-weight:bold;color:black;">了解 Lucene</li>
        <li style="font-weight:bold;color:black;">理解典型的搜索程序结构</li>
        <li style="font-weight:bold;color:black;">了解基本的索引 API</li>
        <li style="font-weight:bold;color:black;">了解基本的搜索 API</li>
    </ul>
</div>

<br/>
&emsp;&emsp;Lucene 实际上是一个强大的 Java 搜索库，它能让我们很容易地将搜索功能加入到任何程序中。近年来，Lucene 变得非常流行，同时它也是使用最为广泛的信息检索类库：它隐藏在很多 web 站点或桌面程序背后，为其提供非常强大的搜索特性。虽然 Lucene 是由 Java 编写的，但由于它广泛的流行，以及热心开发者的努力，目前已经可以自由获取大量的针对其它编程语言的 Lucene 版本，例如 C/C++，C#，Ruby，Perl，Python，以及 PHP 等。

&emsp;&emsp;简单易用是 Lucene 广受欢迎的关键因素之一。但不要被这点迷惑：在后台，其实一直默默地运行着极其复杂先进的信息检索技术。Lucene 是一款设计非常优秀的软件，它向用户提供了简单易用的索引和搜索 API，屏蔽了复杂的内部实现过程。开发者不需要深入了解 Lucene 如何进行信息索引和检索工作的原理，就可以开始使用它。再者，Lucene 提供 API 简单直接，只需要学会如何使用它提供的类就可以使用了。

&emsp;&emsp;在本章，我们将分析一个典型搜索程序的总体架构，以及 Lucene 在其中的应用位置。需要指出的是，Lucene 仅仅是一个提供搜索功能的类库，所以开发者还需要根据实际情况自行完成搜索程序的其它组件，例如，网页抓取、文档处理、服务器运行、用户界面和管理等。在具体的分析过程中，首先通过一些现有的代码示例，展示如何使用 Lucene 进行基本的索引和搜索实现，然后简要地介绍在索引和搜索过程中需要了解的全部核心知识点。

&emsp;&emsp;本书内容基于 **Lucene 8.x**，示例代码使用当前最新 **8.11.2** 版本编译通过。由于 Lucene 版本向后兼容特性，书中内容和代码示例可以在所有 Lucene 8.x 版本中运行。

示例代码位于：[https://github.com/dearall/lia-lucene8-source-code.git](https://github.com/dearall/lia-lucene8-source-code.git)












