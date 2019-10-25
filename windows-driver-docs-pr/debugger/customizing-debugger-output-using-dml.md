---
title: 使用 DML 自定义调试器输出
description: 调试器标记语言（DML）提供了一种机制，用于增强调试器和扩展的输出。
ms.assetid: 04984510-B95F-405F-81DF-E9D0673210B4
ms.date: 11/13/2018
ms.localizationpriority: medium
ms.openlocfilehash: 2fb2477b1e331569a525f9052af6fa16353c5656
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837816"
---
# <a name="customizing-debugger-output-using-dml"></a>使用 DML 自定义调试器输出


调试器标记语言（DML）提供了一种机制，用于增强调试器和扩展的输出。 与 HTML 类似，调试器的标记支持允许输出以标记的形式包括显示指令和额外的非显示信息。 调试程序用户界面（如 WinDbg）分析 DML 中提供的额外信息，以增强信息的显示，并提供新的行为，例如网格显示和排序。 本主题介绍如何使用 DML 自定义调试输出。 有关在调试器中启用和使用 DML 的常规信息，请参阅[使用调试器标记语言](debugger-markup-language-commands.md)。

DML 适用于 Windows 10 及更高版本。

## <a name="span-iddml_overviewspanspan-iddml_overviewspanspan-iddml_overviewspandml-overview"></a><span id="DML_Overview"></span><span id="dml_overview"></span><span id="DML_OVERVIEW"></span>DML 概述


在 DML 的主要优点中，它提供链接到调试器输出中的相关信息的能力。 其中一项主要 DML 标记是 &lt;链接&gt; 标记，该标记允许输出生成方指示可通过链接的指定操作访问与输出片段相关的信息。 与 web 浏览器中的 HTML 链接一样，这允许用户导航超链接的信息。

提供超链接内容的一个优点是它可以用于增强调试器和调试器扩展功能的可发现性。 调试器及其扩展包含大量功能，但很难确定要在不同方案中使用的相应命令。 用户必须只知道哪些命令可用于特定方案。 用户和内核调试之间的差异增加了复杂性。 这通常意味着许多用户不了解可帮助它们的调试命令。 通过 DML 链接，可将任意调试命令包装在备用演示文稿中，如说明性文本、可单击的菜单系统或链接的帮助。 使用 DML，可以增强命令输出，指导用户使用与手头任务相关的其他相关命令。

**调试器 DML 支持**

-   WinDbg 中的命令窗口支持所有 DML 行为，并将显示颜色、字体样式和链接。
-   控制台调试– ntsd、cdb 和 kd –仅支持 DML 的颜色属性，并且仅在启用了颜色模式的真正控制台中运行时才支持。
-   具有重定向 i/o、ntsd – d 或远程 .exe 会话的调试器不会显示任何颜色。

## <a name="span-iddml_content_specificationspanspan-iddml_content_specificationspanspan-iddml_content_specificationspandml-content-specification"></a><span id="DML_Content_Specification"></span><span id="dml_content_specification"></span><span id="DML_CONTENT_SPECIFICATION"></span>DML 内容规范


DML 不应作为一种完整的演示语言（如 HTML）。 DML 特意非常简单，并且只有少量标记。

由于并非所有调试器工具都支持多格式文本，因此 DML 旨在允许在 DML 和纯文本之间进行简单转换。 这允许 DML 在所有现有调试器工具中正常工作。 可能很容易支持颜色等效果，因为删除它们不会删除携带实际信息的文本。

DML 不是 XML。 DML 不会尝试携带语义信息或结构化信息。 如上所述，DML 和纯文本之间必须有一个简单的映射，因此，DML 标记全部可放弃。

DML 不可扩展;所有标记都是预定义的并且经过验证，可以在所有现有的调试器工具上工作。

**标记结构**

与 XML 类似，DML 标记作为开始 &lt;tagname \[args\]&gt; 和以下 &lt;/tagname&gt;。

**特殊字符**

DML 内容大致遵循用于特殊字符的 XML/HTML 规则。 &、&lt;、&gt; 和 "字符是特殊字符，不能以纯文本格式使用。 等效的转义版本 &、&lt;、&gt; 和 "。 例如，以下文本：

"Alice & Bob 认为 3 &lt; 4"

将转换为以下 DML。

```text
"Alice & Bob think 3 &lt 4"
```

**C 编程语言格式字符**

