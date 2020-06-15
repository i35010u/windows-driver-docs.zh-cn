---
title: 打印机扩展
description: 当用户在 Windows 桌面上运行现有应用程序时，打印机扩展应用程序支持打印首选项和打印机通知。
ms.assetid: D617A897-D93E-4006-B42D-923CA7F29D7E
ms.date: 06/12/2020
ms.localizationpriority: medium
ms.openlocfilehash: 085be2e74d01a8fb43375832e249a438276dc9a7
ms.sourcegitcommit: 8a3cb2a87ce9751059bca8145a55b8cc39c34de9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/13/2020
ms.locfileid: "84756173"
---
# <a name="printer-extensions"></a>打印机扩展

当用户在 Windows 桌面上运行现有应用程序时，打印机扩展应用程序支持打印首选项和打印机通知。

## <a name="introduction"></a>介绍

打印机扩展可以采用任何支持 COM 的语言构建，但会经过优化，可使用 Microsoft .NET Framework 4 构建。 打印机扩展可以与打印驱动程序包一起分发，如果它们具有 XCopy 功能且不依赖于操作系统附带的外部运行时，如 .NET。 如果打印机扩展应用程序不满足这些条件，则可以将其分发到 setup.exe 或 MSI 包中，并通过使用 v4 清单中指定的 PrinterExtensionUrl 指令在打印机的设备阶段体验中公布。 当使用 MSI 包分发打印机扩展应用程序时，可以选择将打印驱动程序添加到包，或者将其保留并单独分发驱动程序。 PrinterExtensionUrl 显示在打印机首选项的体验上。

IT 管理员有几个选项可用于管理打印机扩展的分发。 如果将应用程序打包到 setup.exe 或 MSI 中，则 IT 管理员可以使用标准的软件分发工具（如 Microsoft 终结点 Configuration Manager），也可以将应用程序包括在其标准操作系统映像中。 IT 管理员还可以覆盖 v4 清单中指定的 PrinterExtensionUrl （如果它们编辑 HKEY \_ 本地 \_ 计算机 \\ 软件 \\ Microsoft \\ Windows NT \\ CurrentVersion \\ 打印 \\ \\ &lt; 队列名称 &gt; \\ PrinterDriverData PrinterExtensionUrl） \\ 。

如果企业选择完全阻止打印机扩展，则可以通过名为 "计算机配置 \\ 管理模板 \\ 打印机 \\ 不允许 v4 打印机驱动程序显示打印机扩展应用程序" 的组策略来完成此操作。

## <a name="building-a-printer-extension"></a>生成打印机扩展

GitHub 上的[打印机扩展示例](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/printer-extension-sample/)演示如何使用 c # 生成打印机扩展。 为了允许在 UWP 设备应用和打印机扩展之间共享代码，此示例使用两个项目： PrinterExtensionLibrary （a C）和 ExtensionSample （依赖于 PrinterExtensionLibrary 的打印机扩展）。

本主题中所示的代码片段都取自 PrinterExtensionSample 解决方案。 如果要使用 C、c + + 或其他基于 COM 的语言生成打印机扩展，这些概念是类似的，但 Api 必须与在 Windows 驱动程序工具包中包含的*PrinterExtension*中指定的相同。 示例文档 PrinterExtensionLibrary 中的代码注释还包括指示特定对象所对应的基础 COM 接口的代码注释。

开发打印机扩展时，有六个主要方面需要注意。 以下列表显示了这些重点区域。

- 注册

- 启用事件

- OnDriverEvent 处理程序

- 打印首选项

- 打印机通知

- 管理打印机

### <a name="registration"></a>注册

通过指定一组注册表项，或者在 v4 清单文件的 PrinterExtensions 节中指定应用程序信息，将打印机扩展注册到打印系统。

有指定的 Guid 支持打印机扩展的每个不同入口点。 不需要在 v4 清单文件中使用这些 Guid，但必须知道 GUID 值才能使用适用于 v4 驱动程序安装的注册表格式。 下表显示了这两个入口点的 GUID 值。

