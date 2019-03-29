---
title: DBH 命令
description: DBH 命令
ms.assetid: 124e8be9-1b1a-4498-84a4-5dbb6b5b9026
keywords:
- DBH 命令
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6901252e447d6635428b41b42d48f50b6a9f7e59
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575951"
---
# <a name="dbh-commands"></a>DBH 命令


从 DBH 命令行中，可以使用各种命令来分析符号和符号文件。

下表列出了控制 DBH 选项和执行其他基本任务的命令。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Command</th>
<th align="left">效果</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>verbose</strong> [<strong>on</strong>|<strong>off</strong>]</p></td>
<td align="left"><p>打开或关闭详细模式。 不使用任何参数，将显示当前详细模式设置。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>sympath</strong> [<em>Path</em>]</p></td>
<td align="left"><p>设置符号搜索路径。 不使用任何参数，将显示当前符号搜索路径。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>symopt</strong> <em>选项</em></p>
<p><strong>symopt +</strong><em>选项</em></p>
<p><strong>symopt-</strong><em>选项</em></p>
<p><strong>symopt</strong></p></td>
<td align="left"><p>设置符号选项。 不带<strong>+</strong>或<strong>-</strong>的值<em>选项</em>替换当前符号选项。 如果<strong>+</strong>或<strong>-</strong>使用，则<em>选项</em>指定的选项来添加或删除; 必须有之前的空格<strong>+</strong>或<strong>-</strong> ，但它后的没有空格。 不使用任何参数，将显示当前的符号选项。 当启动 DBH 时，所有符号选项的默认值是 0x10C13。 有关可用选项的列表，请参阅<a href="symbol-options.md" data-raw-source="[Setting Symbol Options](symbol-options.md)">设置符号选项</a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>help</strong></p></td>
<td align="left"><p>显示帮助文本 DBH 命令。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>quit</strong></p></td>
<td align="left"><p>退出 DBH 程序。</p></td>
</tr>
</tbody>
</table>

 

下表列出了加载、 卸载，和重定基本值目标模块的命令。 通过在命令行上指定进程 ID 已启动 DBH，不能使用这些命令。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Command</th>
<th align="left">效果</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>加载</strong><em>文件</em></p></td>
<td align="left"><p>加载指定的模块。 <em>文件</em>应指定路径、 文件名和可执行文件或符号文件的文件扩展名。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>unload</strong></p></td>
<td align="left"><p>卸载当前的模块。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>基</strong><em>地址</em></p></td>
<td align="left"><p>为指定的值设置的默认基址。 所有符号地址将都确定相对于此基址。</p></td>
</tr>
</tbody>
</table>

 

下表列出了文件搜索和显示目录信息的命令。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Command</th>
<th align="left">效果</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>findexe</strong> <em>文件路径</em></p></td>
<td align="left"><p>定位指定的可执行文件中指定的路径，使用<strong>FindExecutableImage</strong>例程。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>finddbg</strong> <em>文件路径</em></p></td>
<td align="left"><p>在指定的路径中找到指定的.dbg 文件。 包括.dbg 扩展名是可选的。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>dir</strong> <em>文件路径</em></p></td>
<td align="left"><p>定位指定的文件中指定的路径或在此路径下的任何子目录中使用<strong>EnumDirTree</strong>例程。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>srchtree</strong> <em>文件路径</em></p></td>
<td align="left"><p>定位指定的文件中指定的路径或在此路径下的任何子目录中使用<strong>SearchTreeForFile</strong>例程。 此命令等同于<strong>dir</strong>，只不过参数进行了互换。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>ffpath</strong> <em>文件</em></p></td>
<td align="left"><p>在当前符号路径中查找指定的文件。</p></td>
</tr>
</tbody>
</table>

 

下表列出了分析的模块列表和控件的默认模块的命令。 DBH 提示上显示的默认模块和其基址。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Command</th>
<th align="left">效果</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>mod</strong> <em>地址</em></p></td>
<td align="left"><p>更改为具有指定的基址的模块的默认模块。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>refresh</strong></p></td>
<td align="left"><p>刷新模块列表。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>omap</strong></p></td>
<td align="left"><p>显示模块 OMAP 结构。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>epmod</strong> <em>PID</em></p></td>
<td align="left"><p>枚举加载的指定进程的所有模块。 <em>PID</em>指定所需的进程的进程 ID。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>info</p></td>
<td align="left"><p>显示有关当前已加载模块的信息。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>obj</strong> <em>Mask</em></p></td>
<td align="left"><p>列出关联的所有对象文件与默认模块与指定的模式匹配。 <em>掩码</em>可能包含多个通配符和说明符; 请参阅<a href="string-wildcard-syntax.md" data-raw-source="[String Wildcard Syntax](string-wildcard-syntax.md)">字符串通配符语法</a>有关详细信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>src</strong> <em>掩码</em></p></td>
<td align="left"><p>列出所有源关联文件的默认模块与指定的模式匹配。 <em>掩码</em>可能包含多个通配符和说明符; 请参阅<a href="string-wildcard-syntax.md" data-raw-source="[String Wildcard Syntax](string-wildcard-syntax.md)">字符串通配符语法</a>有关详细信息。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>enummod</strong></p></td>
<td align="left"><p>枚举所有已加载的模块。 将始终至少一个模块，除非 DBH 运行且目标未在此情况下没有任何表。</p></td>
</tr>
</tbody>
</table>

 