从 XML/HTML 规则出发，DML 文本可以包含 C 编程语言流样式的格式设置字符，如 \\b、\\t \\r 和 \\n。 这是为了支持与现有调试器文本生产和使用的兼容性。

## <a name="span-idexample_dmlspanspan-idexample_dmlspanspan-idexample_dmlspanexample-dml"></a><span id="Example_DML"></span><span id="example_dml"></span><span id="EXAMPLE_DML"></span>示例 DML


假设文件 C：\\Dml\_试验包含以下行。

```text
My DML Experiment
<link cmd="lmD musb*">List modules that begin with usb.</link>
```

以下命令在命令浏览器窗口中显示文本和链接。

```dbgcmd
.browse .dml_start c:\Dml_Experiment.txt
```

![dml 文件输出的屏幕截图](images/dmlcommands03.png)

如果单击 "**列出以 usb 链接开头的模块**"，将看到类似于下图的输出。

![模块列表的屏幕截图](images/dmlcommands04.png)

## <a name="span-idright-click_behavior_in_dmlspanspan-idright-click_behavior_in_dmlspanspan-idright-click_behavior_in_dmlspanright-click-behavior-in-dml"></a><span id="Right-Click_Behavior_in_DML"></span><span id="right-click_behavior_in_dml"></span><span id="RIGHT-CLICK_BEHAVIOR_IN_DML"></span>在 DML 中右键单击行为


在 DML 中可使用右键单击行为。 此示例演示如何使用 &lt;altlink&gt; 来定义右键单击行为，以便通过定期单击发送断点[ **（"设置断点"）** ](bp--bu--bm--set-breakpoint-.md)命令并发送[**u （Unassemble）** ](u--unassemble-.md) 。

```text
<link cmd="u MyProgram!memcpy">
<altlink name="Set Breakpoint (bp)" cmd="bp MyProgram!memcpy" />
u MyProgram!memcpy
</link>
```

## <a name="span-iddml_tag_referencespanspan-iddml_tag_referencespanspan-iddml_tag_referencespandml-tag-reference"></a><span id="DML_Tag_Reference"></span><span id="dml_tag_reference"></span><span id="DML_TAG_REFERENCE"></span>DML 标记引用


### <a name="span-id_link_spanspan-id_link_spanltlinkgt"></a><span id="_link_"></span><span id="_LINK_"></span>&lt;链接&gt;

*&lt;链接 \[name = "text"\] \[cmd = "调试器\_command"\]\[alt = "悬停文本以显示"\] \[部分 = "name"\]&gt;/link&lt;链接文本&gt;*

Link 标记是 DML 中的基本超链接机制。 它指导支持 DML 表示形式的用户界面将链接文本显示为可单击的链接。 当单击具有 cmd 规范的链接时，将执行调试器命令，其输出应替换当前输出。

Name 和 section 参数允许在命名链接之间导航，类似于 HTML 的 &lt;名称&gt; 和 \#名称支持。 当在 UI 上单击具有 section 参数的链接时，将扫描名称与匹配的链接，并将其滚动到 "查看"。 这允许链接指向同一页面的不同部分（或新页面的特定部分）。 DML 的部分名称是单独的，以避免必须定义一个新语法，这会允许在命令字符串末尾使用节名称。

转换为纯文本会删除标记。

**示例**

```text
<b> Handy Links </b>
<link cmd="!dml_proc">Display process information with DML rendering.</link>
<link cmd="kM">Display stack information with DML rendering.</link>
```

**示例**

此示例演示如何使用 alt 特性来创建将光标悬停在 DML 链接上时显示的文本。

```text
<b>Hover Example</b>
<link cmd="lmD" alt="This link will run the list modules command and display the output in DML format">LmD</link>
```

### <a name="span-id_altlink_spanspan-id_altlink_spanltaltlinkgt"></a><span id="_altlink_"></span><span id="_ALTLINK_"></span>&lt;altlink&gt;

*&lt;altlink \[name = "text"\] \[cmd = "调试器\_command"\] \[节 = "name"\]&gt;alt link text&lt;/altlink&gt;*

&lt;altlink&gt; 标记提供右键单击行为，在 DML 中提供。 当单击具有 cmd 规范的链接时，将执行调试器命令，其输出应替换当前输出。 &lt;altlink&gt; 选项卡通常与 &lt;链接&gt; 标记配对，以支持常规单击和右击行为。

转换为纯文本会删除标记。

