---
title: 使用 DML 自定义调试器输出
description: 调试器标记语言 (DML) 提供了一种机制增强来自调试器和扩展的输出。
ms.assetid: 04984510-B95F-405F-81DF-E9D0673210B4
ms.date: 11/13/2018
ms.localizationpriority: medium
ms.openlocfilehash: a734a7c41b28019e0b59fe63ba4a5120e9ed1527
ms.sourcegitcommit: d334150abe0b189faf33049908af7aab1458c13d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57464163"
---
# <a name="customizing-debugger-output-using-dml"></a>使用 DML 自定义调试器输出


调试器标记语言 (DML) 提供了一种机制增强来自调试器和扩展的输出。 与 HTML 类似，调试器的标记支持允许将输出包括显示指令和额外非显示的标记窗体中的信息。 调试器用户界面，WinDbg 等中分析出提供在 DML 来增强所显示的信息，并提供新行为，如网格显示和排序的额外信息。 本主题介绍如何自定义使用 DML 您调试输出。 有关启用和使用中的 DML 的常规信息的调试器，请参阅[使用调试器标记语言](debugger-markup-language-commands.md)。

DML 是可用在 Windows 10 及更高版本。

## <a name="span-iddmloverviewspanspan-iddmloverviewspanspan-iddmloverviewspandml-overview"></a><span id="DML_Overview"></span><span id="dml_overview"></span><span id="DML_OVERVIEW"></span>DML 概述


上的 DML 的主要权益以提供链接到调试器输出中的相关信息的能力。 一个主要的 DML 标记的是&lt;链接&gt;标记用于指示是否可以通过链接访问与一种输出相关的信息输出生成者的说明操作。 为使用 web 浏览器中的 HTML 链接这样用户能够导航超链接的信息。

提供超链接内容的优点是，它可用于增强的调试程序和调试器扩展功能可发现性。 调试器和及其扩展插件包含大量的功能，但它可能很难确定要在不同的方案中使用的相应命令。 用户必须只需知道哪些命令可以用来在特定方案中使用。 用户和内核调试之间的差异会进一步增加复杂性。 这通常意味着许多用户不了解可帮助他们的调试命令。 DML 链接提供了任意调试命令来包装在备用的演示文稿，例如说明性文本，可单击的菜单系统或链接的帮助功能。 使用 DML，可以对命令输出来增强用户引导到适用于手头的任务的其他相关命令。

**调试器 DML 支持**

-   命令窗口在 WinDbg 中的支持所有 DML 行为，将显示颜色、 字体样式和链接。
-   使用颜色模式已启用，则返回 true 的控制台中运行时，控制台调试器 – ntsd、 cdb 和 kd – 仅支持 DML，和唯一的颜色属性。
-   通过重定向 I/O 的调试器，ntsd – d 或 remote.exe 会话不会显示任何颜色。

## <a name="span-iddmlcontentspecificationspanspan-iddmlcontentspecificationspanspan-iddmlcontentspecificationspandml-content-specification"></a><span id="DML_Content_Specification"></span><span id="dml_content_specification"></span><span id="DML_CONTENT_SPECIFICATION"></span>DML 内容规范


DML 不应为完整表示语言，如 HTML。 DML 是精心设计的非常简单，只有少量的标记。

由于并非所有调试器工具都支持多格式文本，DML 旨在允许 DML 和纯文本之间的简单转换。 这样，DML 所有现有的调试器工具中的函数。 可以轻松地支持颜色等效果，因为删除它们不会删除携带的实际信息的文本。

DML 不是 XML。 DML 不会尝试执行语义，也不是结构化信息。 如上所述，必须有一个简单之间的映射 DML 和纯文本，因此，DML 标记是所有可放弃。

DML 不是可扩展的;所有标记是预定义的并验证，以跨所有现有的调试器工具工作。

**标记结构**

类似于 XML，DML 标记可以作为起点&lt;tagname \[args\] &gt;并且下列&lt;/tagname&gt;。

**特殊字符**

DML 内容大致遵循特殊字符的 XML/HTML 的规则。 字符 &、 &lt;，&gt;和"很特殊，不能使用以纯文本。 等效的转义字符的版本为 &、 &lt;，&gt;和"。 例如此文本：

"Alice 和 Bob 想 3 &lt; 4"

将转换为以下 dml。

```text
"Alice & Bob think 3 &lt 4"
```

**C 编程语言格式设置字符**

大的不同之处，从 XML/HTML 规则是 DML 文本可以包括 C 编程语言流样式格式设置字符，例如\\b \\t \\r 和\\n。 这是为了支持与现有调试器文本生成和使用的兼容性。

## <a name="span-idexampledmlspanspan-idexampledmlspanspan-idexampledmlspanexample-dml"></a><span id="Example_DML"></span><span id="example_dml"></span><span id="EXAMPLE_DML"></span>示例 DML


假设文件 c:\\Dml\_Experiment.txt 包含以下行。

```text
My DML Experiment
<link cmd="lmD musb*">List modules that begin with usb.</link>
```

以下命令命令浏览器窗口中显示的文本和链接。

```dbgcmd
.browse .dml_start c:\Dml_Experiment.txt
```

