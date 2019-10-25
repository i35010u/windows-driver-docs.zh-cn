---
title: JavaScript 约束
description: V4 打印机驱动程序模型支持从 v3 IPrintOemPrintTicketProvider 接口派生的扩展约束和 PrintTicket 处理。
ms.assetid: CD2EF726-CF0F-4BB6-9F41-794699568F17
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 31309f923c0afba29791feb3f632b4761614921f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845368"
---
# <a name="javascript-constraints"></a>JavaScript 约束


V4 打印机驱动程序模型支持从 v3 [IPrintOemPrintTicketProvider](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nn-prcomoem-iprintoemprintticketprovider)接口派生的扩展约束和 PrintTicket 处理的新模型。

V4 打印机驱动程序不使用已编译的配置插件，而是使用 JavaScript 来实现称为 JavaScript 约束的 Api，并且打印机驱动程序可以根据需要实现其中的一个或多个 Api。 有关详细信息，请参阅本主题末尾的**JavaScript 约束 api**部分中的函数。

JavaScript 约束可用于增加 PrintCapabilities，验证 Printticket 并处理 PrintTicket 到 DEVMODE 的转换，反之亦然。 但是，JavaScript 约束有一些限制。 下面列出了主要限制：

-   使用 CompletePrintCapabilities 添加的功能和选项以及在 validatePrintTicket 中指定的约束不会显示在 "桌面打印机首选项" 窗口中。

-   使用 CompletePrintCapabilities 中添加的功能和选项不会保留在公共 DEVMODE 中。

-   JavaScript 约束无法从资源 dll 访问语言资源来本地化添加的功能和选项或参数。

因此，建议仅在适当的位置使用 JavaScript 约束。 如果可能，应在 GPD 或 PPD 文件中指定功能和选项，并且仅在 JavaScript 中表示复杂的约束。

## <a name="debugging-javascript-files"></a>调试 JavaScript 文件


通过在基于 Windows 的脚本主机中打开 JavaScript 文件，支持对 JavaScript 文件进行基本语法验证。 为此，请右键单击 JavaScript 文件，然后选择 "**打开方式**"，然后在列表中选择 "基于 Windows 的脚本主机" 条目。 如果未引发任何错误，则 JavaScript 在语法上有效。 否则，它将指出问题的行号，如以下屏幕截图所示。

![javascript 语法错误对话框](images/script-host-err.png)

公开发布的 JavaScript 验证工具也可能在评估 JavaScript 文件样式时助手。

可以通过创建以下注册表项来启用交互式调试：

**项名称：** HKEY\_本地\_计算机\\系统\\CurrentControlSet\\控件\\打印

**值名称：** EnableJavaScriptDebugging

**键入：** DWORD

**值：** 1

