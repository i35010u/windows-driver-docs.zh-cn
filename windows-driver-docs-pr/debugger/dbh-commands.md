---
title: DBH 命令
description: DBH 命令
keywords:
- THIS->DBH，命令
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9f2949f8c74c668ceeadc420a2350e4964318177
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823471"
---
# <a name="dbh-commands"></a>DBH 命令


在 THIS->DBH 命令行中，您可以使用各种命令来分析符号和符号文件。

下表列出了用于控制 THIS->DBH 选项和执行其他基本任务的命令。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">命令</th>
<th align="left">效果</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>详细</strong>[<strong>on</strong> | <strong>off</strong>]</p></td>
<td align="left"><p>打开或关闭详细模式。 如果没有参数，则显示当前详细模式设置。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>sympath</strong> [<em>路径</em>]</p></td>
<td align="left"><p>设置符号搜索路径。 如果没有参数，则显示当前符号搜索路径。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>symopt</strong> <em>选项</em></p>
<p><strong>symopt +</strong><em>选项</em></p>
<p><strong>symopt-</strong><em>选项</em></p>
<p><strong>symopt</strong></p></td>
<td align="left"><p>设置符号选项。 如果不包含 <strong>+</strong> 或 <strong>-</strong> ， <em>选项</em> 的值将替换当前符号选项。 如果 <strong>+</strong> <strong>-</strong> 使用了或，则 <em>选项</em> 指定要添加或删除的选项; 在或后面必须有空格 <strong>+</strong> <strong>-</strong> 。 在没有参数的情况下，将显示当前符号选项。 当 THIS->DBH 启动时，所有符号选项的默认值均为0x10C13。 有关可用选项的列表，请参阅 <a href="symbol-options.md" data-raw-source="[Setting Symbol Options](symbol-options.md)">设置符号选项</a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>help</strong></p></td>
<td align="left"><p>显示 THIS->DBH 命令的帮助文本。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>结束</strong></p></td>
<td align="left"><p>退出 THIS->DBH 程序。</p></td>
</tr>
</tbody>
</table>

 