![dml 文件输出的屏幕截图](images/dmlcommands03.png)

如果单击**列表的开头 usb 模块**链接，请参阅下图类似的输出。

![模块列表的屏幕截图](images/dmlcommands04.png)

## <a name="span-idright-clickbehaviorindmlspanspan-idright-clickbehaviorindmlspanspan-idright-clickbehaviorindmlspanright-click-behavior-in-dml"></a><span id="Right-Click_Behavior_in_DML"></span><span id="right-click_behavior_in_dml"></span><span id="RIGHT-CLICK_BEHAVIOR_IN_DML"></span>右键单击 DML 中的行为


右键单击行为是 DML 中可用。 此示例演示如何定义行为使用右键单击&lt;altlink&gt;发送断点[**最佳实践 （设置断点）** ](bp--bu--bm--set-breakpoint-.md)命令并将发送[ **u （反汇编）** ](u--unassemble-.md)正则单击。

```text
<link cmd="u MyProgram!memcpy">
<altlink name="Set Breakpoint (bp)" cmd="bp MyProgram!memcpy" />
u MyProgram!memcpy
</link>
```

## <a name="span-iddmltagreferencespanspan-iddmltagreferencespanspan-iddmltagreferencespandml-tag-reference"></a><span id="DML_Tag_Reference"></span><span id="dml_tag_reference"></span><span id="DML_TAG_REFERENCE"></span>DML 标记参考


### <a name="span-idlinkspanspan-idlinkspanltlinkgt"></a><span id="_link_"></span><span id="_LINK_"></span>&lt;link&gt;

*&lt;链接\[名称 ="text"\] \[cmd ="调试器\_命令"\]\[alt ="将鼠标悬停显示的文本"\] \[部分 ="name"\] &gt;链接文本 &lt; /链接&gt;*

链接标记是 DML 中的基本超链接机制。 它指示用户界面来支持 DML 演示文稿链接文本显示为可单击的链接。 单击与 cmd 规范的链接时执行调试器命令和相应的输出应替换当前的输出。

名称和部分参数允许为命名链接，类似于 HTML 的之间的导航&lt;名称&gt;和\#命名支持。 当在 UI 上单击的链接具有部分参数名为具有匹配名称的链接将扫描并将滚动到视图的。 这允许链接以指向同一页面的不同部分 （或新页的特定部分）。 DML 的节名称是单独为了避免必须定义一种新语法，以允许命令字符串末尾的部分名称。

转换为纯文本中删除标记。

**示例**

```text
<b> Handy Links </b>
<link cmd="!dml_proc">Display process information with DML rendering.</link>
<link cmd="kM">Display stack information with DML rendering.</link>
```

**示例**

此示例演示如何使用 alt 属性创建时你将鼠标悬停 DML 链接将显示的文本。

```text
<b>Hover Example</b>
<link cmd="lmD" alt="This link will run the list modules command and display the output in DML format">LmD</link>
```

### <a name="span-idaltlinkspanspan-idaltlinkspanltaltlinkgt"></a><span id="_altlink_"></span><span id="_ALTLINK_"></span>&lt;altlink&gt;

*&lt;altlink \[name=”text”\] \[cmd=”debugger\_command”\] \[section=”name”\]&gt;alt link text&lt;/altlink&gt;*

&lt;Altlink&gt;标记提供了右键单击行为是 DML 中可用。 单击与 cmd 规范的链接时执行调试器命令和相应的输出应替换当前的输出。 &lt;Altlink&gt;选项卡通常与配对&lt;链接&gt;标记以支持常规和右键单击行为。

转换为纯文本中删除标记。

**示例**

此示例演示如何定义行为使用右键单击&lt;altlink&gt;发送断点[**最佳实践 （设置断点）** ](bp--bu--bm--set-breakpoint-.md)命令并将发送[ **u （反汇编）** ](u--unassemble-.md)正则单击。

```text
<link cmd="u MyProgram!memcpy">
<altlink name="Set Breakpoint (bp)" cmd="bp MyProgram!memcpy" />
u MyProgram!memcpy
</link>
```

### <a name="span-idexecspanspan-idexecspanltexecgt"></a><span id="_exec_"></span><span id="_EXEC_"></span>&lt;exec&gt;

*&lt;exec cmd ="调试器\_命令"&gt;说明性文本&lt;/exec&gt;*

Exec 标记类似于是链接标记中的说明性文本应显示为可单击的项。 但是，当在命令浏览器窗口中使用 exec 标记时，而无需替换当前的输出执行给定的命令，此标记提供了一种方法执行单击一下，从一个菜单命令。

转换为纯文本中删除标记。

**示例**

此示例演示如何定义正则单击两个命令。

```text
<b>Exec Sample</b>
<exec cmd="!dml_proc">Display process information with DML rendering.</exec>
<exec cmd="kM">Display stack information with DML rendering.</exec>
```

### <a name="span-idbspanspan-idbspanltbgt"></a><span id="_b_"></span><span id="_B_"></span>&lt;b&gt;

*&lt;b&gt;粗体文本 &lt; /b&gt;*

此标记请求以粗体显示。 &lt;B&gt;，&lt;我&gt;并&lt;u&gt;可以嵌套以混合的属性。