| 入口点           | GUID                                   |
|-----------------------|----------------------------------------|
| 打印首选项     | {EC8F261F-267C-469F-B5D6-3933023C29CC} |
| 打印机通知 | {23BB1328-63DE-4293-915B-A6A23D929ACB} |

安装在打印机驱动程序之外的打印机扩展需要使用注册表进行注册。 这可以确保安装打印机扩展，而不考虑后台处理程序的状态，或者客户端计算机上的 v4 配置模块。

PrintNotify 服务启动后，它将检查 OfflineRoot 路径下的注册表项 \[ \] ，并处理任何挂起的注册或 unregistrations。 完成任何挂起的注册或 unregistrations 后，将会实时删除注册表项。 请注意，如果使用脚本或迭代过程来放置注册表项，则 \\ \[ \] 每次指定 \\ \[ PrinterDriverId \] 键时，可能需要重新创建 PrinterExtensionID 密钥。 不能删除不完整或格式不正确的键。

仅在首次安装时才需要进行此注册。 以下示例显示了用于注册打印机扩展的正确注册表项格式。

> [!NOTE]
> ** \[ OFFLINEROOT \] **用作 HKEY \_ 本地 \_ 计算机 \\ 软件 \\ Microsoft \\ Windows NT \\ CurrentVersion \\ Print \\ OfflinePrinterExtensions 的简写形式。

```Registry
[OfflineRoot]
    \[PrinterExtensionId] {GUID}
           AppPath=[PrinterExtensionAppPath] {String}
           \[PrinterDriverId] {GUID}
                  \[PrinterExtensionReasonGuid]
(default) = ["0"|"1"] {REG_SZ 0:Unregister, 1:Register}
                  \…
                  \[PrinterExtensionReasonGuidN]
           \[PrinterDriverId2]
                  \[PrinterExtensionReasonGuid2.1]
                  \…
                  \[PrinterExtensionReasonGuid2.Z]
           …
           \[PrinterDriverIdM]
    \[PrinterExtensionId2]
    …
    \[PrinterExtensionIdT]
```

例如，下面的一组密钥将向 {*PrinterExtensionIDGuid*} PrinterExtensionID 注册打印机扩展，并使用 \\ \\ \\ 打印机首选项和打印机通知原因为 {*PrinterDriverID1Guid*} 和 {*PrinterDriverID2Guid*} PrinterDriverIDs 注册 "C： Program Files Fabrikampe.exe" 可执行文件的完全限定路径。

```Registry
[OfflineRoot]
    \{PrinterExtensionIDGuid}
           AppPath="C:\Program Files\Fabrikam\pe.exe"
           \{PrinterDriverID1Guid}
                 \{EC8F261F-267C-469F-B5D6-3933023C29CC}
            (default) = "1"
                 \{23BB1328-63DE-4293-915B-A6A23D929ACB}
            (default) = "1"
           \{PrinterDriverID1Guid}
                 \{EC8F261F-267C-469F-B5D6-3933023C29CC}
            (default) = "1"
                 \{23BB1328-63DE-4293-915B-A6A23D929ACB}
            (default) = "1"
```

若要卸载同一打印机扩展，应指定以下密钥集。

```Registry
[OfflineRoot]
    \{PrinterExtensionIDGuid}
           AppPath="C:\Program Files\Fabrikam\pe.exe"
           \{PrinterDriverID1Guid}
                 \{EC8F261F-267C-469F-B5D6-3933023C29CC}
            (default) = "0"
                 \{23BB1328-63DE-4293-915B-A6A23D929ACB}
            (default) = "0"
           \{PrinterDriverID1Guid}
                 \{EC8F261F-267C-469F-B5D6-3933023C29CC}
            (default) = "0"
                 \{23BB1328-63DE-4293-915B-A6A23D929ACB}
            (default) = "0"
```