**示例**

此示例显示了如何使用 &lt;altlink&gt; 来定义右键单击行为，以便通过定期单击发送断点[ **（"设置断点"）** ](bp--bu--bm--set-breakpoint-.md)命令并发送[**u （Unassemble）** ](u--unassemble-.md) 。

```text
<link cmd="u MyProgram!memcpy">
<altlink name="Set Breakpoint (bp)" cmd="bp MyProgram!memcpy" />
u MyProgram!memcpy
</link>
```

### <a name="span-id_exec_spanspan-id_exec_spanltexecgt"></a><span id="_exec_"></span><span id="_EXEC_"></span>&lt;exec&gt;

*&lt;exec cmd = "调试器\_命令"&gt;描述性文本&lt;/exec&gt;*

Exec 标记类似于 link 标记，其中描述性文本应显示为可单击的项。 但是，当在命令浏览器窗口中使用 exec 标记时，将在不替换当前输出的情况下执行给定的命令，此标记提供了一种通过单击菜单中的命令来执行命令的方法。

转换为纯文本会删除标记。

**示例**

此示例演示如何使用定期单击定义两个命令。

```text
<b>Exec Sample</b>
<exec cmd="!dml_proc">Display process information with DML rendering.</exec>
<exec cmd="kM">Display stack information with DML rendering.</exec>
```

### <a name="span-id_b_spanspan-id_b_spanltbgt"></a><span id="_b_"></span><span id="_B_"></span>&lt;b&gt;

*&lt;b&gt;粗体文本&lt;/b&gt;*

此标记请求粗体。 &lt;b&gt;，&lt;我&gt;，&lt;u&gt; 可以嵌套起来，以混合使用属性。

转换为纯文本会删除标记。

**示例**

此示例演示如何粗体文本。

```text
<b>This is bold Text</b>
```

### <a name="span-id_i_spanspan-id_i_spanltigt"></a><span id="_i_"></span><span id="_I_"></span>&lt;我&gt;

*&lt;&gt;斜体文本&lt;/i&gt;*

此标记请求倾斜。 &lt;b&gt;，&lt;我&gt;，&lt;u&gt; 可以嵌套起来，以混合使用属性。

转换为纯文本会删除标记。

**示例**

此示例演示如何使文本倾斜。

```text
<i>This is italicized Text</i>
```

### <a name="span-id_u_spanspan-id_u_spanltugt"></a><span id="_u_"></span><span id="_U_"></span>&lt;u&gt;

*&lt;u&gt;带下划线的文本&lt;/u&gt;*

此标记请求带下划线的文本。 &lt;b&gt;，&lt;我&gt;，&lt;u&gt; 可以嵌套起来，以混合使用属性。

转换为纯文本会删除标记。

**示例**

此示例显示了如何给文本加下划线。

```text
<u>This is underlined Text</u>
```

**示例**

此示例演示如何将标记组合为粗体、下划线和斜体文本。

```text
<b><u><i>This is bold, underlined and italizized text. </i></u></b> 
```

### <a name="span-id_col_spanspan-id_col_spanltcolgt"></a><span id="_col_"></span><span id="_COL_"></span>&lt;列&gt;

&lt;col fg = "name" bg = "name"&gt;text&lt;/col&gt;

请求文本的前景色和背景色。 颜色被指定为已知颜色的名称而不是绝对值，因为这样可以让客户控制他们看到的颜色类型。 当前颜色名称（默认值仅适用于 WinDbg）。