转换为纯文本中删除标记。

**示例**

此示例演示如何为粗体文本。

```text
<b>This is bold Text</b>
```

### <a name="span-idispanspan-idispanltigt"></a><span id="_i_"></span><span id="_I_"></span>&lt;i&gt;

*&lt;我&gt;斜体文本&lt;/i&gt;*

此标记请求斜体。 &lt;B&gt;，&lt;我&gt;并&lt;u&gt;可以嵌套以混合的属性。

转换为纯文本中删除标记。

**示例**

此示例演示如何以文本变为斜体。

```text
<i>This is italicized Text</i>
```

### <a name="span-iduspanspan-iduspanltugt"></a><span id="_u_"></span><span id="_U_"></span>&lt;u&gt;

*&lt;u&gt;带下划线的文本&lt;/u&gt;*

此标记请求带下划线的文本。 &lt;B&gt;，&lt;我&gt;并&lt;u&gt;可以嵌套以混合的属性。

转换为纯文本中删除标记。

**示例**

此示例演示如何以带有下划线的文本。

```text
<u>This is underlined Text</u>
```

**示例**

此示例演示如何组合标记来设置粗体、 下划线和斜体文本。

```text
<b><u><i>This is bold, underlined and italizized text. </i></u></b> 
```

### <a name="span-idcolspanspan-idcolspanltcolgt"></a><span id="_col_"></span><span id="_COL_"></span>&lt;col&gt;

&lt;col fg="name" bg="name"&gt;text&lt;/col&gt;

请求的文本的前景色和背景色。 因为这样将允许客户控制他们将看到哪种颜色，颜色可以为已知颜色而不是绝对值的名称。 当前颜色名称 （默认值仅适用于 WinDbg）。

**前景色和背景元素标记**

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><strong>设置</strong></td>
<td align="left"><strong>说明 / 示例</strong></td>
</tr>
<tr class="even">
<td align="left"><p>wbg-Windows 背景</p>
<p>wfg-Windows 前景色</p></td>
<td align="left">默认窗口前景色和背景颜色。 默认为窗口和窗口文本的系统颜色。
<p>&lt;col fg ="wfg"bg ="wbg"&gt;这是标准的前景 / 背景文本&lt;/col&gt;</p></td>
</tr>
<tr class="odd">
<td align="left"><p>clbg 的当前行的前景色</p>
<p>clfg 的当前行背景</p></td>
<td align="left">当前行背景和前景颜色。 默认为突出显示的系统颜色和突出显示文本。
<p>&lt;col fg="clfg" bg="clbg"&gt; Test Text - Current Line&lt;/col&gt;</p></td>
</tr>
<tr class="even">
<td align="left"><p>empbg 的重要背景</p>
<p>emphfg-重要的前景色</p></td>
<td align="left">加粗的文本。 默认为浅蓝色。
<p>&lt;col fg ="empfg"bg ="empbg"&gt;这是强调前景 / 背景文本&lt;/col&gt;</p></td>
</tr>
<tr class="odd">
<td align="left"><p>subbg-Subdued 背景</p>
<p>subfg Subdued 前景色</p></td>
<td align="left">Subdued 的文本。 默认为非活动标题文本和非活动状态的隐藏式字幕的系统颜色。
<p>&lt;col fg ="subfg"bg ="subbg"&gt;这是 subdued 的前景 / 背景文本&lt;/col&gt;</p></td>
</tr>
<tr class="even">
<td align="left"><p>normbg 的正常后台</p>
<p>normfg-正常的前景色</p></td>
<td align="left">正常
<p>&lt;col fg ="normfg"bg ="normbg"&gt;测试文本-正常 (normfg / normbg) &lt;/col&gt;</p></td>
</tr>
<tr class="odd">
<td align="left"><p>warnbg-警告背景</p>
<p>warnfg-警告前景色</p></td>
<td align="left">警告
<p>&lt;col fg ="warnfg"bg ="warnbg"&gt;测试文本-警告 (warnfg / warnbg) &lt;/col&gt;</p></td>
</tr>
<tr class="even">
<td align="left"><p>errbg-错误背景</p>
<p>errfg-错误前景色</p></td>
<td align="left">错误
<p>&lt;col fg ="errfg"bg ="errbg"&gt;测试文本的错误 (errfg / errbg) &lt;/col&gt;</p></td>
</tr>
<tr class="odd">
<td align="left"><p>verbbg-Verbose 背景</p>
<p>verbfg-Verbose 前景色</p></td>
<td align="left">Verbose
<p>&lt;col fg ="verbfg"bg ="verbbg"&gt;测试文本-Verbose (verbfg / verbbg) &lt;/col&gt;</p></td>
</tr>
</tbody>
</table>



