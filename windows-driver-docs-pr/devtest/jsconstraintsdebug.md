---
title: JSConstraintsDebug
description: JSConstraintsDebug (JSConstraintsDebug.exe) 是一个命令行工具，开发 V4 打印机驱动程序时提供的 JavaScript 约束的调试支持。
ms.assetid: 48C39A2C-7EA6-4BAA-B5E8-3B426C9697B3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0fe2a51979dd2ab3a69eeb553582b1b1a24bd6b5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373657"
---
# <a name="jsconstraintsdebug"></a>JSConstraintsDebug


JSConstraintsDebug (JSConstraintsDebug.exe) 是一个命令行工具，提供了有关调试支持[JavaScript 约束](https://docs.microsoft.com/windows-hardware/drivers/print/javascript-constraints)开发时[V4 打印机驱动程序](https://docs.microsoft.com/windows-hardware/drivers/print/v4-printer-driver)。

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">在何处可以下载 JSConstraintsDebug？</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>JSConstraintsDebug.exe 包含 Microsoft Windows Driver Kit (WDK) 中。 有关获取 WDK 的信息，请参阅<a href="https://go.microsoft.com/fwlink/p/?LinkId=808351" data-raw-source="[Windows Driver Kit downloads](https://go.microsoft.com/fwlink/p/?LinkId=808351)">Windows 驱动程序工具包下载</a>。</p></td>
</tr>
</tbody>
</table>

 

该工具执行以下相关入口点 Api 的每个用户提供的打印票证针对目标的驱动程序的 JavaScript 约束上：

[**PTGetPrintCapabilities**](https://docs.microsoft.com/windows/desktop/api/prntvpt/nf-prntvpt-ptgetprintcapabilities)

[**PTConvertDevModeToPrintTicket**](https://docs.microsoft.com/windows/desktop/api/prntvpt/nf-prntvpt-ptconvertdevmodetoprintticket)

[**TConvertPrintTicketToDevMode**](https://docs.microsoft.com/windows/desktop/api/prntvpt/nf-prntvpt-ptconvertprinttickettodevmode)

[**PTMergeAndValidatePrintTicket**](https://docs.microsoft.com/windows/desktop/api/prntvpt/nf-prntvpt-ptmergeandvalidateprintticket)

在执行期间该工具将提示输入适当的 IDE 调试程序，如 Visual Studio。 选择它后将打开并在 JavaScript 调试器语句处停止约束源代码。

若要调试 JS 约束文件，请按照下列步骤：

1.  打开“命令提示符”窗口。

2.  运行 JSConstraintsDebug.exe 工具和指定，在最小值、 打印机名称和路径向测试打印票证。

3.  选择你想要使用的调试工具。

## <a name="span-idrunningjsconstraintsdebuginusermodespanspan-idrunningjsconstraintsdebuginusermodespanspan-idrunningjsconstraintsdebuginusermodespanrunning-jsconstraintsdebug-in-user-mode"></a><span id="Running_JSConstraintsDebug_in_user_mode"></span><span id="running_jsconstraintsdebug_in_user_mode"></span><span id="RUNNING_JSCONSTRAINTSDEBUG_IN_USER_MODE"></span>在用户模式下运行 JSConstraintsDebug


启用调试的 JS 函数需要提升的权限。 若要在用户模式下运行，必须在执行 JSConstraintsDebug.exe 之前设置以下注册表项：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>项名称</p></td>
<td align="left"><p>HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Print</p></td>
</tr>
<tr class="even">
<td align="left"><p>值名称</p></td>
<td align="left"><p>EnableJavaScriptDebugging</p></td>
</tr>
<tr class="odd">
<td align="left"><p>在任务栏的搜索框中键入</p></td>
<td align="left"><p>DWORD</p></td>
</tr>
<tr class="even">
<td align="left"><p>值</p></td>
<td align="left"><p>1</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idjavascriptdebuggerstatementsspanspan-idjavascriptdebuggerstatementsspanspan-idjavascriptdebuggerstatementsspanjavascript-debugger-statements"></a><span id="JavaScript_debugger_statements"></span><span id="javascript_debugger_statements"></span><span id="JAVASCRIPT_DEBUGGER_STATEMENTS"></span>JavaScript 调试器语句


通过使用调试程序语句，可以在 JavaScript 源中创建断点。 这将暂停所有允许分步调试的 Visual Studio 中的操作。 这些语句可插入中的任何[JavaScript 约束 Api](https://go.microsoft.com/fwlink/p/?LinkId=808350)。

例如：

```JavaScript
function validatePrintTicket(PrintTicket, scriptContext)
{
    debugger; // debug tool will pause at this breakpoint
    ...
}
```

## <a name="span-idjsconstraintsdebugcommandsyntaxspanspan-idjsconstraintsdebugcommandsyntaxspanspan-idjsconstraintsdebugcommandsyntaxspanjsconstraintsdebug-command-syntax"></a><span id="JSConstraintsDebug_Command_Syntax"></span><span id="jsconstraintsdebug_command_syntax"></span><span id="JSCONSTRAINTSDEBUG_COMMAND_SYNTAX"></span>JSConstraintsDebug 命令语法


```
JSConstraintsDebug <PrinterName> <PrintTicket> [MergePrintTicket] [Constraints]
```

## <a name="span-idcommandparametersspanspan-idcommandparametersspanspan-idcommandparametersspancommand-parameters"></a><span id="Command_parameters"></span><span id="command_parameters"></span><span id="COMMAND_PARAMETERS"></span>命令参数


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Parameters</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span id="PrinterName"></span><span id="printername"></span><span id="PRINTERNAME"></span>PrinterName</p></td>
<td align="left"><p>必需。 指定其中包含 JS 约束源文件的打印驱动程序的字符串名称。 此驱动程序将用于调试的所有操作。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="PrintTicket"></span><span id="printticket"></span><span id="PRINTTICKET"></span>PrintTicket</p></td>
<td align="left"><p>必需。 指定的路径和要验证的打印票证 XML 文件的名称。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="MergePrintTicket"></span><span id="mergeprintticket"></span><span id="MERGEPRINTTICKET"></span>MergePrintTicket</p></td>
<td align="left"><p>可选。 指定的路径和名称将用于验证合并操作的打印票证 XML 文件。</p>
<p>如果此参数未设置默认值 DevMode 将转换为打印票证，并将传递为合并转换和验证 API。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Constraints"></span><span id="constraints"></span><span id="CONSTRAINTS"></span>约束</p></td>
<td align="left"><p>可选。 指定的路径和名称的 JavaScript 约束文件将替换现有约束源文件调试之前找到目标的打印机驱动程序中的条件。</p></td>
</tr>
</tbody>
</table>

 

**请注意**  约束参数与指定约束文件将覆盖现有目标驱动程序中的源代码。

 

## <a name="span-idexamplesspanspan-idexamplesspanspan-idexamplesspanexamples"></a><span id="Examples"></span><span id="examples"></span><span id="EXAMPLES"></span>示例


调试打印驱动程序针对已知的测试打印票证。

```
JSConstraintsDebug “Contoso Printer” PrintTicket.xml
```

与已知的测试打印票证针对新约束源文件调试打印驱动程序。

```
JSConstraintsDebug “Contoso Printer” PrintTicket.xml Constraints.js
```

测试合并和验证两个自定义的打印票证之间的操作。

```
JSConstraintsDebug “Contoso Printer” PrintTicket.xml PrintTicket2.xml
```

 

 