下表列出的命令的显示和搜索符号。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Command</th>
<th align="left">效果</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>枚举</strong><em>模块</em><strong>！</strong><em>符号</em></p></td>
<td align="left"><p>枚举匹配指定的模块和符号的所有符号。 <em>模块</em>指定要搜索 （不带文件扩展名） 的模块。 <em>符号</em>指定模式，它必须包含符号。 这两<em>模块</em>并<em>符号</em>可能包含多个通配符和说明符; 请参阅<a href="string-wildcard-syntax.md" data-raw-source="[String Wildcard Syntax](string-wildcard-syntax.md)">字符串通配符语法</a>有关详细信息。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>enumaddr</strong> <em>Address</em></p></td>
<td align="left"><p>枚举与指定的地址相关联的所有符号。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>addr</strong> <em>Address</em></p></td>
<td align="left"><p>显示详细信息与指定的地址相关联的符号。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>名称</strong>[<em>模块</em><strong>！</strong>]<em>符号</em></p></td>
<td align="left"><p>显示有关指定的符号的详细的信息。 一个可选<em>模块</em>说明符中可能包含。 通配符不应使用，因为如果多个符号与模式匹配<strong>名称</strong>仅显示其中的第一个。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>下一步</strong>[<em>模块</em><strong>！</strong>]<em>符号</em></p>
<p><strong>下一步</strong><em>地址</em></p></td>
<td align="left"><p>显示有关详细信息的下一个符号后的指定的符号或地址。 如果按名称、 可选指定符号<em>模块</em>说明符中可能包含，但不是应使用通配符。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>prev</strong> [<em>模块</em><strong>！</strong>]<em>符号</em></p>
<p><strong>prev</strong> <em>Address</em></p></td>
<td align="left"><p>显示详细信息之前指定的符号或地址的第一个符号。 如果按名称、 可选指定符号<em>模块</em>说明符中可能包含，但不是应使用通配符。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>line</strong> <em>File</em><strong>#</strong><em>LineNum</em></p></td>
<td align="left"><p>显示与指定的源行相关的二进制说明和与此行关联的任何符号的十六进制的地址。 此外将设置为当前行号等于指定的行号。 <em>文件</em>指定的源文件的名称和<em>LineNum</em>指定该文件; 中的行号它们应分隔以井号 ( <strong> #</strong> )。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>srclines</strong> <em>文件 LineNum</em></p></td>
<td align="left"><p>显示与指定的源行和与此行关联的二进制说明的十六进制地址相关联的对象文件。 不会更改当前的行号。 <em>文件</em>指定的源文件的名称和<em>LineNum</em>指定该文件; 中的行号应使用空格分隔这些。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>laddr</strong> <em>Address</em></p></td>
<td align="left"><p>显示位于指定的地址的符号与对应的源代码文件和行号。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>linenext</strong></p></td>
<td align="left"><p>递增当前行号，并显示有关新的行号信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>lineprev</strong></p></td>
<td align="left"><p>递减当前行号，并显示有关新的行号信息。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>局部变量</strong><em>函数</em>[<em>掩码</em>]</p></td>
<td align="left"><p>显示指定的函数中包含的所有本地变量。 如果<em>掩码</em>是包含，显示那些与指定的模式匹配的局部变量; 请参阅<a href="string-wildcard-syntax.md" data-raw-source="[String Wildcard Syntax](string-wildcard-syntax.md)">字符串通配符语法</a>有关详细信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>type</strong> <em>TypeName</em></p></td>
<td align="left"><p>显示有关指定的数据类型的详细的信息。 <em>TypeName</em>指定数据类型 (例如，WSTRING) 的名称。 如果没有类型名称与此值匹配，将显示任何匹配的符号。 大多数 DBH 命令与参数不同， <em>TypeName</em>区分大小写。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>elines</strong> [<em>Source</em> [<em>Obj</em>]]</p></td>
<td align="left"><p>枚举与指定的源掩码和对象掩码匹配的所有源行。 <em>源</em>指定源文件，其中包括绝对路径和文件扩展名的名称。 <em>Obj</em>指定对象文件，其中包括相对路径和文件扩展名的名称。 这两<em>源</em>并<em>Obj</em>可能包含多个通配符和说明符; 请参阅<a href="string-wildcard-syntax.md" data-raw-source="[String Wildcard Syntax](string-wildcard-syntax.md)">字符串通配符语法</a>有关详细信息。 如果省略一个参数，这相当于使用星号 (<strong><em></strong>) 通配符。 如果不希望指定路径的信息，请使用文件名称前缀<strong> </em> &lt;/ 强&gt;可指示通配符路径。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>index</strong> <em>Value</em></p></td>
<td align="left"><p>显示有关指定的索引值的符号的详细的信息。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>作用域</strong><em>地址</em></p>
<p><strong>作用域</strong>[<em>模块</em><strong>！</strong>]<em>符号</em></p></td>
<td align="left"><p>显示有关指定的符号的父级的详细的信息。 通过地址或名称，可能指定的符号。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>srch</strong> [<strong>mask=</strong><em>Symbol</em>] [<strong>index=</strong><em>Index</em>] [<strong>tag=</strong><em>Tag</em>] [<strong>addr=</strong><em>Address</em>] [<strong>globals</strong>]</p></td>
<td align="left"><p>搜索与指定的掩码匹配的所有符号。 <em>符号</em>指定符号名称。 它不应包含模块名称，但它可能包含通配符字符和说明符;请参阅<a href="string-wildcard-syntax.md" data-raw-source="[String Wildcard Syntax](string-wildcard-syntax.md)">字符串通配符语法</a>有关详细信息。 <em>索引</em>指定的符号用作搜索父十六进制的地址。 <em>标记</em>指定十六进制符号类型分类器 (<strong>SymTag</strong><em>Xxx</em>) 必须与匹配的符号的值。 <em>地址</em>指定符号的地址。 如果<strong>globals</strong>是包含，就会显示仅全局符号。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>uw</strong> <em>Address</em></p></td>
<td align="left"><p>显示指定地址处的函数的展开信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>dtag</strong></p></td>
<td align="left"><p>显示所有符号类型分类器 (<strong>SymTag</strong><em>Xxx</em>) 值。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>etypes</strong></p></td>
<td align="left"><p>枚举的所有数据类型。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>dump</strong></p></td>
<td align="left"><p>显示目标文件中的所有符号信息的完整列表。</p></td>
</tr>
</tbody>
</table>

 

下表列出了与符号服务器和符号存储区关联的命令。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Command</th>
<th align="left">效果</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>home</strong> [<em>Path</em>]</p></td>
<td align="left"><p>设置用于 SymSrv 和 SrcSrv 默认下游存储的主目录。 如果符号路径包含一个引用到符号服务器使用默认下游存储区，则<strong>sym</strong>主目录的子目录用于下游应用商店。 不使用任何参数，<strong>家庭</strong>显示当前的主目录。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>srvpath</strong> <em>Path</em></p></td>
<td align="left"><p>测试指定的路径是否符号存储区的路径。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>srvind</strong> <em>文件</em></p></td>
<td align="left"><p>查找对应于指定的文件的符号服务器索引。 符号服务器索引是基于文件，无论是否实际已添加到任何符号存储区的内容的唯一值。 <em>文件</em>应指定文件的名称和所需的文件的绝对路径。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>fii</strong> <em>文件</em></p></td>
<td align="left"><p>显示指定的二进制文件及其关联的文件的符号服务器索引。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>getfile</strong> <em>文件索引</em></p></td>
<td align="left"><p>显示具有指定名称和符号服务器索引的文件。 <em>文件</em>指定名称的所需的文件; 这不应包含其路径。 <em>索引</em>指定所需的文件的符号服务器索引。 使用 DBH <strong>SymFindFileInPath</strong>例程，以搜索具有此名称，此索引的文件的当前符号路径下的树。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>sup</strong> <em>路径 File1 File2</em></p></td>
<td align="left"><p>将文件存储在符号存储区中，根据参数的值。 <em>路径</em>指定符号存储区的目录路径。 <em>File1</em>并<em>File2</em>用于创建一个增量值，这反过来又用于确定要存储的文件。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>storeadd</strong> <em>文件存储</em></p></td>
<td align="left"><p>将指定的文件添加到指定的符号存储区。 <em>存储</em>应符号存储区的根路径。</p></td>
</tr>
</tbody>
</table>

 

下表列出了适用于实部和虚部的符号的 DBH 命令。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Command</th>
<th align="left">效果</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>undec</strong> <em>Name</em></p></td>
<td align="left"><p>将显示附加到指定的符号名称的修饰的含义。 <em>名称</em>可以是任意字符串; 它不需要对应的当前加载的符号。 如果<em>名称</em>包含 c + + 修饰显示这些修饰的含义。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>添加</strong><em>名称地址大小</em></p></td>
<td align="left"><p>将指定的虚部符号添加到在 DBH 中加载的符号的列表。 <em>名称</em>指定要添加的符号名称<em>地址</em>指定其十六进制的地址，以及<em>大小</em>其十六进制大小 （字节）。 这都被视为在更高版本 DBH 命令中，任何其他符号，直到 DBH 会话结尾<strong>退出</strong>或<strong>卸载</strong>，或直到使用删除的虚符号<strong>del</strong>。不会更改实际目标符号文件。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>del</strong> <em>Name</em></p>
<p><strong>del</strong> <em>地址</em></p></td>
<td align="left"><p>删除以前添加的虚部符号<strong>添加</strong>命令。 按名称或地址，可以指定的符号。 这不能用于删除实际的符号。</p></td>
</tr>
</tbody>
</table>

 

 

 