**前台和后台元素标记**

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><strong>将</strong></td>
<td align="left"><strong>说明/示例</strong></td>
</tr>
<tr class="even">
<td align="left"><p>wbg-Windows 后台</p>
<p>wfg-Windows 前台</p></td>
<td align="left">默认窗口背景色和前景色。 默认为窗口和窗口文本的系统颜色。
<p>&lt;col fg = "wfg" bg = "wbg"&gt; 这是标准前景/背景文本 &lt;/col&gt;</p></td>
</tr>
<tr class="odd">
<td align="left"><p>clbg-当前行前景</p>
<p>clfg-当前行背景</p></td>
<td align="left">当前线条背景色和前景色。 默认为突出显示和突出显示文本的系统颜色。
<p>&lt;col fg = "clfg" bg = "clbg"&gt; 测试文本-当前行&lt;/col&gt;</p></td>
</tr>
<tr class="even">
<td align="left"><p>empbg-强调背景</p>
<p>emphfg-突出前景</p></td>
<td align="left">强调文本。 默认为浅蓝色。
<p>&lt;col fg = "empfg" bg = "empbg"&gt; 这是强调前景/背景文本 &lt;/col&gt;</p></td>
</tr>
<tr class="odd">
<td align="left"><p>subbg-温柔背景</p>
<p>subfg-温柔前台</p></td>
<td align="left">温柔文本。 默认为非活动标题文本和非活动标题的系统颜色。
<p>&lt;col fg = "subfg" bg = "subbg"&gt; 这是温柔前台/背景文本 &lt;/col&gt;</p></td>
</tr>
<tr class="even">
<td align="left"><p>normbg-正常背景</p>
<p>normfg-正常前景</p></td>
<td align="left">正常
<p>&lt;col fg = "normfg" bg = "normbg"&gt; 测试文本-Normal （normfg/normbg） &lt;/col&gt;</p></td>
</tr>
<tr class="odd">
<td align="left"><p>warnbg-警告背景</p>
<p>warnfg-Warning 前台</p></td>
<td align="left">警告
<p>&lt;col fg = "warnfg" bg = "warnbg"&gt; 测试文本-警告（warnfg/warnbg） &lt;/col&gt;</p></td>
</tr>
<tr class="even">
<td align="left"><p>errbg-错误背景</p>
<p>errfg-错误前景</p></td>
<td align="left">错误
<p>&lt;col fg = "errfg" bg = "errbg"&gt; 测试文本-错误（errfg/errbg） &lt;/col&gt;</p></td>
</tr>
<tr class="odd">
<td align="left"><p>verbbg-详细背景</p>
<p>verbfg-详细前景</p></td>
<td align="left">Verbose
<p>&lt;col fg = "verbfg" bg = "verbbg"&gt; 测试文本-Verbose （verbfg/verbbg） &lt;/col&gt;</p></td>
</tr>
</tbody>
</table>



**源代码单元素标记**

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>srcnum-源数值常量</p></td>
<td align="left">源元素颜色。
<p>&lt;col fg = "srcnum" bg = "wbg"&gt; 测试文本-srcnum &lt;/col&gt;</p></td>
</tr>
<tr class="even">
<td align="left"><p>srcchar-源字符常量</p></td>
<td align="left"><p>&lt;col fg = "srcchar" bg = "wbg"&gt; 测试文本-srcchar &lt;/col&gt;</p></td>
</tr>
<tr class="odd">
<td align="left"><p>srcstr-源字符串常量</p></td>
<td align="left"><p>&lt;col fg = "srcstr" bg = "wbg"&gt; 测试文本-srcstr &lt;/col&gt;</p></td>
</tr>
<tr class="even">
<td align="left"><p>srcid-源标识符</p></td>
<td align="left"><p>&lt;col fg = "srcid" bg = "wbg"&gt; 测试文本-srcid &lt;/col&gt;</p></td>
</tr>
<tr class="odd">
<td align="left"><p>srckw 关键字</p></td>
<td align="left"><p>&lt;col fg = "srckw" bg = "wbg"&gt; 测试文本-srckw &lt;/col&gt;</p></td>
</tr>
<tr class="even">
<td align="left"><p>srcpair-源大括号或匹配符号对</p></td>
<td align="left"><p>&lt;col fg = "srcpair" bg = "empbbg"&gt; 测试文本-srcpair &lt;/col&gt;</p></td>
</tr>
<tr class="odd">
<td align="left"><p>srccmnt-源注释</p></td>
<td align="left"><p>&lt;col fg = "srccmnt" bg = "wbg"&gt; 测试文本-srccmnt &lt;/col&gt;</p></td>
</tr>
<tr class="even">
<td align="left"><p>srcdrct-源指令</p></td>
<td align="left"><p>&lt;col fg = "srcdrct" bg = "wbg"&gt; 测试文本-srcdrct &lt;/col&gt;</p></td>
</tr>
<tr class="odd">
<td align="left"><p>srcspid-源特殊标识符</p></td>
<td align="left"><p>&lt;col fg = "srcspid" bg = "wbg"&gt; 测试文本-srcspid &lt;/col&gt;</p></td>
</tr>
<tr class="even">
<td align="left"><p>srcannot-源批注</p></td>
<td align="left"><p>&lt;col fg = "srcannot" bg = "wbg"&gt; 测试文本-srcannot &lt;/col&gt;</p></td>
</tr>
<tr class="odd">
<td align="left"><p>更改的数据</p></td>
<td align="left">用于自上一停止点以来发生更改的数据，例如，在 WinDbg 中更改寄存器。 默认值为红色。
<p>&lt;col fg = "changed" bg = "wbg"&gt; 测试文本-已更改&lt;/col&gt;</p></td>
</tr>
</tbody>
</table>



