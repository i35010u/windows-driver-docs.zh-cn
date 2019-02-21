---
title: 打印机扩展
description: 当用户在 Windows 桌面上运行现有应用程序时，打印机扩展应用程序支持打印首选项和打印机通知。
ms.assetid: D617A897-D93E-4006-B42D-923CA7F29D7E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6ac419a9f97ecb648733dd3244c41e632ff722b2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541452"
---
# <a name="printer-extensions"></a>打印机扩展

当用户在 Windows 桌面上运行现有应用程序时，打印机扩展应用程序支持打印首选项和打印机通知。

## <a name="introduction"></a>简介

打印机扩展可以构建采用任何支持 COM 的语言，但进行了优化以使用 Microsoft.NET Framework 4 构建。 打印机扩展可能会随打印驱动程序包，分发，如果它们 XCopy 能够和不附带了操作系统，例如，.NET 等外部运行时没有任何依赖关系。 如果打印机扩展应用程序不符合这些条件，它是分布式 setup.exe 或 MSI 包中，打印机的 Device Stage 体验所播发的使用 v4 清单中指定的 PrinterExtensionUrl 指令。 将打印机扩展应用程序通过 MSI 程序包分发，必须将打印驱动程序添加到包或省略它并将驱动程序分发单独的选项。 PrinterExtensionUrl 显示打印机首选项体验上。

IT 管理员有几个选项用于管理打印机扩展的分发。 如果应用程序打包在 setup.exe 或 MSI，然后 IT 管理员可以使用标准软件分发工具如 System Center Configuration Manager (SCCM)，或它们可以在其标准 OS 映像中包括应用程序。 IT 管理员还可以重写 v4 清单中指定 PrinterExtensionUrl 如果他们编辑 HKEY\_本地\_MACHINE\\软件\\Microsoft\\Windows NT\\CurrentVersion\\打印\\打印机\\&lt;打印队列名称&gt;\\PrinterDriverData\\PrinterExtensionUrl。

如果企业选择完全阻止打印机扩展，这可以通过名为的组策略和"计算机配置\\管理模板\\打印机\\不允许 v4 打印机驱动程序以显示打印机扩展应用程序"。

## <a name="building-a-printer-extension"></a>构建打印机扩展