由于打印机扩展可以同时在用户启动的上下文和事件启动的上下文中运行，因此，能够确定打印机扩展运行的上下文非常有用。 例如，如果为通知或打印首选项启动了某个应用程序，则该应用程序可允许应用程序在所有队列中枚举状态。 Microsoft 建议从驱动程序中单独安装的打印机扩展（例如，使用 MSI 或 setup.exe）应在 "开始" 菜单快捷方式中使用命令行开关，或使用注册期间在注册表中填充的应用项中的命令行开关。 由于随驱动程序一起安装的打印机扩展已安装到 DriverStore，因此不会在打印首选项或打印机通知事件之外启动这些扩展。 因此，在这种情况下不支持指定命令行开关。

当打印机扩展插件为当前 PrinterDriverID 注册时，它必须包含应用中的 PrinterDriverID。 例如，对于名称为*printerextension.exe*的打印机扩展应用程序，PrinterDriverID 值为 *{GUID}*，PrinterExtensionAppPath 将如下所 \[ \] 示：

```console
"C:\program files\fabrikam\printerextension.exe {GUID}"
```

### <a name="enabling-events"></a>启用事件

在运行时，打印机扩展必须启用当前 PrinterDriverID 的事件触发。 这是通过 args 数组传递给应用的 PrinterDriverID \[ \] ，它允许打印系统提供适当的事件上下文，用于处理打印首选项或打印机通知等原因。

因此，应用程序应该为当前 PrinterDriverID 创建新的 PrinterExtensionManager，注册一个委托来处理 OnDriverEvent 事件，并使用 PrinterDriverID 调用 EnableEvents 方法。 下面的代码段演示了此方法。

```csharp
PrinterExtensionManager mgr = new PrinterExtensionManager();
mgr.OnDriverEvent += OnDriverEvent;
mgr.EnableEvents(new Guid(PrinterDriverID1));
```

如果应用在5秒内未调用 EnableEvents，则 Windows 将超时并启动标准 UI。 为了缓解这种情况，打印机扩展应遵循最新的性能最佳实践，包括以下各项：

- 在调用 EnableEvents 之后，尽可能延迟应用初始化。 此后，使用异步方法确定 UI 响应能力的优先级，而不会在初始化期间阻止 UI 线程。