但是，因为*PrintConfig*是频繁加载和卸载的，所以调试打印的应用程序并不是建议的测试/调试策略。 相反，Microsoft 建议制造商构建一个测试应用程序，该应用程序使用以下公共 Api 为 JavaScript 约束调用每个相关入口点： [PTGetPrintCapabilities](https://docs.microsoft.com/windows/desktop/api/prntvpt/nf-prntvpt-ptgetprintcapabilities)、 [PTConvertDevModeToPrintTicket](https://docs.microsoft.com/windows/desktop/api/prntvpt/nf-prntvpt-ptconvertdevmodetoprintticket)、 [PTConvertPrintTicketToDevMode](https://docs.microsoft.com/windows/desktop/api/prntvpt/nf-prntvpt-ptconvertprinttickettodevmode)和[PTMergeAndValidatePrintTicket](https://docs.microsoft.com/windows/desktop/api/prntvpt/nf-prntvpt-ptmergeandvalidateprintticket)。

仅测试应用程序足以启用调试，但添加单元测试也有好处，以确保整个驱动程序按预期处理 PrintTicket、PrintCapabilities 和约束。 有关如何在 Visual Studio 中生成单元测试的详细信息，请参阅以下主题：

[使用 Visual Studio Team Test 单元测试演练](https://docs.microsoft.com/previous-versions/ms379625(v=vs.80))

[Microsoft Visual Studio 2010 和 Team Foundation Server 的单元测试](https://channel9.msdn.com/Events/TechEd/Australia/2010/DEV362)

在创建上述文本中显示的注册表项并重新启动宿主进程后，可以调试 JavaScript 源文件。

需要注意的是，如果源文件分析失败，则不会调用调试器，它看起来就像调试环境失败。 如果源文件未能解析，请参阅[Windows 脚本宿主](https://docs.microsoft.com/previous-versions/9bbdkx3k(v=vs.85))，了解有关如何继续操作的详细信息。

如果没有错误并且已成功分析源文件，请按如下所示调试源文件：

1. 在测试计算机上安装 Microsoft Visual Studio 2012 或更高版本

2. 使用具有约束 JavaScript 代码的驱动程序创建打印队列

3. 将此打印队列设置为默认值。

4. 启动测试应用程序或打印并开始将导致 JavaScript 约束被调用的方案的应用程序。 应用必须调入 PrintTicket/PrintCapabilities Api 才能中断 JavaScript 约束;旧版应用程序（如记事本）不会调入这些 Api，而 XPS 查看器应用程序也会这样做。 Microsoft 建议在此处使用测试应用，因为方案可以更轻松地进行隔离和重现。

5. 此时，会弹出 "Visual Studio 实时调试器"，指出 "&lt;应用中发生了未经处理的异常&gt;"

6. 启动 Visual Studio 2012 或更高版本的新实例

7. 依次选择 "调试"、"附加到进程"

8. 在 "附加到进程" 对话框中，确保 "附加到：" 设置为 "脚本代码"

9. 现在，选择测试应用或应用打印，最后选择 "附加"

10. 单击 "全部中断"

11. 现在，返回到 "Visual Studio 实时调试器" 对话框，然后单击 "否"

12. Visual Studio 将在当前测试调用的位置中断调试器。 你现在可以正常调试代码。

## <a name="javascript-constraint-apis"></a>JavaScript 约束 Api


此部分指定充当在 JavaScript 约束文件中使用的 API 入口点的函数。 这些函数包括：

-   ValidatePrintTicket
-   completePrintCapabilities
-   convertDevModeToPrintTicket
-   ConvertPrintTicketToDevMode

## <a name="validateprintticket-function"></a>validatePrintTicket 函数


调用此 API 是为了验证 PrintTicket 对象对于特定打印机是否有效。 在函数中，这类似于[**IPrintOemPrintTicketProvider：： ValidatePrintTicket**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff553184(v=vs.85)) API。

语法

```javascript
function validatePrintTicket(printTicket, scriptContext)
```

参数

*printTicket*

\]中的 \[\[\] 要验证的[**IPrintSchemaTicket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprintschematicket)对象。
*scriptContext*

\[在\] 提供对驱动程序属性包、队列属性包和用户属性包的访问的[**IPrinterScriptContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprinterscriptcontext)对象中。
返回值

| 返回值 | 描述                                                                                                                                                                                                |
|--------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 0            | 指示*printTicket*参数无效，无法更正。 等效于[E\_PRINTTICKET\_格式](https://docs.microsoft.com/windows/desktop/api/prntvpt/nf-prntvpt-ptmergeandvalidateprintticket)。 |
| 1            | 指示*printTicket*参数是此打印机的有效 printticket。 等效于[S\_PT\_不\_冲突](https://docs.microsoft.com/windows/desktop/api/prntvpt/nf-prntvpt-ptmergeandvalidateprintticket)。   |
| 2            | 指示已修改*printTicket*参数，使其有效。 与[\_PT\_冲突\_解决](https://docs.microsoft.com/windows/desktop/api/prntvpt/nf-prntvpt-ptmergeandvalidateprintticket)。       |

 

## <a name="completeprintcapabilities-function"></a>completePrintCapabilities 函数


调用此 API 以允许修改 PrintCapabilities 对象。 这应该用于条件性功能（例如，仅在相纸上支持无边距），或表示无法由 GPD 或 PPD 文件（如嵌套功能定义）生成的功能。 在函数中，这类似于[**IPrintOemPrintTicketProvider：： CompletePrintCapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemprintticketprovider-completeprintcapabilities) API。

语法

```javascript
function completePrintCapabilities(printTicket, scriptContext, printCapabilities)
```

参数

*printTicket*

\[\] [**IPrintSchemaTicket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprintschematicket)对象输入，以将生成的 PrintCapabilities 文档约束到。
*scriptContext*

\[在\] 提供对驱动程序属性包、队列属性包和用户属性包的访问的[**IPrinterScriptContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprinterscriptcontext)对象中。
*printCapabilities*

\]中的 \[\[\] [**IPrintSchemaCapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprintschemacapabilities)对象，该对象表示配置模块生成的基本 PrintCapabilities 对象。
返回值

无。

## <a name="convertdevmodetoprintticket-function"></a>convertDevModeToPrintTicket 函数


调用此 API 可将值从 DEVMODE 属性包转换为 PrintTicket。 这类似于[**IPrintOemPrintTicketProvider：： ConvertDevModeToPrintTicket**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff553161(v=vs.85)) API 的功能，只不过此实现会将 DEVMODE 的 private 部分封装到[**IPrinterScriptablePropertyBag**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprinterscriptablepropertybag)对象中，并允许不访问 DEVMODE 的公共部分。

语法

```javascript
function convertDevModeToPrintTicket(devModeProperties, scriptContext, printTicket)
```

参数

*devModeProperties*

\[中\] 表示 DEVMODE 属性包的**IPrinterScriptablePropertyBag**对象。
*scriptContext*

\[在\] 提供对驱动程序属性包、队列属性包和用户属性包的访问的[**IPrinterScriptContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprinterscriptcontext)对象中。
*printTicket*

\]中的 \[\[\] 表示 PrintTicket 的[**IPrintSchemaTicket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprintschematicket)对象。
返回值

无。

## <a name="convertprinttickettodevmode-function"></a>convertPrintTicketToDevMode 函数


调用此 API 可将值从 PrintTicket 转换为 DEVMODE 属性包。 这类似于[**IPrintOemPrintTicketProvider：： ConvertPrintTicketToDevMode**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemprintticketprovider-convertprinttickettodevmode) API 的功能，只不过此实现会将 DEVMODE 的 private 部分封装到**IPrinterScriptablePropertyBag**对象中，并允许不访问 DEVMODE 的公共部分。

语法

```javascript
function convertPrintTicketToDevMode(printTicket, scriptContext, devModeProperties)
```

参数

*printTicket*

\[\] 表示要转换的 PrintTicket 的**IPrintSchemaTicket**对象。
*scriptContext*

\[在\] 提供对驱动程序属性包、队列属性包和用户属性包的访问的**IPrinterScriptContext**对象中。
*devModeProperties*

\]中的 \[\[\] 表示 DEVMODE 属性包的**IPrinterScriptablePropertyBag**对象。
返回值

无。

## <a name="constraint-best-practices"></a>约束最佳实践


Windows 8 打印对话框和打印首选项体验仅支持打印架构关键字命名空间的子集。 因此，Microsoft 不建议在 Windows 8 "打印" 对话框或 "打印首选项" UI 和不在该 UI 中的功能之间使用受支持的功能，因为用户没有机会解析此类约束。

例如，如果将名为 Photo 的 PageMediaType 选项限制为仅使用1200dpi 的 PageResolution 值，则用户将永远无法选择照片媒体类型。 在这种情况下，最好匹配用户的意图（照片介质），并调整进行此项设置所需的任何设置。 可以在 JavaScript 约束代码中进行这些调整。

如果驱动程序没有使用 JavaScript 约束，则不需要提供文件。 如果驱动程序只对入口点（例如，validatePrintTicket）的子集使用 JavaScript 约束，则应该从 JavaScript 文件中完全省略其他入口点。

有关如何使用 JavaScript 约束的详细信息，请参阅[打印驱动程序约束示例](https://go.microsoft.com/fwlink/p/?LinkId=617946)。

 

 