## <a name="span-iddml_example_codespanspan-iddml_example_codespanspan-iddml_example_codespandml-example-code"></a><span id="DML_Example_Code"></span><span id="dml_example_code"></span><span id="DML_EXAMPLE_CODE"></span>DML 示例代码


此代码示例演示了以下代码。

-   调用调试命令
-   实现右键单击命令
-   在文本上实现悬停
-   使用颜色和丰富文本

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

此代码示例演示如何使用颜色和格式标记。

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

## <a name="span-iddml_additions_to_the_dbgeng_interfacespanspan-iddml_additions_to_the_dbgeng_interfacespanspan-iddml_additions_to_the_dbgeng_interfacespandml-additions-to-the-dbgeng-interface"></a><span id="DML_Additions_to_the_dbgeng_Interface"></span><span id="dml_additions_to_the_dbgeng_interface"></span><span id="DML_ADDITIONS_TO_THE_DBGENG_INTERFACE"></span>对 dbgeng 接口的 DML 添加


[调试器引擎和扩展 api](debugger-engine-and-extension-apis.md)提供了一个接口，用来创建自定义应用程序。 你还可以编写将在 WinDbg、KD、CDB 和 NTSD 中运行的自定义扩展插件。 有关详细信息，请参阅[编写 DbgEng 扩展](writing-dbgeng-extensions.md)。 本节介绍调试器引擎接口的可用 DML 增强功能。

Dbgeng 已具有一组文本处理输入方法和输出接口，使用 DML 只需要指定输入和输出文本中携带的内容类型。

**向 dbgeng 提供 DML 内容**

Output 控件标记 DEBUG\_OUTCTL\_DML 表示 dbgeng 方法生成的文本应作为 DML 内容处理。 如果未指定此标志，则文本将被视为纯文本上下文。 调试\_OUTCTL\_DML 可以与以下方法一起使用。

