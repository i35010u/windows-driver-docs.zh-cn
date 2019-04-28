---
title: JavaScript 约束
description: V4 打印机驱动程序模型支持扩展的约束，PrintTicket 处理派生自 v3 IPrintOemPrintTicketProvider 接口。
ms.assetid: CD2EF726-CF0F-4BB6-9F41-794699568F17
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 178c92b13970c1636671e7b85273ea1ee48dc152
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330143"
---
# <a name="javascript-constraints"></a>JavaScript 约束


V4 打印机驱动程序模型支持新模型，用于扩展约束和 PrintTicket 处理功能，它派生自 v3 [IPrintOemPrintTicketProvider](https://msdn.microsoft.com/library/windows/hardware/ff553174)接口。

而不是但是使用已编译的配置插件，v4 打印机驱动程序使用 JavaScript 来实现 Api 调用 JavaScript 约束和打印机驱动程序可以实现一个或多个所需对它们。 有关详细信息，请参阅中的函数**JavaScript 约束 Api**本主题末尾部分。

可以使用 JavaScript 约束来补充 PrintCapabilities、 验证 Printticket 和处理转换的 PrintTicket 到 DEVMODE，反之亦然。 但是，JavaScript 约束具有一些限制。 下面是主要的限制的列表：

-   桌面打印机首选项窗口中不显示功能和使用 CompletePrintCapabilities，添加的选项，以及 validatePrintTicket 中指定的约束。

-   功能和选项中使用 CompletePrintCapabilities 添加不会保留到公共 DEVMODE。

-   JavaScript 约束无法访问要本地化添加的功能和选项或参数的资源 dll 中的语言资源。

在这种情况下，我们建议只有在适合使用 JavaScript 约束。 应在其中在 JavaScript 中表示，且唯一的复杂的约束 GPD 或 PPD 文件中指定功能和选项。

## <a name="debugging-javascript-files"></a>调试 JavaScript 文件


通过在基于 Windows 脚本宿主中打开 JavaScript 文件支持的 JavaScript 文件的基本语法验证。 若要执行此操作，右键单击 JavaScript 文件，并选择**打开**，并选择 Windows 基于列表中的脚本主机条目。 如果不引发了任何错误，JavaScript 是语法上有效。 否则，它将指出问题的行号，如以下屏幕截图中所示。

![javascript 语法错误对话框](images/script-host-err.png)

公开提供的 JavaScript 验证工具也可能是为评估 JavaScript 文件的样式的助手有价值。

可以通过创建以下注册表项启用交互式调试：

**项名称：** HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\Print

**值名称：** EnableJavaScriptDebugging

**类型：** DWORD

**值：** 1

但是，由于*PrintConfig.dll*加载和卸载通常情况下，调试的应用程序将打印不是建议的测试/调试策略。 相反，Microsoft 建议制造商生成一个测试应用，使用这些公共 Api 的 JavaScript 约束调用的每个相关入口点：[PTGetPrintCapabilities](https://msdn.microsoft.com/library/windows/desktop/dd162881.aspx)， [PTConvertDevModeToPrintTicket](https://msdn.microsoft.com/library/windows/desktop/dd162879.aspx)， [PTConvertPrintTicketToDevMode](https://msdn.microsoft.com/library/windows/desktop/dd162880.aspx)，并且[PTMergeAndValidatePrintTicket](https://msdn.microsoft.com/library/windows/desktop/dd162884.aspx)。

测试应用程序只是不足以启用调试，但也有益添加单元测试以确保 PrintTicket 和 PrintCapabilities 约束按预期方式处理整个驱动程序。 有关如何构建 Visual Studio 中的单元测试的详细信息，请参阅以下主题：

[创建单元测试使用 Visual Studio Team Test 的演练](https://msdn.microsoft.com/library/ms379625.aspx)

[使用 Microsoft Visual Studio 2010 和 Team Foundation Server 进行单元测试](http://channel9.msdn.com/Events/TechEd/Australia/2010/DEV362)

创建上述文本中所示的注册表项，并重新启动托管进程后，您可以调试 JavaScript 源文件。

请务必注意，如果源文件无法分析，则不调用调试器，它将看起来像调试环境失败。 如果无法解析源文件，请参阅[Windows Script Host](https://msdn.microsoft.com/library/9bbdkx3k.aspx)详细了解如何继续。

如果没有任何错误，并且成功分析您的源文件，调试您的源文件，如下所示：

1. 安装 Microsoft Visual Studio 2012 或更高版本上测试计算机

2. 创建使用具有约束的 JavaScript 代码的驱动程序的打印队列

3. 将此打印队列设置为默认值。

4. 开始测试应用程序或打印并开始将导致 JavaScript 约束要调用的方案的应用。 应用程序必须调用的 PrintTicket/PrintCapabilities Api 以便分解成 JavaScript 约束;诸如记事本这样的旧版应用程序不调用这些 api，但 XPS 查看器应用。 Microsoft 建议使用测试应用程序在这里，由于的方案可以更轻松地隔离和重现。

5. 此时，"Visual Studio 实时调试器"会弹出说:"中发生未经处理的异常&lt;您的应用程序&gt;"

6. 启动 Visual Studio 2012 或更高版本的新实例

7. 选择调试，然后附加到进程

8. 在附加到进程对话框，请确保该附加到： 设置为脚本代码

9. 现在选择测试应用程序或应用程序打印，最后选择附加

10. 单击"全部中断"

11. 现在请返回到"Visual Studio 实时调试器"对话框，然后单击"否"

12. Visual Studio 将中断到调试器中调用的当前测试的位置。 您现在可能通常情况下调试代码。

## <a name="javascript-constraint-apis"></a>JavaScript 约束 Api


本部分中指定用作 JavaScript 约束文件中使用的 API 入口点的函数。 这些是函数：

-   validatePrintTicket
-   completePrintCapabilities
-   convertDevModeToPrintTicket
-   convertPrintTicketToDevMode

## <a name="validateprintticket-function"></a>validatePrintTicket 函数


若要验证 PrintTicket 对象是对特定打印机有效调用此 API。 这是在功能上与类似[ **IPrintOemPrintTicketProvider::ValidatePrintTicket** ](https://msdn.microsoft.com/library/windows/hardware/ff553184) API。

语法

```javascript
function validatePrintTicket(printTicket, scriptContext)
```

Parameters

*printTicket*

\[在中\]\[出\] [ **IPrintSchemaTicket** ](https://msdn.microsoft.com/library/windows/hardware/hh451398)对象进行验证。
*scriptContext*

\[在中\] [ **IPrinterScriptContext** ](https://msdn.microsoft.com/library/windows/hardware/hh768279)对象，它提供访问驱动程序属性包、 队列属性包和用户属性包。
返回值

| 返回值 | 描述                                                                                                                                                                                                |
|--------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 0            | 指示*printTicket*参数无效，并且不会得到更正。 等效于[E\_PRINTTICKET\_格式](https://msdn.microsoft.com/library/windows/desktop/dd162884.aspx)。 |
| 1            | 指示*printTicket*参数是有效 PrintTicket 此打印机。 等效于[S\_PT\_否\_冲突](https://msdn.microsoft.com/library/windows/desktop/dd162884.aspx)。   |
| 2            | 指示*printTicket*参数已修改以使其生效。 等效于[S\_PT\_冲突\_已解决](https://msdn.microsoft.com/library/windows/desktop/dd162884.aspx)。       |

 

## <a name="completeprintcapabilities-function"></a>completePrintCapabilities 函数


此 API 调用以允许要修改的 PrintCapabilities 对象。 这应该用于条件性功能 （例如，无边距仅支持照片纸） 或表示无法否则生成 GPD 或 PPD 文件 （例如，嵌套的功能定义） 的功能。 这是在功能上与类似[ **IPrintOemPrintTicketProvider::CompletePrintCapabilities** ](https://msdn.microsoft.com/library/windows/hardware/ff553158) API。

语法

```javascript
function completePrintCapabilities(printTicket, scriptContext, printCapabilities)
```

Parameters

*printTicket*

\[在中\] [ **IPrintSchemaTicket** ](https://msdn.microsoft.com/library/windows/hardware/hh451398)对象输入要约束到生成的 PrintCapabilities 文档。
*scriptContext*

\[在中\] [ **IPrinterScriptContext** ](https://msdn.microsoft.com/library/windows/hardware/hh768279)对象，它提供访问驱动程序属性包、 队列属性包和用户属性包。
*printCapabilities*

\[在中\]\[出\] [ **IPrintSchemaCapabilities** ](https://msdn.microsoft.com/library/windows/hardware/hh451256)对象，表示由配置模块生成的基 PrintCapabilities 对象。
返回值

无。

## <a name="convertdevmodetoprintticket-function"></a>convertDevModeToPrintTicket 函数


调用此 API 将从 DEVMODE 属性包的值转换为 PrintTicket。 这是在功能上与类似[ **IPrintOemPrintTicketProvider::ConvertDevModeToPrintTicket** ](https://msdn.microsoft.com/library/windows/hardware/ff553161) API，不同之处在于此实现封装到 DEVMODE 的专用部分[ **IPrinterScriptablePropertyBag** ](https://msdn.microsoft.com/library/windows/hardware/hh973217)对象，并允许 DEVMODE 的公共部分不能访问。

语法

```javascript
function convertDevModeToPrintTicket(devModeProperties, scriptContext, printTicket)
```

Parameters

*devModeProperties*

\[在中\] **IPrinterScriptablePropertyBag**对象，表示 DEVMODE 属性包。
*scriptContext*

\[在中\] [ **IPrinterScriptContext** ](https://msdn.microsoft.com/library/windows/hardware/hh768279)对象，它提供访问驱动程序属性包、 队列属性包和用户属性包。
*printTicket*

\[在中\]\[出\] [ **IPrintSchemaTicket** ](https://msdn.microsoft.com/library/windows/hardware/hh451398)表示 PrintTicket 对象。
返回值

无。

## <a name="convertprinttickettodevmode-function"></a>convertPrintTicketToDevMode 函数


调用此 API 将 PrintTicket 值转换入 DEVMODE 属性包。 这是在功能上与类似[ **IPrintOemPrintTicketProvider::ConvertPrintTicketToDevMode** ](https://msdn.microsoft.com/library/windows/hardware/ff553167) API，不同之处在于此实现封装到 DEVMODE 的专用部分**IPrinterScriptablePropertyBag**对象，并允许 DEVMODE 的公共部分不能访问。

语法

```javascript
function convertPrintTicketToDevMode(printTicket, scriptContext, devModeProperties)
```

Parameters

*printTicket*

\[在中\] **IPrintSchemaTicket**表示 PrintTicket 要转换的对象。
*scriptContext*

\[在中\] **IPrinterScriptContext**对象，它提供访问驱动程序属性包、 队列属性包和用户属性包。
*devModeProperties*

\[在中\]\[出\] **IPrinterScriptablePropertyBag**对象，表示 DEVMODE 属性包。
返回值

无。

## <a name="constraint-best-practices"></a>约束的最佳做法


Windows 8 打印对话框和打印首选项体验支持打印架构关键字命名空间的一个子集。 因此，Microsoft 不建议使用支持 Windows 8 打印对话框中或打印首选项用户界面的功能和由于用户会不有任何机会，若要解决此类约束，因此不在该 UI 中的功能之间的约束。

例如，如果名为 Photo 的 PageMediaType 选项被约束为仅适用于 1200 dpi PageResolution 值，然后用户永远不会将能够选择照片媒体类型。 在这种情况下，它是更好地匹配用户的意图 （照片媒体），并调整使这种情况所需的任何设置。 约束的 JavaScript 代码中就可以进行下述调整。

如果驱动程序不使用 JavaScript 约束，则将提供一个文件没有要求。 如果驱动程序中使用 JavaScript 约束的入口点 (例如，validatePrintTicket) 的一个子集，其他入口点应完全省略从 JavaScript 文件。

有关如何使用 JavaScript 约束的详细信息，请参阅[打印驱动程序约束示例](https://go.microsoft.com/fwlink/p/?LinkId=617946)。

 

 