**源代码单个元素标记**

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>srcnum-源数值常量</p></td>
<td align="left">源元素的颜色。
<p>&lt;col fg="srcnum" bg="wbg"&gt; Test Text - srcnum &lt;/col&gt;</p></td>
</tr>
<tr class="even">
<td align="left"><p>srcchar-源字符常量</p></td>
<td align="left"><p>&lt;col fg="srcchar" bg="wbg"&gt; Test Text - srcchar &lt;/col&gt;</p></td>
</tr>
<tr class="odd">
<td align="left"><p>srcstr-源字符串常量</p></td>
<td align="left"><p>&lt;col fg="srcstr" bg="wbg"&gt; Test Text - srcstr &lt;/col&gt;</p></td>
</tr>
<tr class="even">
<td align="left"><p>srcid-源标识符</p></td>
<td align="left"><p>&lt;col fg="srcid " bg="wbg"&gt; Test Text - srcid &lt;/col&gt;</p></td>
</tr>
<tr class="odd">
<td align="left"><p>srckw 关键字</p></td>
<td align="left"><p>&lt;col fg ="srckw"bg ="wbg"&gt;测试文本-srckw &lt;/col&gt;</p></td>
</tr>
<tr class="even">
<td align="left"><p>srcpair-源大括号或匹配的符号对</p></td>
<td align="left"><p>&lt;col fg="srcpair" bg="empbbg"&gt; Test Text - srcpair &lt;/col&gt;</p></td>
</tr>
<tr class="odd">
<td align="left"><p>srccmnt-源注释</p></td>
<td align="left"><p>&lt;col fg ="srccmnt"bg ="wbg"&gt;测试文本-srccmnt &lt;/col&gt;</p></td>
</tr>
<tr class="even">
<td align="left"><p>srcdrct-源指令</p></td>
<td align="left"><p>&lt;col fg="srcdrct" bg="wbg"&gt; Test Text - srcdrct &lt;/col&gt;</p></td>
</tr>
<tr class="odd">
<td align="left"><p>srcspid-源特殊标识符</p></td>
<td align="left"><p>&lt;col fg="srcspid" bg="wbg"&gt; Test Text - srcspid &lt;/col&gt;</p></td>
</tr>
<tr class="even">
<td align="left"><p>srcannot-源批注</p></td>
<td align="left"><p>&lt;col fg="srcannot" bg="wbg"&gt; Test Text - srcannot &lt;/col&gt;</p></td>
</tr>
<tr class="odd">
<td align="left"><p>更改-更改的数据</p></td>
<td align="left">用于自以前的停止点，例如在 WinDbg 中已更改注册以来已更改的数据。 默认值为红色。
<p>&lt;col fg ="更改"bg ="wbg"&gt;测试文本-更改&lt;/col&gt;</p></td>
</tr>
</tbody>
</table>



## <a name="span-iddmlexamplecodespanspan-iddmlexamplecodespanspan-iddmlexamplecodespandml-example-code"></a><span id="DML_Example_Code"></span><span id="dml_example_code"></span><span id="DML_EXAMPLE_CODE"></span>DML 的示例代码


此示例代码说明了以下。

-   调用调试命令
-   实现右键单击命令
-   实现悬停文本
-   使用颜色和丰富的文本

