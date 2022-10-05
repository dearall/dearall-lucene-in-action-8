# 第7章 利用 Tika 提取文本 Extracting text with Tika #

<div style="background-color:gray;padding:2px;">
<h4>本章要点</h4>
    <ul style="list-style-type:square">
        <li style="font-weight:bold;color:black;">理解 Tika 的逻辑设计</li>
        <li style="font-weight:bold;color:black;">使用 Tika 内置工具和 API 提取文本</li>
        <li style="font-weight:bold;color:black;">解析 XML</li>
        <li style="font-weight:bold;color:black;">处理已知的 Tika 限制</li>
    </ul>
</div>

<br/>

在构建搜索程序时，一个经常而重要的步骤就是从文件中提取出文本，以用于建立索引。在幸运的情况下，应用程序处理的数据已经是文本格式的，或者文件都是同一种格式的，例如 XML 文件或数据库中有规则的行。如果不幸，就必须面对当前流行的庞大的文件格式，例如 Outlook、Word、Excel、PowerPoint、Visio、Flash、PDF、OpenOffice、富文本格式（RTF），甚至是存档文件格式，例如 TAR、ZIP、BZIP2 等。看起来似乎是的文本格式，如 XML 或 HTML，也面临挑战，因为必须小心处理，以避免偶尔将任何标签或 JavaScrip 代码包含到文本内容中。纯文本格式看起来最简单了，但要确定其字符集可能也不那么容易。

&emsp;&emsp;在过去，单干就可以了：跟踪自己的文档过滤器，一个接一个地，并通过它们特有的 API 交互提取出所需的文本。也会自己检测文档类型和字符编码。所幸的是，现在有一个开源的 Tika 框架，在 Apache 顶级项目之下，可以为我们处理大部分的工作。

Tika 具有简单易用的 API，提供一个文档源，然后就可以从中检索出经过滤的文本内容。