- 在安装过程中使用 ngen 生成本机映像。 有关详细信息，请参阅[本机映像生成器](https://docs.microsoft.com/dotnet/framework/tools/ngen-exe-native-image-generator)。

- 使用性能度量工具来查找加载时的性能问题。 有关详细信息，请参阅[Windows 性能分析工具](https://docs.microsoft.com/windows-hardware/test/wpt/)。

### <a name="driverevent-handler"></a>DriverEvent 处理程序

注册 OnDriverEvent 处理程序并启用事件之后，如果启动了打印机扩展来处理打印首选项或打印机通知，则将调用处理程序。 在上面的代码段中，将名为 OnDriverEvent 的方法注册为事件处理程序。 在以下代码片段中， *PrinterExtensionEventArgs*参数是可用于构造打印首选项和打印机通知方案的对象。 *PrinterExtensionEventArgs*是[**IPrinterExtensionEventArgs**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprinterextensioneventargs)的包装器。

```csharp
static void OnDriverEvent(object sender, PrinterExtensionEventArgs eventArgs)
{
    //
    // Display the print preferences window.
    //

    if (eventArgs.ReasonId.Equals(PrinterExtensionReason.PrintPreferences))
    {
        PrintPreferenceWindow printPreferenceWindow = new PrintPreferenceWindow();
        printPreferenceWindow.Initialize(eventArgs);

        //
        // Set the caller application's window as parent/owner of the newly created printing preferences window.
        //

        WindowInteropHelper wih = new WindowInteropHelper(printPreferenceWindow);
        wih.Owner = eventArgs.WindowParent;

        //
        // Display a modal/non-modal window based on the 'WindowModal' parameter.
        //

        if (eventArgs.WindowModal)
        {
            printPreferenceWindow.ShowDialog();
        }
        else
        {
            printPreferenceWindow.Show();
        }
    }

    //
    // Handle driver events.
    //

    else if (eventArgs.ReasonId.Equals(PrinterExtensionReason.DriverEvent))
    {
        // Handle driver events here.
    }
}
```

若要防止错误的用户体验与崩溃或慢速打印机扩展相关联，如果在启动应用后的短时间内未调用 EnableEvents，Windows 将实现超时。 若要启用调试，如果有一个调试器附加到 PrintNotify 服务，则将禁用此超时。

然而，在大多数情况下，我们感兴趣的所有与应用相关的代码都在 OnDriverEvent 回调期间或之后运行。 在开发过程中，在从 OnDriverEvent 回调开始打印首选项或打印机通知体验之前，显示 MessageBox 可能也很有用。 显示 MessageBox 后，返回 Visual Studio，单击 "**调试**" " &gt; **附加到进程**"，然后选择进程的名称。 最后，返回到 MessageBox，并单击 "确定" 继续。 这将确保你看到异常，并从该点开始命中任何断点。

将来可能会支持新 ReasonIds。 因此，打印机扩展必须显式检查 ReasonID，并且不能使用 "else" 语句来检测上一个已知的 ReasonID。 如果收到并未知的 ReasonID，应用应正常退出。

### <a name="print-preferences"></a>打印首选项

打印首选项由 PrintSchemaEventArgs 对象驱动。 此对象封装用于描述设备功能和选项的 PrintTicket 和 PrintCapabilities 文档。 虽然基础 XML 也可用，但对象模型可以更轻松地使用这些格式。

在每个[**IPrintSchemaTicket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprintschematicket)或[**IPrintSchemaCapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprintschemacapabilities)对象中都有功能（[**IPrintSchemaFeature**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprintschemafeature)）和选项（[**IPrintSchemaOption**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprintschemaoption)）。 尽管用于功能和选项的接口是相同的，但不管来源如何，该行为会因基础 XML 而略有不同。 例如，PrintCapabilities documents 指定了多个功能的选项，而 PrintTicket 文档仅指定了选择的（或默认的）选项。 同样，PrintCapabilities 文档指定本地化的显示字符串，而 PrintTicket 文档则不指定。

[打印机扩展示例](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/printer-extension-sample/)使用数据绑定为打印机首选项创建 ComboBox 控件。 Microsoft 建议使用数据绑定，因为这样可以减少分散功能，从而使代码更易于维护。 有关 WPF 中数据绑定的详细信息，请参阅[数据绑定概述](https://docs.microsoft.com/dotnet/framework/wpf/data/data-binding-overview)。

为了最大限度地提高性能，Microsoft 建议仅在需要更新 PrintCapabilities 文档时才应执行对 GetPrintCapabilities 的调用。

用户使用 "数据绑定" 组合框控件进行选择时，PrintTicket 对象会自动更新。 当用户最后单击 **"确定"** 时，将开始一系列异步验证和完成。 此异步模式广泛用于阻止 UI 线程上出现长时间运行的任务，并导致打印首选项 UI 或正在打印的应用程序挂起。 下面是在用户单击 **"确定"** 后用于处理 PrintTicket 更改的步骤列表。

1. PrintSchemaTicket 是使用[**IPrintSchemaTicket：： ValidateAsync**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nf-printerextension-iprintschematicket-validateasync)方法验证的 asynchrously。

1. 异步验证完成后，公共语言运行时（CLR）将调用 PrintTicketValidateCompleted 方法。

    1. 如果验证成功，则它将调用 CommitPrintTicketAsync 方法，CommitPrintTicketAsync 调用[**IPrintSchemaTicket：： CommitAsync**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nf-printerextension-iprintschematicket-commitasync)方法。 成功完成更新 PrintTicket 后，将调用 PrintTicketCommitCompleted 方法，该方法调用一种便捷方法，该方法调用 PrinterExtensionEventArgs 方法来指示打印首选项已完成，然后关闭应用程序。

    1. 否则，它向用户提供用于处理约束情形的 UI。

如果用户单击 "取消" 或直接关闭 "打印首选项" 窗口，则打印机扩展会使用相应的 HRESULT 值和错误日志的消息调用 IPrinterExtensionEventArgs。

如果打印机扩展的进程已关闭，并且未按前面的段落中所述的方式调用 Complete 或 Cancel 方法，打印系统将自动回退到使用 Microsoft 提供的 UI。

为了检索设备状态信息，打印机扩展可以使用双向查询打印设备。 例如，若要显示墨迹状态或设备的其他类型状态，打印机扩展可以使用 IPrinterExtensionEventArgs. PrinterQueue. SendBidiQuery 方法向设备发出双向查询。 获取最新的双向状态的过程分为两个步骤：设置 OnBidiResponseReceived 事件的事件处理程序，并使用有效的双向查询调用 SendBidiQuery 方法。 以下代码片段显示了此两步过程。

```csharp
PrinterQueue.OnBidiResponseReceived += new
EventHandler<PrinterQueueEventArgs>(OnBidiResponseReceived);
PrinterQueue.SendBidiQuery("\\Printer.consumables");
```

收到双向响应时，将调用以下事件处理程序。 请注意，此事件处理程序还具有模拟的墨迹状态实现，这在设备不可用时可能很有用。 PrinterQueueEventArgs 对象包括 HRESULT 和双向 XML 响应。 有关双向 XML 响应的详细信息，请参阅[双向请求和响应架构](https://docs.microsoft.com/previous-versions/dd183368(v=vs.85))。

```csharp
private void OnBidiResponseReceived(object sender, PrinterQueueEventArgs e)
{
    if (e.StatusHResult != (int)HRESULT.S_OK)
    {
        MockInkStatus();
        return;
    }

    //
    // Display the ink levels from the data.
    //

    BidiHelperSource = new BidiHelper(e.Response);
    if (PropertyChanged != null)
    {
        PropertyChanged(this, new PropertyChangedEventArgs("BidiHelperSource"));
    }
    InkStatusTitle = "Ink status (Live data)";
}
```

### <a name="printer-notifications"></a>打印机通知

按与打印首选项相同的方式调用打印机通知。 在 OnDriverEvent 处理程序中，如果 IPrinterExtensionEventArgs 指示 ReasonID 与 DriverEvents GUID 相匹配，则可以生成处理此事件的体验。

[打印机扩展示例](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/printer-extension-sample/)项目并不演示功能打印机通知体验，但以下变量对于处理此情况最有用。

- PrinterExtensionEventArgs. BidiNotification –这会携带导致事件触发的双向 XML。

- PrinterExtensionEventArgs. DetailedReasonId –其中包含驱动程序事件 xml 文件中的 eventID GUID。

用于通知的 IPrinterExtensionEventArgs 对象的最重要的属性是 BidiNotification 属性。 这会携带导致触发事件的双向 XML。 有关双向 XML 响应的详细信息，请参阅[双向请求和响应架构](https://docs.microsoft.com/previous-versions/dd183368(v=vs.85))。

### <a name="managing-printers"></a>管理打印机

为了支持将打印机扩展作为应用程序（可用作管理/维护打印机的集线器）的角色，可以枚举当前打印机扩展已注册到的打印队列，并获得每个队列的状态。 这不在 PrinterExtensionSample 项目中演示，但以下代码片段可以添加到 App.xaml.cs 的 Main 方法中，以注册事件处理程序。

```csharp
mgr.OnPrinterQueuesEnumerated += new EventHandler<PrinterQueuesEnumeratedEventArgs>(mgr_OnPrinterQueuesEnumerated);
```

枚举队列后，将调用事件处理程序，并且可能会发生状态操作。 在应用程序的生存期内会定期引发此事件，以确保枚举的打印队列的列表是最新的，即使用户自打开后已安装了多个队列也是如此。 因此，在每次执行事件处理程序时，事件处理程序不会创建新窗口，这一点很重要，如下代码片段所示。

```csharp
static void mgr_OnPrinterQueuesEnumerated(object sender, PrinterQueuesEnumeratedEventArgs e)
{
    foreach (IPrinterExtensionContext pContext in e)
    {
        // show status
    }
}
```

为了使用打印机扩展执行维护任务，Microsoft 建议使用以下伪代码中所述的旧版 WritePrinter API。

```Pseudocode
OpenPrinter
    StartDocPrinter
        StartPagePrinter
          WritePrinter
        EndPagePrinter
    EndDocPrinter
ClosePrinter
```

若要详细了解如何将这些旧版 Api 封送到 .NET，请参阅[如何使用 Visual c # .net 将原始数据发送到打印机](https://support.microsoft.com/help/322091)，或者[如何使用 Visual Basic .net 将原始数据发送到打印机](https://support.microsoft.com/help/322090)。

## <a name="printer-extension-performance-best-practices"></a>打印机扩展性能最佳做法

为了确保获得最佳的用户体验，应尽可能快地加载打印机扩展。 打印机扩展示例项目是 .NET 应用程序，这意味着它内置于中间语言（IL）中，在运行时必须将其编译为本机处理器体系结构的相应格式。 在安装过程中，Microsoft 建议根据最佳做法安装打印机扩展，以确保应用已针对本机系统体系结构进行了编译。 有关代码编译和安装最佳实践的详细信息，请参阅[提高桌面应用程序的启动性能](https://devblogs.microsoft.com/dotnet/improving-launch-performance-for-your-desktop-applications/)。

Microsoft 还建议在调用 EnableEvents 方法之前，打印机扩展会推迟初始化任务（例如加载资源）。 这会最大程度地减少应用程序调用 EnableEvents 的可能性，这是打印机扩展的5秒超时。

OnDriverEvent 调用后，打印机扩展应尽可能快地初始化其 UI，并尽快使用异步方法，以确保响应能力。 打印机扩展不应与网络调用或双向相关，因此无法为打印首选项或打印机通知创建初始窗口状态。

当用户在影响 PrintTicket 的屏幕 UI 上进行选择时，打印机扩展应使用 IPrintSchemaTicket：： ValidateAsync 方法来验证更改。 最后，打印机扩展应使用[**IPrintSchemaTicket：： CommitAsync**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nf-printerextension-iprintschematicket-commitasync)方法来提交 PrintTicket 更改。

打印机扩展始终从调用它们的进程中执行。 因此，在开发打印机扩展时，必须记住窗口行为：

- [**IPrinterExtensionEventArgs**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprinterextensioneventargs)的**WindowParent**属性指定调用应用的窗口的句柄。
- [**IPrinterExtensionEventArgs**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprinterextensioneventargs)的**WindowModal**属性指定是否应以模式方式运行打印机扩展（处于打印首选项模式）。

打印机扩展示例演示如何创建通常作为最顶层窗口启动的 UI。 但在某些情况下，将不会在前台显示 UI，例如当导致调用 UI 的进程在不同的完整性级别运行时，或在为不同的处理器体系结构编译该过程时。 在这种情况下，打印机扩展应调用 FlashWindowEx 来请求用户使用任务栏中的图标来进入前台。

## <a name="related-topics"></a>相关主题

[双向请求和响应架构](https://docs.microsoft.com/previous-versions/dd183368(v=vs.85))

[数据绑定概述](https://docs.microsoft.com/dotnet/framework/wpf/data/data-binding-overview)

[如何使用 Visual Basic .NET 将原始数据发送到打印机](https://support.microsoft.com/help/322090)

[如何使用 Visual c # .NET 将原始数据发送到打印机](https://support.microsoft.com/help/322091)

[提高桌面应用程序的启动性能](https://devblogs.microsoft.com/dotnet/improving-launch-performance-for-your-desktop-applications/)

[本机映像生成器](https://docs.microsoft.com/dotnet/framework/tools/ngen-exe-native-image-generator)

[打印架构接口](https://docs.microsoft.com/windows-hardware/drivers/ddi/_print/index)

[打印机扩展示例](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/printer-extension-sample/)

[Windows 性能分析工具](https://docs.microsoft.com/windows-hardware/test/wpt/)