```XML
<col fg="srckw" bg="wbg"> <b>
*******************************************************
*** Example debug commands for crash dump analysis ****
*******************************************************
</b></col>
<col fg="srcchar" bg="wbg"><i>
**** Hover over commands for additional information ****
        **** Right-click for command help ****
</i></col>

<col fg="srccmnt" bg="wbg"><b>*** Common First Steps for Crash Dump Analysis ***</b> </col>
<link cmd=".symfix" alt="Set standard symbol path using .symfix">.symfix<altlink name="Help about .symfix" cmd=".hh .symfix" /> </link> - Set standard symbol path
<link cmd=".sympath+ C:\Symbols" alt="This link adds addtional symbol directories">.sympath+ C:\Symbols<altlink name="Help for .sympath" cmd=".hh .sympath" /> </link> - Add any additional symbol directories, for example C:\Symbols
<link cmd=".reload /f" alt="This link reloads symbols">.reload /f<altlink name="Help for .reload" cmd=".hh .reload" /> </link> - Reloads symbols to make sure they are in good shape
<link cmd="!analyze -v" alt="This link runs !analyze with the verbose option">!analyze -v<altlink name="Help for !analyze" cmd=".hh !analyze" /> </link> - Run !analyze with the verbose option
<link cmd="vertarget" alt="This link runs checks the target version">vertarget<altlink name="Help for vertarget" cmd=".hh vertarget" /></link> - Check the target version
<link cmd="version" alt="This link displays the versions in use">version<altlink name="Help for version" cmd=".hh version" /></link> - Display the versions in use
<link cmd=".chain /D" alt="This link runs .chain">.chain /D<altlink name="Help for .chain" cmd=".hh .chain" /></link> - Use the .chain /D command to list debugger extensions
<link cmd="kM" alt="This link displays the stack backtrace using DML">kD<altlink name="Help for k" cmd=".hh k, kb, kc, kd, kp, kP, kv (Display Stack Backtrace)" /> </link> - Display the stack backtrace using DML rendering
<link cmd="lmD" alt="This link will run the list modules command and display the output in DML format">LmD<altlink name="Help for lmD" cmd=".hh lm" /> </link> - List modules command and display the output in DML format
<link cmd=".help /D" alt="Display help for commands">.help /D <altlink name="Help for .dot commands" cmd=".hh commands" /></link> - Display help for commands in WinDbg
<link cmd=".hh" alt="Start help">.hh<altlink name="Debugger Reference Help".hh Contents" cmd=".hh Debugger Reference" /></link> - Start help

<col fg="srccmnt" bg="wbg"><b>*** Registers and Context ***</b></col>
<link cmd="r" alt="This link displays registers">r<altlink name="Help about r command" cmd=".hh r" /></link>  - Display registers
<link cmd="dt nt!_CONTEXT" alt="This link displays information about nt_CONTEXT">dt nt!_CONTEXT<altlink name="Help about the dt command" cmd=".hh dt" /></link> - Display information about nt_CONTEXT
<link cmd="dt nt!_PEB" alt="This link calls the dt command to display nt!_PEB">dt nt!_PEB<altlink name="Help about dt command" cmd=".hh dt" /></link> - Display information about the nt!_PEB
<link cmd="ub" alt="This link unassembles backwards">ub<altlink name="Help about ub command" cmd=".hh u, ub, uu (Unassemble)" /></link> - Unassemble Backwards

<col fg="srcchar" bg="wbg"><i>
**** Note: Not all of the following commands will work with all crash dump data ****
</i></col>
<col fg="srccmnt" bg="wbg"><b>*** Device Drivers ***</b></col>
<link cmd="!devnode 0 1" alt="This link displays the devnodes">!devnode 0 1<altlink name="Help about !devnode command" cmd=".hh !devnode" /></link> - Display devnodes
<link cmd=".load wdfkd.dll;!wdfkd.help" alt="Load wdfkd extensions and display help">.load wdfkd.dll;!wdfkd.help<altlink name="Help about the wdfkd extensions" cmd=".hh !wdfkd" /></link> - Load wdfkd extensions and display help
<link cmd="!wdfkd.wdfldr" alt="This link displays !wdfkd.wdfldr">!wdfkd.wdfldr<altlink name="Help about !wdfkd.wdfldr" cmd=".hh !wdfkd.wdfldr" /></link>  - Display WDF framework driver loader information
<link cmd="!wdfkd.wdfumtriage" alt="This link displays !wdfkd.umtriage">!wdfkd.umtriage<altlink name="Help about !wdfkd.umtriage" cmd=".hh !wdfkd_wdfumtriage" /></link> - Display WDF umtriage driver information

<col fg="srccmnt" bg="wbg"><b>*** IRPs and IRQL ***</b></col>
<link cmd="!processirps" alt="This link displays process IRPs">!processirps<altlink name="Help about !processirps command" cmd=".hh !processirps" /></link> - Display process IRPs
<link cmd="!irql" alt="This link displays !irql">!irql<altlink name="Help about !irql command" cmd=".hh !irql" /></link> - Run !irql

<col fg="srccmnt" bg="wbg"><b>*** Variables and Symbols ***</b></col>
<link cmd="dv" alt="This link calls the dv command">dv<altlink name="Help about dv command" cmd=".hh dv" /></link> - Display the names and values of all local variables in the current scope

<col fg="srccmnt" bg="wbg"><b>*** Threads, Processes, and Stacks ***</b></col>
<link cmd="!threads" alt="This link displays threads">!threads<altlink name="Help about the !threads command" cmd=".hh !threads" /></link> - Display threads
<link cmd="!ready 0xF" alt="This link runs !ready 0xF">!ready 0xF<altlink name="Help about the !ready command" cmd=".hh !ready" /></link> - Display threads in the ready state
<link cmd="!process 0 F" alt="This link runs !process 0 F ">!process 0 F<altlink name="Help about the !process command" cmd=".hh !process" /></link> - Run !process 0 F
<link cmd="!stacks 2" alt="This link displays stack information using !stacks 2 ">!stacks 2<altlink name="Help about the !stacks command" cmd=".hh !stacks" /></link> - Display stack information using !stacks 2
<link cmd=".tlist" alt="This link displays a process list using TList ">tlist<altlink name="Help about the TList command" cmd=".hh .tlist" /></link> - Display a process list using tlist
<link cmd="!process" alt="This link displays process ">!process<altlink name="Help about the !process command" cmd=".hh !process" /></link> - Display process information
<link cmd="!dml_proc" alt="This link displays process information with DML rendering.">!dml_proc<altlink name="Help about the !dml_proc command" cmd=".hh !dml_proc" /></link> - Display process information with DML rendering
```

此示例代码演示如何使用颜色和格式设置标记。