[扩展插件示例的打印机](https://go.microsoft.com/fwlink/p/?LinkId=617945)在 GitHub 上演示了如何生成打印机扩展使用C#。 为了使 UWP 设备应用程序和打印机扩展之间共享代码，本示例使用两个项目：PrinterExtensionLibrary (C) 和 ExtensionSample （取决于 PrinterExtensionLibrary 打印机扩展）。

本主题中所示的代码片段全部摘自 PrinterExtensionSample 解决方案。 如果要生成 C、 c + + 或其他基于 COM 的语言中的打印机扩展插件，概念是类似但中指定的而是必须匹配 Api *PrinterExtension.IDL*，包含在 Windows 驱动程序工具包。 从示例文档 PrinterExtensionLibrary 中的代码注释还包括指示对应于特定对象的基础 COM 接口的代码注释。

开发打印机扩展时, 有个，您必须知道的六个主要区域。 以下列表中显示这些关注领域。

- 注册

- 启用事件

- OnDriverEvent Handler

- 打印首选项

- 打印机通知

- 管理打印机

### <a name="registration"></a>注册

通过指定一组注册表项或通过 PrinterExtensions 一部分 v4 清单文件中指定的应用程序信息，打印机扩展打印系统注册。

没有指定打印机扩展支持的每个不同入口点的 Guid。 无需在 v4 清单文件中，使用这些 Guid，但你必须知道要使用的 v4 驱动程序安装的注册表格式的 GUID 值。 下表显示了两个入口点的 GUID 值。

| 入口点           | GUID                                   |
|-----------------------|----------------------------------------|
| 打印首选项     | {EC8F261F-267C-469F-B5D6-3933023C29CC} |
| 打印机通知 | {23BB1328-63DE-4293-915B-A6A23D929ACB} |

打印机之外的打印机驱动程序安装的扩展插件需要使用注册表进行注册。 这可确保该打印机可以安装扩展，而不考虑将后台处理程序或在客户端计算机上的 v4 配置模块的状态。

一旦 PrintNotify 服务启动时，它将检查下的注册表项\[OfflineRoot\]路径并处理任何挂起的注册或 unregistrations。 完成任何挂起的注册或 unregistrations 后，会在真实时间中删除注册表项。 请注意，是否您使用脚本或迭代的过程将注册表项，您可能需要重新创建\\ \[PrinterExtensionID\]密钥每次您指定\\ \[PrinterDriverId\]密钥。 不会删除不完整或格式不正确的密钥。

此注册时才需要在首次安装。 下面的示例显示了用于注册打印机扩展正确的注册表密钥格式。

> [!NOTE]
> **\[OfflineRoot\]** 用作 HKEY 速记\_本地\_机\\软件\\Microsoft\\Windows NT\\CurrentVersion\\打印\\OfflinePrinterExtensions。

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

例如，以下键集将注册使用的打印机扩展 {*PrinterExtensionIDGuid*} PrinterExtensionID 和完全限定的路径"c:\\Program Files\\Fabrikam\\pe.exe"可执行文件 {*PrinterDriverID1Guid*} 和 {*PrinterDriverID2Guid*} PrinterDriverIDs，使用的打印机首选项和打印机通知原因。

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

若要卸载同一打印机扩展，应指定以下键集。

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

打印机扩展可以在用户启动的上下文和事件启动的上下文中运行，因为它可用于将无法确定您的打印机扩展操作的上下文。 这可以使应用程序，例如，如果已启动的通知，枚举上的所有队列的状态或打印首选项。 Microsoft 建议从驱动程序 （例如带有的 MSI 或 setup.exe） 单独安装的打印机扩展应使用命令行开关上开始菜单快捷方式，或在注册表中填充的 AppPath 项中注册。 由于与驱动程序一起安装的打印机扩展安装到 DriverStore 时，这些将不会启动打印首选项或打印机通知事件的外部。 因此指定命令行开关不支持这种情况下。

当打印机扩展注册当前 PrinterDriverID 时，它必须包括 PrinterDriverID AppPath 中。 例如，对于包含名称的打印机扩展应用*printerextension.exe*，并将 PrinterDriverID 值 *{GUID}*，则\[PrinterExtensionAppPath\]将如下所示以下内容：

```console
"C:\program files\fabrikam\printerextension.exe {GUID}"
```

### <a name="enabling-events"></a>启用事件

在运行时，打印机扩展必须启用的当前 PrinterDriverID 触发事件。 这是通过此参数传递给应用 PrinterDriverID\[ \]数组，并且它允许打印系统提供相应的事件上下文，用于处理打印首选项或打印机通知等原因。

因此该应用程序应为当前 PrinterDriverID 创建新 PrinterExtensionManager、 注册一个委托来处理 OnDriverEvent 事件和调用与 PrinterDriverID EnableEvents 方法。 下面的代码段演示了此方法。

```csharp
PrinterExtensionManager mgr = new PrinterExtensionManager();
mgr.OnDriverEvent += OnDriverEvent;
mgr.EnableEvents(new Guid(PrinterDriverID1));
```

如果应用不会调用 EnableEvents 在 5 秒内，Windows 将超时并启动一个标准用户界面。 若要缓解此问题，打印机扩展应遵循的最新性能最佳实践，其中包括：

- 尽可能多的应用程序初始化尽可能延迟截止时间之后调用 EnableEvents。 在此之后，通过使用异步方法并不在初始化期间会阻止 UI 线程优先级 UI 响应能力。

- 使用 ngen 安装期间生成的本机映像。 有关详细信息，请参阅[本机映像生成器](https://msdn.microsoft.com/library/6t9t5wcf.aspx)。

- 使用性能度量工具上加载的查找性能问题。 有关详细信息，请参阅[Windows 性能分析工具](https://msdn.microsoft.com/performance/cc825801.aspx)。

### <a name="driverevent-handler"></a>DriverEvent 处理程序

注册一个 OnDriverEvent 处理程序并启用了事件，如果启动打印机扩展以处理打印首选项或打印机通知后，将调用该处理程序。 在前面的代码片段中，一个名为 OnDriverEvent 方法注册为事件处理程序。 在以下代码片段中， *PrinterExtensionEventArgs*参数是可以实现打印首选项和打印机通知方案，来构造的对象。 *PrinterExtensionEventArgs*是包装[ **IPrinterExtensionEventArgs**](https://msdn.microsoft.com/library/windows/hardware/hh973207)。

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

为了防止不良用户体验与崩溃或速度缓慢打印机扩展，Windows 实现超时，如果 EnableEvents 不在一小段时间之后启动应用程序中调用。 若要启用调试，如果没有一个调试器附加到 PrintNotify 服务，将禁用此超时。

在大多数情况下，但是，所有应用相关的代码我们感兴趣，运行期间或之后 OnDriverEvent 回调。 在开发期间，也可能是用于显示一个消息框在开始之前打印首选项或打印机通知体验从 OnDriverEvent 回调。 消息框出现时，请返回到 Visual Studio 并单击**调试** &gt; **附加到进程**选择过程的名称。 最后，请返回到你的 MessageBox，并单击确定以继续。 这将确保你看到异常并到达任何断点，从该点向前。

新 ReasonIds 可能在将来支持。 因此，打印机扩展必须显示检查 ReasonID，必须使用"else"语句来检测最后一个已知的 ReasonID。 如果接收到的和未知 ReasonID，应用应正常退出。

### <a name="print-preferences"></a>打印首选项

打印首选项取决于 PrintSchemaEventArgs.Ticket 对象。 此对象将封装 PrintTicket 和 PrintCapabilities 文档描述的功能和设备的选项。 此外提供基础的 XML 时，对象模型轻松使用这些格式。

在每个[ **IPrintSchemaTicket** ](https://msdn.microsoft.com/library/windows/hardware/hh451398)或[ **IPrintSchemaCapabilities** ](https://msdn.microsoft.com/library/windows/hardware/hh451256)对象功能 ([ **IPrintSchemaFeature**](https://msdn.microsoft.com/library/windows/hardware/hh451284)) 和选项 ([**IPrintSchemaOption**](https://msdn.microsoft.com/library/windows/hardware/hh451335))。 虽然用于功能和选项的接口是相同的无论来源如何的行为发生作为基础的 XML 结果略有变化。 例如，PrintCapabilities 文档指定多个选项，每个功能，而 PrintTicket 文档指定仅所选 （或默认值） 选项。 同样，PrintCapabilities 文档指定本地化的显示字符串，而 PrintTicket 文档不这样做。

[PrinterExtensionSample](https://go.microsoft.com/fwlink/p/?LinkId=617945)使用数据绑定来创建打印机首选项的组合框控件。 Microsoft 建议使用数据绑定，因为它使代码更易于维护，从而不赞成这样做。 在 WPF 中的数据绑定的详细信息，请参阅[数据绑定概述](https://msdn.microsoft.com/library/ms752347.aspx)。

为了获得最佳性能，Microsoft 建议对 GetPrintCapabilities 调用仅需要更新 PrintCapabilities 文档时完成。

因为用户可选择使用数据绑定组合框控件，所以 PrintTicket 对象自动更新。 当用户最后单击**确定**，开始异步验证和完成的链。 此异步模式是为了防止长时间运行的任务，从在 UI 线程上发生，导致挂起了打印首选项用户界面或正在打印的应用程序中广泛使用。 下面是用于处理 PrintTicket 更改用户单击鼠标后的步骤的列表**确定**。

1. 验证 PrintSchemaTicket 使用 asynchrously [ **IPrintSchemaTicket::ValidateAsync** ](https://msdn.microsoft.com/library/windows/hardware/hh451448)方法。

1. 完成异步验证后，公共语言运行时 (CLR) 调用 PrintTicketValidateCompleted 方法。

    1. 如果验证成功，它将调用 CommitPrintTicketAsync 方法，并且调用 CommitPrintTicketAsync [ **IPrintSchemaTicket::CommitAsync** ](https://msdn.microsoft.com/library/windows/hardware/hh451382)方法。 和更新 PrintTicket 成功完成，这将调用 PrintTicketCommitCompleted 方法，后者调用调用 PrinterExtensionEventArgs.Request.Complete 方法，以指示打印首选项已完成的便捷方法，然后它将关闭该应用程序。

    1. 否则，它显示给用户以处理约束情况显示 UI。

如果用户单击取消，或直接关闭打印首选项窗口中，打印机扩展 IPrinterExtensionEventArgs.Request.Cancel 使用调用相应的 HRESULT 值和消息的错误日志。

如果打印机扩展的过程已关闭，并且不调用的完成或取消方法，如前面段落所述，然后打印系统将自动回退到使用 Microsoft 提供的 UI。

若要检索设备状态信息，打印机扩展可以使用 Bidi 查询打印设备。 例如，若要显示墨迹状态或其他类型的有关设备的状态，打印机扩展可以使用 IPrinterExtensionEventArgs.PrinterQueue.SendBidiQuery 方法向设备发出 Bidi 查询。 获取最新的 Bidi 状态是设置了 OnBidiResponseReceived 事件的事件处理程序并调用 SendBidiQuery 方法与有效 Bidi 查询涉及一个两步过程。 下面的代码段显示了此两步过程。

```csharp
PrinterQueue.OnBidiResponseReceived += new
EventHandler<PrinterQueueEventArgs>(OnBidiResponseReceived);
PrinterQueue.SendBidiQuery("\\Printer.consumables");
```

当收到 Bidi 响应时，将调用以下事件处理程序。 请注意，此事件处理程序也模拟的墨迹状态实现中，当设备不可用的可能是对开发非常有用。 PrinterQueueEventArgs 对象包括 HRESULT 和 Bidi XML 响应。 Bidi XML 响应的详细信息，请参阅[Bidi 请求和响应架构](https://msdn.microsoft.com/library/windows/desktop/dd183368.aspx)。

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

准确地说是相同的打印首选项中调用的打印机通知。 在 OnDriverEvent 处理程序中，如果 IPrinterExtensionEventArgs 指示 ReasonID 匹配 DriverEvents GUID，然后我们可以构建的体验来处理此事件。

[PrinterExtensionSample](https://go.microsoft.com/fwlink/p/?LinkId=617945)项目并不演示功能的打印机的通知体验，但以下变量是在这种处理最有帮助。

- PrinterExtensionEventArgs.BidiNotification – 此项带有 Bidi XML 导致要触发的事件。

- PrinterExtensionEventArgs.DetailedReasonId – 此文件包含 eventID 驱动程序事件 xml 文件中的 GUID。

通知的 IPrinterExtensionEventArgs 对象中的最重要属性是 BidiNotification 属性。 这将把 Bidi XML 导致要触发的事件。 Bidi XML 响应的详细信息，请参阅[Bidi 请求和响应架构](https://msdn.microsoft.com/library/windows/desktop/dd183368.aspx)。

### <a name="managing-printers"></a>管理打印机

为了支持作为应用程序可以用作一个中心管理/维护打印机的打印机扩展角色，则可以枚举打印队列为其注册当前打印机扩展，并获得每个队列的状态。 不说明了这一点在 PrinterExtensionSample 项目中，但可以将下面的代码段添加到 App.xaml.cs 注册事件处理程序的 Main 方法。

```csharp
mgr.OnPrinterQueuesEnumerated += new EventHandler<PrinterQueuesEnumeratedEventArgs>(mgr_OnPrinterQueuesEnumerated);
```

枚举队列后, 会调用事件处理程序和状态操作发生。 若要确保枚举打印队列的列表的最新的即使用户已安装更多的队列，因为它已打开的应用程序生命周期内定期引发此事件。 因此，很重要的事件处理程序不会创建新的窗口每次执行，而且这下面的代码段中所示。

```csharp
static void mgr_OnPrinterQueuesEnumerated(object sender, PrinterQueuesEnumeratedEventArgs e)
{
    foreach (IPrinterExtensionContext pContext in e)
    {
        // show status
    }
}
```

若要执行维护任务使用的打印机扩展，Microsoft 建议的旧 WritePrinter API 用作以下伪代码中所述。

```Pseudocode
OpenPrinter
    StartDocPrinter
        StartPagePrinter
          WritePrinter
        EndPagePrinter
    EndDocPrinter
ClosePrinter
```

有关如何将这些旧 Api 封送到.NET 的详细信息，请参阅[如何将原始数据发送到打印机，通过使用 Visual C# .NET](http://support.microsoft.com/?kbid=322091)或[如何使用 Visual Basic.NET 将原始数据发送到打印机](http://support.microsoft.com/?kbid=322090)。

## <a name="printer-extension-performance-best-practices"></a>打印机扩展的性能最佳实践

为了确保获得最佳用户体验，打印机扩展应旨在尽可能快加载。 打印机扩展插件示例的项目是.NET 应用程序，这意味着它获取内置到适合的格式用于本机处理器体系结构必须在运行时中编译中间语言 (IL)。 在安装期间，Microsoft 建议根据最佳实践，以确保应用程序已被编译为本机系统体系结构将安装打印机扩展。 有关代码的编译和安装的最佳做法的详细信息，请参阅[提高您的桌面应用程序的启动性能](http://blogs.msdn.com/b/dotnet/archive/2012/03/20/improving-launch-performance-for-your-desktop-applications.aspx)。

Microsoft 还建议打印机扩展推迟初始化任务，例如在调用方法 EnableEvents 后加载之前的资源。 这将减少在 5 秒超时之前调用 EnableEvents，打印机扩展应用程序的可能性。

在 OnDriverEvent 调用后，打印机扩展应初始化它们的 UI，并在可能的情况以确保响应能力作为可能的这会让使用异步方法快速绘制。 打印机扩展应不依赖于网络调用，或若要创建的初始窗口状态 Bidi 打印首选项或打印机通知。

用户进行选项使用影响 PrintTicket，打印机扩展插件的 UI 应使在屏幕使用的 IPrintSchemaTicket::ValidateAsync 方法以便尽可能验证尽早更改。 最后，应使用的打印机扩展[ **IPrintSchemaTicket::CommitAsync** ](https://msdn.microsoft.com/library/windows/hardware/hh451382)方法，以提交 PrintTicket 更改。

打印机扩展始终执行的过程中的过程调用它们。 因此您必须记住窗口行为时你正在开发的打印机扩展：

- **WindowParent**属性从[ **IPrinterExtensionEventArgs** ](https://msdn.microsoft.com/library/windows/hardware/hh973207)指定调用应用程序窗口的句柄。
- **WindowModal**属性从[ **IPrinterExtensionEventArgs** ](https://msdn.microsoft.com/library/windows/hardware/hh973207)指定打印机扩展 （在打印首选项模式下） 是否应以模式方式运行。

打印机扩展插件示例演示如何创建一个 UI，通常为最顶层窗口启动。 但在某些情况下，将不会在 UI 显示在前台，如时引起 UI 要调用的进程正在运行时的不同完整性级别，或对于不同的处理器体系结构编译过程时。 在这种情况下，打印机扩展应调用 FlashWindowEx 请求用户权限以通过在任务栏中闪烁图标转到前台。

## <a name="related-topics"></a>相关主题

[Bidi 请求和响应架构](https://msdn.microsoft.com/library/windows/desktop/dd183368.aspx)

[数据绑定概述](https://msdn.microsoft.com/library/ms752347.aspx)

[如何使用 Visual Basic.NET 将原始数据发送到打印机](http://support.microsoft.com/?kbid=322090)

[如何将原始数据发送到打印机，由使用视觉对象C#.NET](http://support.microsoft.com/?kbid=322091)

[提高桌面应用程序的启动性能](http://blogs.msdn.com/b/dotnet/archive/2012/03/20/improving-launch-performance-for-your-desktop-applications.aspx)

[本机映像生成器](https://msdn.microsoft.com/library/6t9t5wcf.aspx)

[打印架构接口](https://msdn.microsoft.com/library/windows/hardware/hh464019)

[打印机扩展插件示例](https://go.microsoft.com/fwlink/p/?LinkId=617945)

[Windows 性能分析工具](https://msdn.microsoft.com/performance/cc825801.aspx)
