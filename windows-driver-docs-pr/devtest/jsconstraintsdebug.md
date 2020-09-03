---
title: JSConstraintsDebug
description: 'JSConstraintsDebug ( # A0) 是一个命令行工具，用于在开发 V4 打印机驱动程序时为 JavaScript 约束提供调试支持。'
ms.assetid: 48C39A2C-7EA6-4BAA-B5E8-3B426C9697B3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f3101d71ddc1c65fd1eee12aee714c40ed097e81
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89383925"
---
# <a name="jsconstraintsdebug"></a>JSConstraintsDebug


JSConstraintsDebug ( # A0) 是一个命令行工具，用于在开发[V4 打印机驱动程序](../print/v4-printer-driver.md)时为[JavaScript 约束](../print/javascript-constraints.md)提供调试支持。

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">在哪里可以下载 JSConstraintsDebug？</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>JSConstraintsDebug.exe 包含在 Microsoft Windows 驱动程序工具包 (WDK) 中。 有关获取 WDK 的信息，请参阅 <a href="https://docs.microsoft.com/windows-hardware/drivers/download-the-wdk" data-raw-source="[Windows Driver Kit downloads](../download-the-wdk.md)">Windows 驱动程序工具包下载</a>。</p></td>
</tr>
</tbody>
</table>

 

该工具在目标驱动程序的 JavaScript 约束上针对用户提供的打印票证执行以下每个相关入口点 Api：

[**PTGetPrintCapabilities**](/windows/desktop/api/prntvpt/nf-prntvpt-ptgetprintcapabilities)

[**PTConvertDevModeToPrintTicket**](/windows/desktop/api/prntvpt/nf-prntvpt-ptconvertdevmodetoprintticket)

[**TConvertPrintTicketToDevMode**](/windows/desktop/api/prntvpt/nf-prntvpt-ptconvertprinttickettodevmode)

[**PTMergeAndValidatePrintTicket**](/windows/desktop/api/prntvpt/nf-prntvpt-ptmergeandvalidateprintticket)

在执行期间，该工具会提示输入合适的 IDE 调试器，如 Visual Studio。 选择后，约束源代码将在 JavaScript 调试器语句中打开和停止。

若要调试 JS 约束文件，请执行以下步骤：

1.  打开命令提示符窗口。

2.  运行 JSConstraintsDebug.exe 工具，并至少指定打印机名称和测试打印票证的路径。

3.  选择要使用的调试工具。

## <a name="span-idrunning_jsconstraintsdebug_in_user_modespanspan-idrunning_jsconstraintsdebug_in_user_modespanspan-idrunning_jsconstraintsdebug_in_user_modespanrunning-jsconstraintsdebug-in-user-mode"></a><span id="Running_JSConstraintsDebug_in_user_mode"></span><span id="running_jsconstraintsdebug_in_user_mode"></span><span id="RUNNING_JSCONSTRAINTSDEBUG_IN_USER_MODE"></span>在用户模式下运行 JSConstraintsDebug


启用 JS 函数调试需要提升的权限。 若要在用户模式下运行，必须先设置以下注册表项，然后再执行 JSConstraintsDebug.exe：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>项名称</p></td>
<td align="left"><p>HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Control\Print</p></td>
</tr>
<tr class="even">
<td align="left"><p>值名称</p></td>
<td align="left"><p>EnableJavaScriptDebugging</p></td>
</tr>
<tr class="odd">
<td align="left"><p>类型</p></td>
<td align="left"><p>DWORD</p></td>
</tr>
<tr class="even">
<td align="left"><p>值</p></td>
<td align="left"><p>1</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idjavascript_debugger_statementsspanspan-idjavascript_debugger_statementsspanspan-idjavascript_debugger_statementsspanjavascript-debugger-statements"></a><span id="JavaScript_debugger_statements"></span><span id="javascript_debugger_statements"></span><span id="JAVASCRIPT_DEBUGGER_STATEMENTS"></span>JavaScript 调试器语句


可以使用调试器语句在 JavaScript 源中创建断点。 这会在 Visual Studio 中暂停操作，并允许逐步调试。 可以在任何 [JavaScript 约束 api](../print/javascript-constraints.md)中插入这些语句。

例如：

```JavaScript
function validatePrintTicket(PrintTicket, scriptContext)
{
    debugger; // debug tool will pause at this breakpoint
    ...
}
```

## <a name="span-idjsconstraintsdebug_command_syntaxspanspan-idjsconstraintsdebug_command_syntaxspanspan-idjsconstraintsdebug_command_syntaxspanjsconstraintsdebug-command-syntax"></a><span id="JSConstraintsDebug_Command_Syntax"></span><span id="jsconstraintsdebug_command_syntax"></span><span id="JSCONSTRAINTSDEBUG_COMMAND_SYNTAX"></span>JSConstraintsDebug 命令语法


```
JSConstraintsDebug <PrinterName> <PrintTicket> [MergePrintTicket] [Constraints]
```

## <a name="span-idcommand_parametersspanspan-idcommand_parametersspanspan-idcommand_parametersspancommand-parameters"></a><span id="Command_parameters"></span><span id="command_parameters"></span><span id="COMMAND_PARAMETERS"></span>命令参数


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span id="PrinterName"></span><span id="printername"></span><span id="PRINTERNAME"></span>PrinterName</p></td>
<td align="left"><p>必需。 指定包含 JS 约束源文件的打印驱动程序的字符串名称。 此驱动程序将用于所有调试操作。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="PrintTicket"></span><span id="printticket"></span><span id="PRINTTICKET"></span>PrintTicket</p></td>
<td align="left"><p>必需。 指定要验证的打印票证 XML 文件的路径和名称。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="MergePrintTicket"></span><span id="mergeprintticket"></span><span id="MERGEPRINTTICKET"></span>MergePrintTicket</p></td>
<td align="left"><p>可选。 指定将用于验证合并操作的打印票证 XML 文件的路径和名称。</p>
<p>如果未设置此参数，则会将默认 DevMode 转换为打印票证，并将其传递到合并和验证 API。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Constraints"></span><span id="constraints"></span><span id="CONSTRAINTS"></span>约束</p></td>
<td align="left"><p>可选。 指定 JavaScript 约束文件的路径和名称，该文件将替换在调试之前在目标打印机驱动程序中找到的现有约束源文件。</p></td>
</tr>
</tbody>
</table>

 

**注意**   使用约束参数指定约束文件将覆盖目标驱动程序中的现有源代码。

 

## <a name="span-idexamplesspanspan-idexamplesspanspan-idexamplesspanexamples"></a><span id="Examples"></span><span id="examples"></span><span id="EXAMPLES"></span>示例


针对已知测试打印票证调试打印驱动程序。

```
JSConstraintsDebug “Contoso Printer” PrintTicket.xml
```

使用新的约束源文件针对已知测试打印票证调试打印驱动程序。

```
JSConstraintsDebug “Contoso Printer” PrintTicket.xml Constraints.js
```

测试合并并验证两个自定义打印票证之间的操作。

```
JSConstraintsDebug “Contoso Printer” PrintTicket.xml PrintTicket2.xml
```

 