```XML
*** Text Tag Examples ****

<b>This is bold text</b>
<u>This is underlined text</u>
<i>This is italizized text</i>
<b><u><i>This is bold, underlined and italizized text</i></u></b>

<b>Color Tag Examples</b>
<col fg="wfg" bg="wbg"> This is standard foreground / background text </col>
<col fg="empfg" bg="empbg"> This is emphasis foreground / background text </col>
<col fg="subfg" bg="subbg"> This is subdued foreground / background text </col>
<col fg="clfg" bg="clbg"> Test Text - Current Line</col>

<b>Other Tags Sets</b>
<col fg="normfg" bg="normbg"> Test Text - Normal (normfg / normbg) </col>
<col fg="warnfg" bg="warnbg"> Test Text - Warning (warnfg / warnbg) </col>
<col fg="errfg" bg="errbg"> Test Text - Error (errfg / errbg) </col>
<col fg="verbfg" bg="verbbg"> Test Text - Verbose (verbfg / verbbg) </col>

<b>Changed Text Tag Examples</b>
<col fg="changed" bg="wbg"> Test Text - Changed</col>

<b>Source Tags - using wbg background</b>
<col fg="srcnum" bg="wbg"> Test Text - srcnum  </col>
<col fg="srcchar" bg="wbg"> Test Text - srcchar  </col>
<col fg="srcstr" bg="wbg"> Test Text - srcstr  </col>
<col fg="srcid " bg="wbg"> Test Text - srcid   </col>
<col fg="srckw" bg="wbg"> Test Text - srckw </col>
<col fg="srcpair" bg="empbbg"> Test Text - srcpair </col>
<col fg="srccmnt" bg="wbg"> Test Text - srccmnt  </col>
<col fg="srcdrct" bg="wbg"> Test Text - srcdrct </col>
<col fg="srcspid" bg="wbg"> Test Text - srcspid </col>
<col fg="srcannot" bg="wbg"> Test Text - srcannot </col>

<b>Source Tags - using empbg background</b>
<col fg="srcnum" bg="empbg"> Test Text - srcnum  </col>
<col fg="srcchar" bg="empbg"> Test Text - srcchar  </col>
<col fg="srcstr" bg="empbg"> Test Text - srcstr  </col>
<col fg="srcid " bg="empbg"> Test Text - srcid   </col>
<col fg="srckw" bg="empbg"> Test Text - srckw </col>
<col fg="srcpair" bg="empbbg"> Test Text - srcpair </col>
<col fg="srccmnt" bg="empbg"> Test Text - srccmnt  </col>
<col fg="srcdrct" bg="empbg"> Test Text - srcdrct </col>
<col fg="srcspid" bg="empbg"> Test Text - srcspid </col>
<col fg="srcannot" bg="empbg"> Test Text - srcannot </col>

<b>Source Tags - using subbg background</b>
<col fg="srcnum" bg="subbg"> Test Text - srcnum  </col>
<col fg="srcchar" bg="subbg"> Test Text - srcchar  </col>
<col fg="srcstr" bg="subbg"> Test Text - srcstr  </col>
<col fg="srcid " bg="subbg"> Test Text - srcid   </col>
<col fg="srckw" bg="subbg"> Test Text - srckw </col>
<col fg="srcpair" bg="subbg"> Test Text - srcpair </col>
<col fg="srccmnt" bg="subbg"> Test Text - srccmnt  </col>
<col fg="srcdrct" bg="subbg"> Test Text - srcdrct </col>
<col fg="srcspid" bg="subbg"> Test Text - srcspid </col>
<col fg="srcannot" bg="subbg"> Test Text - srcannot </col>
```

## <a name="span-iddmladditionstothedbgenginterfacespanspan-iddmladditionstothedbgenginterfacespanspan-iddmladditionstothedbgenginterfacespandml-additions-to-the-dbgeng-interface"></a><span id="DML_Additions_to_the_dbgeng_Interface"></span><span id="dml_additions_to_the_dbgeng_interface"></span><span id="DML_ADDITIONS_TO_THE_DBGENG_INTERFACE"></span>Dbgeng 接口 DML 新增功能


[调试器引擎和扩展 Api](debugger-engine-and-extension-apis.md)提供接口以使用调试器引擎来创建自定义应用程序。 此外可以编写自定义扩展插件将在 WinDbg、 KD、 CDB 和 NTSD 中运行。 有关详细信息请参阅[编写 DbgEng 扩展](writing-dbgeng-extensions.md)。 本部分介绍调试器引擎接口的可用 DML 增强功能。

Dbgeng 已有一组文本处理输入的法和输出接口，DML 的使用仅需要执行输入和输出文本中的内容类型的规范。

**为 dbgeng 提供 DML 内容**

输出控制标志调试\_OUTCTL\_DML 指示 dbgeng 方法生成的文本应作为 DML 内容进行处理。 如果未指定此标志的文本视为纯文本格式上下文。 调试\_OUTCTL\_可以使用以下方法使用 DML。