下表列出了用于加载、卸载和变基目标模块的命令。 如果 THIS->DBH 是通过在命令行上指定进程 ID 启动的，则不能使用这些命令。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">命令</th>
<th align="left">效果</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>加载</strong><em>文件</em></p></td>
<td align="left"><p>加载指定的模块。 <em>文件</em> 应指定可执行文件或符号文件的路径、文件名和文件扩展名。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>[</strong></p></td>
<td align="left"><p>卸载当前模块。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>基</strong><em>址</em></p></td>
<td align="left"><p>将默认基址设置为指定值。 将根据此基址确定所有符号地址。</p></td>
</tr>
</tbody>
</table>

 

下表列出了搜索文件和显示目录信息的命令。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">命令</th>
<th align="left">效果</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>findexe</strong> <em>文件路径</em></p></td>
<td align="left"><p>使用 <strong>FindExecutableImage</strong> 例程在指定路径中查找指定的可执行文件。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>finddbg</strong> <em>文件路径</em></p></td>
<td align="left"><p>在指定的路径中查找指定的 dbg 文件。 包含 dbg 扩展名是可选的。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>目录</strong><em>文件路径</em></p></td>
<td align="left"><p>使用 <strong>EnumDirTree</strong> 例程定位指定路径或此路径下的任何子目录中的指定文件。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>srchtree</strong> <em>路径文件</em></p></td>
<td align="left"><p>使用 <strong>SearchTreeForFile</strong> 例程定位指定路径或此路径下的任何子目录中的指定文件。 除了参数反转外，此命令与 <strong>dir</strong>相同。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>ffpath</strong> <em>文件</em></p></td>
<td align="left"><p>查找当前符号路径中的指定文件。</p></td>
</tr>
</tbody>
</table>

 

下表列出了用于分析模块列表并控制默认模块的命令。 默认模块及其基址显示在 THIS->DBH 提示符下。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">命令</th>
<th align="left">效果</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>mod</strong> <em>地址</em></p></td>
<td align="left"><p>将默认模块更改为具有指定基址的模块。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>刷新</strong></p></td>
<td align="left"><p>刷新模块列表。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>omap</strong></p></td>
<td align="left"><p>显示 module OMAP 结构。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>epmod</strong> <em>PID</em></p></td>
<td align="left"><p>枚举为指定进程加载的所有模块。 <em>PID</em> 指定所需进程的进程 ID。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>信息</strong></p></td>
<td align="left"><p>显示有关当前加载的模块的信息。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>obj</strong> <em>掩码</em></p></td>
<td align="left"><p>列出与与指定模式匹配的默认模块关联的所有对象文件。 <em>掩码</em> 可能包含各种通配符和说明符;有关详细信息，请参阅 <a href="string-wildcard-syntax.md" data-raw-source="[String Wildcard Syntax](string-wildcard-syntax.md)">字符串通配符语法</a> 。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>src</strong> <em>掩码</em></p></td>
<td align="left"><p>列出与指定模式匹配的默认模块关联的所有源文件。 <em>掩码</em> 可能包含各种通配符和说明符;有关详细信息，请参阅 <a href="string-wildcard-syntax.md" data-raw-source="[String Wildcard Syntax](string-wildcard-syntax.md)">字符串通配符语法</a> 。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>enummod</strong></p></td>
<td align="left"><p>枚举所有已加载的模块。 始终存在至少一个模块，除非在没有目标的情况下运行 THIS->DBH，在这种情况下没有任何目标。</p></td>
</tr>
</tbody>
</table>

 

下表列出了用于显示和搜索符号的命令。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">命令</th>
<th align="left">效果</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>枚举</strong><em>模块</em><strong>！</strong><em>符号</em></p></td>
<td align="left"><p>枚举与指定的模块和符号匹配的所有符号。 <em>模块</em> 指定要搜索 (的模块，而不) 文件扩展名。 <em>符号</em> 指定符号必须包含的模式。 <em>模块</em>和<em>符号</em>可能包含各种通配符和说明符;有关详细信息，请参阅<a href="string-wildcard-syntax.md" data-raw-source="[String Wildcard Syntax](string-wildcard-syntax.md)">字符串通配符语法</a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>enumaddr</strong> <em>地址</em></p></td>
<td align="left"><p>枚举与指定地址相关联的所有符号。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>addr</strong> <em>地址地址</em></p></td>
<td align="left"><p>显示与指定地址相关联的符号的详细信息。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>名称</strong> [<em>Module</em><strong>！</strong>]<em>符号</em></p></td>
<td align="left"><p>显示有关指定符号的详细信息。 可以包含可选的 <em>模块</em> 说明符。 不应使用通配符，因为如果多个符号与模式匹配，则 <strong>name</strong> 仅显示其中的第一个。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>下一步</strong> [<em>Module</em><strong>！</strong>]<em>符号</em></p>
<p><strong>下一个</strong><em>地址</em></p></td>
<td align="left"><p>显示有关指定符号或地址后面的下一个符号的详细信息。 如果符号由名称指定，则可以包含可选的 <em>模块</em> 说明符，但不应使用通配符。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>上</strong> 一个 [<em>Module</em><strong>！</strong>]<em>符号</em></p>
<p><strong>上</strong>一个 <em>地址</em></p></td>
<td align="left"><p>显示有关指定符号或地址之前的第一个符号的详细信息。 如果符号由名称指定，则可以包含可选的 <em>模块</em> 说明符，但不应使用通配符。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>行</strong><em>文件</em> <strong>#</strong> <em>LineNum</em></p></td>
<td align="left"><p>显示与指定的源行关联的二进制指令的十六进制地址以及与此行关联的任何符号。 还将当前行号设置为等于指定的行号。 <em>File</em> 指定源文件的名称， <em>LineNum</em> 指定该文件中的行号;应使用数字符号 ( ) 来分隔这些值 <strong>#</strong> 。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>srclines</strong> <em>文件 LineNum</em></p></td>
<td align="left"><p>显示与指定的源行关联的对象文件，以及与此行关联的二进制指令的十六进制地址。 不会更改当前行号。 <em>File</em> 指定源文件的名称， <em>LineNum</em> 指定该文件中的行号;它们应该用空格分隔。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>laddr</strong> <em>地址</em></p></td>
<td align="left"><p>显示与位于指定地址处的符号相对应的源文件和行号。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>linenext</strong></p></td>
<td align="left"><p>递增当前行号，并显示有关新行号的信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>lineprev</strong></p></td>
<td align="left"><p>减少当前行号，并显示有关新行号的信息。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>局部变量</strong><em>函数</em>[<em>Mask</em>]</p></td>
<td align="left"><p>显示指定函数中包含的所有局部变量。 如果包含 <em>掩码</em> ，则只显示与指定模式匹配的局部变量;有关详细信息，请参阅 <a href="string-wildcard-syntax.md" data-raw-source="[String Wildcard Syntax](string-wildcard-syntax.md)">字符串通配符语法</a> 。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>类型类型</strong><em>名称</em></p></td>
<td align="left"><p>显示有关指定数据类型的详细信息。 <em>TypeName</em> 指定数据类型的名称 (例如 WSTRING) 。 如果没有与此值匹配的类型名称，则将显示任何匹配的符号。 与大多数 THIS->DBH 命令参数不同， <em>TypeName</em> 区分大小写。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>elines</strong> [<em>源</em> [<em>Obj</em>]]</p></td>
<td align="left"><p>枚举与指定的源掩码和对象掩码匹配的所有源行。 <em>Source</em> 指定源文件的名称，包括绝对路径和文件扩展名。 <em>Obj</em> 指定对象文件的名称，包括相对路径和文件扩展名。 <em>源</em>和<em>Obj</em>都可能包含各种通配符和说明符;有关详细信息，请参阅<a href="string-wildcard-syntax.md" data-raw-source="[String Wildcard Syntax](string-wildcard-syntax.md)">字符串通配符语法</a>。 如果省略参数，则此参数等效于使用星号 (<strong> <em> </strong>) 通配符。 如果你不希望指定路径信息，请在文件名前加上 <strong> </em> &lt; /strong &gt; 以指示通配符路径。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>索引</strong><em>值</em></p></td>
<td align="left"><p>显示具有指定索引值的符号的详细信息。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>作用域</strong><em>地址</em></p>
<p><strong>scope</strong> [<em>Module</em><strong>！</strong>]<em>符号</em></p></td>
<td align="left"><p>显示有关指定符号的父对象的详细信息。 符号可以按 address 或 name 指定。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>srch</strong> [<strong>mask =</strong><em>Symbol</em>] [<strong>index =</strong><em>index</em>] [<strong>tag =</strong><em>tag</em>] [<strong>addr =</strong><em>Address</em>] [<strong>globals</strong>]</p></td>
<td align="left"><p>搜索与指定掩码匹配的所有符号。 <em>符号</em> 指定符号名称。 它不应包含模块名称，但它可以包含通配符和说明符;有关详细信息，请参阅 <a href="string-wildcard-syntax.md" data-raw-source="[String Wildcard Syntax](string-wildcard-syntax.md)">字符串通配符语法</a> 。 <em>Index</em> 指定要用作搜索父级的符号的十六进制地址。 <em>标记</em> 指定十六进制符号类型分类器 (<strong>SymTag</strong><em>Xxx</em>) 值，该值必须与符号匹配。 <em>Address</em> 指定符号的地址。 如果包含 <strong>globals</strong> ，将只显示全局符号。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>uw</strong> <em>地址</em></p></td>
<td align="left"><p>显示指定地址处的函数的展开信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>dtag</strong></p></td>
<td align="left"><p>显示所有符号类型分类器 (<strong>SymTag</strong><em>Xxx</em>) 值。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>etypes</strong></p></td>
<td align="left"><p>枚举所有数据类型。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>dump</strong></p></td>
<td align="left"><p>显示目标文件中所有符号信息的完整列表。</p></td>
</tr>
</tbody>
</table>

 

下表列出了与符号服务器和符号存储区相关的命令。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">命令</th>
<th align="left">效果</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>home</strong> [<em>路径</em>]</p></td>
<td align="left"><p>设置 SymSrv 和 Srcsrv.ini 用于默认下游存储的主目录。 如果符号路径包含对使用默认下游存储的符号服务器的引用，则主目录的 <strong>符号</strong> 子目录将用于下游存储。 如果没有参数， <strong>home</strong> 将显示当前主目录。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>srvpath</strong> <em>路径</em></p></td>
<td align="left"><p>测试指定的路径是否为符号存储区的路径。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>srvind</strong> <em>文件</em></p></td>
<td align="left"><p>查找对应于指定文件的符号服务器索引。 符号服务器索引是基于文件内容的唯一值，而不考虑它是否确实已添加到任何符号存储区中。 <em>文件</em> 应指定所需文件的文件名和绝对路径。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>fii</strong> <em>文件</em></p></td>
<td align="left"><p>显示指定的二进制文件及其关联文件的符号服务器索引。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>getfile</strong> <em>文件索引</em></p></td>
<td align="left"><p>显示具有指定名称和符号服务器索引的文件。 <em>文件</em> 指定所需文件的名称;这不应包含其路径。 <em>Index</em> 指定所需文件的符号服务器索引。 THIS->DBH 使用 <strong>SymFindFileInPath</strong> 例程搜索此名称和此索引所在的文件的当前符号路径下的树。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>sup</strong> <em>路径 File1 File2</em></p></td>
<td align="left"><p>根据参数的值，将文件存储在符号存储区中。 <em>路径</em> 指定符号存储区的目录路径。 <em>File1</em> 和 <em>File2</em> 用于创建增量值，该值又用于确定所存储的文件。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>storeadd</strong> <em>文件存储</em></p></td>
<td align="left"><p>将指定的文件添加到指定的符号存储区。 <em>存储</em> 应是符号存储区的根路径。</p></td>
</tr>
</tbody>
</table>

 

下表列出了适用于实部和虚部的 THIS->DBH 命令。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">命令</th>
<th align="left">效果</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>undec</strong> <em>名称</em></p></td>
<td align="left"><p>显示附加到指定符号名称的修饰的含义。 <em>名称</em> 可以是任何字符串;它不需要与当前加载的符号相对应。 如果 <em>Name</em> 包含 c + + 修饰，则显示这些修饰的含义。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>添加</strong><em>名称地址大小</em></p></td>
<td align="left"><p>将指定的虚符号添加到在 THIS->DBH 中加载的符号列表。 <em>名称</em> 指定要添加的符号的名称， <em>Address</em> 指定其十六进制地址，并将其十六进制大小 <em>大小</em> （以字节为单位）。 此处理方式类似于后面的 THIS->DBH 命令中的任何其他符号，直到 THIS->DBH 会话以 <strong>quit</strong> 或 <strong>unload</strong>结束，或直到用 <strong>del</strong>删除了虚部。实际目标符号文件未更改。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>del</strong> <em>名称</em></p>
<p><strong>del</strong> <em>地址</em></p></td>
<td align="left"><p>删除先前使用 <strong>add</strong> 命令添加的虚部。 可以按名称或地址指定符号。 这不能用于删除实际符号。</p></td>
</tr>
</tbody>
</table>

 

 

 