-   [**IDebugControl4::ControlledOutput**](https://msdn.microsoft.com/library/windows/hardware/ff539248)
-   [**IDebugControl4::ControlledOutputVaList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-controlledoutputvalist)
-   [**IDebugControl4::ControlledOutputWide**](https://msdn.microsoft.com/library/windows/hardware/ff539266)
-   [**IDebugControl4::ControlledOutputVaListWide**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol4-controlledoutputvalistwide)

给定的文本必须遵循用于有效字符的 DML 规则。

所有输出例程均已增强，以允许新格式说明符%\[h | w\]Y {t}。 此格式说明符包含一个字符串指针作为参数，指示给定文本为纯文本，并应在输出处理期间转换为 DML 格式。 这为调用方提供了一种简单的方法，在 DML 内容中包含纯文本，而无需事先转换为 DML 格式。 H 和 w 限定符指示 ANSI 或 Unicode 文本，如% s。

下表总结了% Y 格式说明符的用法。

|        |                                                                                                                                                                                                                                    |
|--------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| % Y {t}  | 带引号的字符串。 如果输出格式（第一个 arg）为 DML，则将文本转换为 DML。                                                                                                                                                   |
| % Y {T}  | 带引号的字符串。 将始终将文本转换为 DML，而不考虑输出格式。                                                                                                                                                    |
| % Y {s}  | 未加引号的字符串。 如果输出格式（第一个 arg）为 DML，则将文本转换为 DML。                                                                                                                                                 |
| % Y {S}  | 未加引号的字符串。 将始终将文本转换为 DML，而不考虑输出格式。                                                                                                                                                  |
| % Y {as} | ULONG64. 添加一个空字符串或9个空格的间距，以填充调试器格式的指针字段的高32位部分。 额外的空间输出9个空格，其中包含前8个零加上 \` 字符。 |
| % Y {ps} | ULONG64. 填充调试器格式化指针字段的额外空间（包括前8个零加上 \` 字符）。                                                                                                             |
| % Y {l}  | ULONG64. 作为源行信息的地址。                                                                                                                                                                                       |



此代码段演示如何使用% Y 格式说明符。

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

此示例代码将生成以下输出。

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

额外的控制标志、DEBUG\_OUTCTL\_环境\_DML）允许指定 DML 上下文文本，而无需修改任何输出控制特性。 调试\_OUTCTL\_环境\_文本添加为以前存在的调试\_OUTCTL\_环境的更具描述性的别名。 在 dbgeng 中定义了输出控制标志。

```cpp
#define DEBUG_OUTCTL_DML               0x00000020

// Special values which mean leave the output settings
// unchanged.
#define DEBUG_OUTCTL_AMBIENT_DML       0xfffffffe
#define DEBUG_OUTCTL_AMBIENT_TEXT      0xffffffff

// Old ambient flag which maps to text.
#define DEBUG_OUTCTL_AMBIENT           DEBUG_OUTCTL_AMBIENT_TEXT
```

**从调试对象中提供 DML 内容**

已对 dbgeng 进行了增强，以便扫描特定标记的调试对象输出–表示调试对象输出中的剩余文本应视为 DML。 模式更改仅适用于单个调试对象输出片段（如单个 OutputDebugString 字符串），而不是全局模式开关。

此示例显示了混合输出的混合。

```text
OutputDebugString(“This is plain text\n<?dml?>This is <col fg=\”emphfg\”>DML</col> text\n”);
```

生成的输出将具有一行纯文本，后跟一个 DML 行，其中的缩写词以不同的颜色显示。

**IDebugOutputCallbacks2**

IDebugOutputCallbacks2 允许 dbgeng 接口客户端接收用于显示的完整 DML 内容。 IDebugOutputCallbacks2 是 IDebugOutputCallbacks 的扩展（而不是 IDebugOutputCallbacksWide），以便可以将其传递到现有的 SetOutputCallbacks 方法中。 该引擎将为 IDebugOutputCallbacks2 执行 QueryInterface，以查看传入输出回调对象支持的接口。 如果对象支持 IDebugOutputCallbacks2，则所有输出都将通过扩展的 IDebugOutputCallbacks2 方法发送;不会使用基本 IDebugOutputCallbacks：： Output 方法。

新的方法是：

-   IDebugOutputCallbacks2：： GetInterestMask –允许回调对象描述其要接收的输出通知的类型。 基本的选择是在纯文本内容（调试\_OUTCBI\_文本）和 DML 内容（调试\_OUTCBI\_DML）之间进行。 此外，回调对象还可以请求显式刷新（调试\_OUTCBI\_显式\_刷新）的通知。
-   IDebugOutputCallbacks2：：输出2–所有 IDebugOutputCallbacks2 通知都通过输出2。 一个参数，指示在 Flags、Arg 和 Text 参数携带通知有效负载时传入哪种类型的通知。 通知包括：

    -   调试\_OUTCB\_文本–纯文本输出。 标志来自 DEBUG\_OUTCBF\_\*，Arg 为输出掩码，文本为纯文本。 仅当在兴趣掩码中提供了 DEBUG\_OUTCBI\_文本时才会收到此内容。

    -   调试\_OUTCB\_DML – DML 内容输出。 标志来自调试\_OUTCBF\_\*，Arg 是输出掩码，文本是 DML 内容。 仅当在兴趣掩码中提供了 DEBUG\_OUTCBI\_DML 时才会收到此项。
    
    -   调试\_OUTCB\_显式\_刷新–调用方调用了 FlushCallbacks，但未缓冲文本。 通常情况下，在刷新缓冲的文本时，将设置 "调试\_OUTCBF"\_组合\_显式\_刷新标志，将两个通知折叠为一个。 如果未缓冲任何文本，则发送仅限刷新通知。

 相关掩码标志在 dbgeng 中定义，如下所示。

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

请注意，输出对象可以同时对文本和 DML 内容进行处理。 在回调的输出处理过程中，引擎将选取减小转换的格式，因此支持两者都可以减少引擎中的转换。 但这并不是必需的，仅支持一种格式，这是预期的操作模式。

**自动转换**

根据需要，dbgeng 将在纯文本和 DML 之间自动转换。 例如，如果调用方将 DML 内容发送到引擎，则引擎会将其转换为纯文本，以供仅接受纯文本的所有输出客户端使用。 另外，引擎会将纯文本转换为仅接受 DML 的所有输出回调。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[使用调试器标记语言](debugger-markup-language-commands.md)