-   [**IDebugControl4::ControlledOutput**](https://msdn.microsoft.com/library/windows/hardware/ff539248)
-   [**IDebugControl4::ControlledOutputVaList**](https://msdn.microsoft.com/library/windows/hardware/ff539252)
-   [**IDebugControl4::ControlledOutputWide**](https://msdn.microsoft.com/library/windows/hardware/ff539266)
-   [**IDebugControl4::ControlledOutputVaListWide**](https://msdn.microsoft.com/library/windows/hardware/ff539259)

给定的文本必须遵循有效字符的 DML 的规则。

所有输出例程已得到都增强，允许新的格式说明符 %\[h | w\]Y {t}。 此格式说明符已作为自变量的字符串指针，并指示给定的文本是纯文本以及应将转换为 DML 格式输出处理过程。 这样，调用方的 DML 内容中包括纯文本，而无需预先转换为 DML 格式本身的简单方法。 H 和 w 限定符表示与 %的 ANSI 或 Unicode 文本。

下表总结了使用 %Y 格式说明符。

|        |                                                                                                                                                                                                                                    |
|--------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| %Y{t}  | 带引号的字符串。 会将文本转换为 DML，如果输出格式 （第一个参数） 是 DML。                                                                                                                                                   |
| %Y{T}  | 带引号的字符串。 将始终将文本转换为 DML 无论输出格式。                                                                                                                                                    |
| %Y {s}  | 不带引号的字符串。 会将文本转换为 DML，如果输出格式 （第一个参数） 是 DML。                                                                                                                                                 |
| %Y{S}  | 不带引号的字符串。 将始终将文本转换为 DML 无论输出格式。                                                                                                                                                  |
| %Y{as} | ULONG64。 添加一个空字符串或填充调试器格式化指针字段的高 32 位部分的间距的 9 个字符。 额外的空间输出 9 空格包括上限 8 零再加上\`字符。 |
| %Y{ps} | ULONG64。 多余空间用于填充调试器格式化指针字段 (包括上限 8 零再加上\`字符)。                                                                                                             |
| %Y{l}  | ULONG64。 地址作为源行信息。                                                                                                                                                                                       |



此代码片段演示如何使用 %Y 格式说明符。

```cpp
HRESULT CALLBACK testout(_In_ PDEBUG_CLIENT pClient, _In_ PCWSTR /*pwszArgs*/)
{
    HRESULT hr = S_OK;

    ComPtr<IDebugControl4> spControl;
    IfFailedReturn(pClient->QueryInterface(IID_PPV_ARGS(&spControl)));

    spControl->ControlledOutputWide(DEBUG_OUTCTL_DML, DEBUG_OUTPUT_NORMAL, L"DML/NORMAL Y{t}: %Y{t}\n", L"Hello <World>");
    spControl->ControlledOutputWide(DEBUG_OUTCTL_DML, DEBUG_OUTPUT_NORMAL, L"DML/NORMAL Y{T}: %Y{T}\n", L"Hello <World>");
    spControl->ControlledOutputWide(DEBUG_OUTCTL_DML, DEBUG_OUTPUT_NORMAL, L"DML/NORMAL Y{s}: %Y{s}\n", L"Hello <World>");
    spControl->ControlledOutputWide(DEBUG_OUTCTL_DML, DEBUG_OUTPUT_NORMAL, L"DML/NORMAL Y{S}: %Y{S}\n", L"Hello <World>");

    spControl->ControlledOutputWide(0, DEBUG_OUTPUT_NORMAL, L"TEXT/NORMAL Y{t}: %Y{t}\n", L"Hello <World>");
    spControl->ControlledOutputWide(0, DEBUG_OUTPUT_NORMAL, L"TEXT/NORMAL Y{T}: %Y{T}\n", L"Hello <World>");
    spControl->ControlledOutputWide(0, DEBUG_OUTPUT_NORMAL, L"TEXT/NORMAL Y{s}: %Y{s}\n", L"Hello <World>");
    spControl->ControlledOutputWide(0, DEBUG_OUTPUT_NORMAL, L"TEXT/NORMAL Y{S}: %Y{S}\n", L"Hello <World>");

    spControl->ControlledOutputWide(DEBUG_OUTCTL_DML, DEBUG_OUTPUT_NORMAL, L"DML/NORMAL Y{a}: %Y{a}\n", (ULONG64)0x00007ffa7da163c0);
    spControl->ControlledOutputWide(DEBUG_OUTCTL_DML, DEBUG_OUTPUT_NORMAL, L"DML/NORMAL Y{as} 64bit   : '%Y{as}'\n", (ULONG64)0x00007ffa7da163c0);
    spControl->ControlledOutputWide(DEBUG_OUTCTL_DML, DEBUG_OUTPUT_NORMAL, L"DML/NORMAL Y{as} 32value : '%Y{as}'\n", (ULONG64)0x1);

    spControl->ControlledOutputWide(DEBUG_OUTCTL_DML, DEBUG_OUTPUT_NORMAL, L"DML/NORMAL Y{ps} 64bit   : '%Y{ps}'\n", (ULONG64)0x00007ffa7da163c0);
    spControl->ControlledOutputWide(DEBUG_OUTCTL_DML, DEBUG_OUTPUT_NORMAL, L"DML/NORMAL Y{ps} 32value : '%Y{ps}'\n", (ULONG64)0x1);

    spControl->ControlledOutputWide(DEBUG_OUTCTL_DML, DEBUG_OUTPUT_NORMAL, L"DML/NORMAL Y{l}: %Y{l}\n", (ULONG64)0x00007ffa7da163c0);

    return hr;

}
```

此示例代码会生成以下输出。

```dbgcmd
0:004> !testout
DML/NORMAL Y{t}: "Hello <World>"
DML/NORMAL Y{T}: "Hello <World>"
DML/NORMAL Y{s}: Hello <World>
DML/NORMAL Y{S}: Hello <World>
TEXT/NORMAL Y{t}: "Hello <World>"
TEXT/NORMAL Y{T}: "Hello &lt;World&gt;"
TEXT/NORMAL Y{s}: Hello <World>
TEXT/NORMAL Y{S}: Hello &lt;World&gt;
DML/NORMAL Y{a}: 00007ffa`7da163c0
DML/NORMAL Y{as} 64bit   : '         '
DML/NORMAL Y{as} 32value : '         '
DML/NORMAL Y{ps} 64bit   : '        '
DML/NORMAL Y{ps} 32value : '        '
DML/NORMAL Y{l}: [d:\th\minkernel\kernelbase\debug.c @ 443]
```

更多控制标志，调试\_OUTCTL\_AMBIENT\_DML，而无需修改任何 out 输出控件特性允许 DML 上下文文本的规范。 调试\_OUTCTL\_AMBIENT\_文本已添加还为更具描述性的别名对先前已调试\_OUTCTL\_AMBIENT。 Dbgeng.h 中定义的输出控制标志。

```cpp
#define DEBUG_OUTCTL_DML               0x00000020

// Special values which mean leave the output settings
// unchanged.
#define DEBUG_OUTCTL_AMBIENT_DML       0xfffffffe
#define DEBUG_OUTCTL_AMBIENT_TEXT      0xffffffff

// Old ambient flag which maps to text.
#define DEBUG_OUTCTL_AMBIENT           DEBUG_OUTCTL_AMBIENT_TEXT
```

**从调试对象提供 DML 内容**

Dbgeng 已增强，可以查看调试对象输出中的特殊标记 – –，该值指示在调试对象输出的一段的剩余文本应视为 DML。 模式更改仅适用于单个调试对象输出，如单个 OutputDebugString 字符串，且不是全局模式开关。

此示例演示纯和 DML 输出的组合。

```text
OutputDebugString(“This is plain text\n<?dml?>This is <col fg=\”emphfg\”>DML</col> text\n”);
```

输出生成，将具有一个行跟的 DML 首字母缩略词 DML 以不同的颜色的显示位置的行的纯文本。

**IDebugOutputCallbacks2**

IDebugOutputCallbacks2 允许 dbgeng 接口客户端接收完整的演示文稿的 DML 内容。 IDebugOutputCallbacks2 是 IDebugOutputCallbacks (不 IDebugOutputCallbacksWide) 的扩展，以便它可以对现有 SetOutputCallbacks 方法传入。 该引擎将执行 IDebugOutputCallbacks2 若要查看的接口传入的输出回调对象支持的 QueryInterface。 如果对象支持所有的输出将发送通过扩展 IDebugOutputCallbacks2 方法; IDebugOutputCallbacks2将不使用基本 idebugoutputcallbacks:: Output 方法。

新的方法是：

-   IDebugOutputCallbacks2::GetInterestMask – 允许回调对象来描述想要接收哪些类型的输出的通知。 基本的选择是纯文本内容之间 (调试\_OUTCBI\_文本) 和 DML 内容 (调试\_OUTCBI\_DML)。 此外，回调对象还可以请求通知的显式刷新 (调试\_OUTCBI\_EXPLICIT\_刷新)。
-   通过 Output2 IDebugOutputCallbacks2::Output2 – 所有 IDebugOutputCallbacks2 通知的都显示。 参数指示哪种通知即将推出的功能标志时，Arg 和文本参数具有的通知负载。 通知包括：

    -   调试\_OUTCB\_文本 – 纯文本输出。 标志是从调试\_OUTCBF\_\*，Arg 是输出掩码文本为纯文本。 这将仅收到如果调试\_OUTCBI\_相关掩码中所提供的文本。

    -   调试\_OUTCB\_DML – DML 内容输出。 标志是从调试\_OUTCBF\_\*，Arg 是输出掩码文本是 DML 内容。 这将仅收到如果调试\_OUTCBI\_DML 相关掩码中所提供。
    
    -   调试\_OUTCB\_EXPLICIT\_刷新-调用方已 FlushCallbacks 使用调用无缓冲的文本。 通常情况下在刷新缓冲的文本时调试\_OUTCBF\_组合\_EXPLICIT\_将设置刷新标志，折叠成一个的两个通知。 如果没有文本进行缓冲处理仅刷新通知将发送。

 Dbgeng.h 中定义了感兴趣的掩码标志，如下所示。

 ```cpp
 // IDebugOutputCallbacks2 interest mask flags.
 //
 // Indicates that the callback wants notifications
// of all explicit flushes.
#define DEBUG_OUTCBI_EXPLICIT_FLUSH 0x00000001
// Indicates that the callback wants
// content in text form.
#define DEBUG_OUTCBI_TEXT           0x00000002
// Indicates that the callback wants
// content in markup form.
#define DEBUG_OUTCBI_DML            0x00000004

#define DEBUG_OUTCBI_ANY_FORMAT     0x00000006
 ```

请注意是否它可以处理这两个输出对象可以注册为文本和 DML 内容。 输出处理引擎将选择的回调过程可以减少转换，因此同时支持的格式可能会降低转换引擎中。 但是，没有必要，并且支持仅一种格式是操作的预期的模式。

**自动转换**

Dbgeng 自动将纯文本和 DML 之间根据需要转换。 例如，如果调用方将发送 DML 内容到引擎引擎会将其转换为纯文本的所有输出客户端仅接受纯文本。 或者，该引擎将所有输出回调仅接受 DML，将纯文本都转换为 DML。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[使用调试器标记语言](debugger-markup-language-commands.md)










