---
title: 如何在 UWP 设备应用中进行打印机维护
description: 在 Windows 8.1 中，UWP 设备应用可以执行打印机维护，如对齐打印头和清洁喷嘴。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 706cb112fa55a7c35fb931eb37c4396508448a21
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815175"
---
# <a name="how-to-do-printer-maintenance-in-a-uwp-device-app"></a>如何在 UWP 设备应用中进行打印机维护

在 Windows 8.1 中，UWP 设备应用可以执行打印机维护，如对齐打印头和清洁喷嘴。 本主题使用 [打印作业管理和打印机维护](https://go.microsoft.com/fwlink/p/?LinkID=299829) 示例的 c # 版本来演示如何使用双向通信 () 双向通信来执行此类设备维护。 若要详细了解 UWP 设备应用的详细信息，请参阅了解 [uwp 设备应用](meet-uwp-device-apps.md)。

[打印作业管理和打印机维护](https://go.microsoft.com/fwlink/p/?LinkID=299829)示例的 c # 版本演示了在 **DeviceAppForPrinters2** 项目中通过 **DeviceMaintenance.xaml.cs** 文件进行的打印机维护。 若要使用双向，示例将在 **PrinterExtensionLibrary** 项目中使用打印机扩展库。 打印机扩展库提供了一种便捷的方式来访问 v4 打印驱动程序的打印机扩展接口。 有关详细信息，请参阅 [打印机扩展库概述](printer-extension-library-overview.md)。

>[!NOTE]
>本主题中所示的代码示例基于 c # 版本的 [打印作业管理和打印机维护](https://go.microsoft.com/fwlink/p/?LinkID=299829) 示例。 此示例在 JavaScript 和 c + + 中也可用。 请注意，由于 c + + 可以直接访问 COM，因此该示例的 c + + 版本不包括代码库项目。 下载示例以查看最新版本的代码。

## <a name="printer-maintenance"></a>打印机维护

Windows 8.1 在 v4 打印机驱动程序中引入了新的打印机扩展接口，可用于实现设备维护： [**IPrinterBidiSetRequestCallback**](/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprinterbidisetrequestcallback)、 [**IPrinterExtensionAsyncOperation**](/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprinterextensionasyncoperation) 和 [**IPrinterQueue2**](/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprinterqueue2)。 通过这些接口，可以将双向请求异步发送到端口监视器，以便将其转换为设备和特定于协议的命令，然后将其发送到打印机。 有关详细信息，请参阅 [设备维护 (V4 打印机驱动程序) ](../print/device-maintenance.md)。

**提示**  C # 和 JavaScript 应用无法直接与 COM Api 一起使用。 如果要编写 c # 或 JavaScript UWP 设备应用，请使用打印机扩展库来访问这些接口 (如本主题) 中所示。

## <a name="prerequisites"></a>先决条件

准备工作：

1. 请确保您的打印机是使用 v4 打印驱动程序安装的。 有关详细信息，请参阅 [开发 v4 打印驱动程序](../print/v4-printer-driver.md)。
2. 设置开发 PC。 有关下载工具和创建开发人员帐户的信息[，请参阅入门。](getting-started.md)
3. 将应用与应用商店相关联。 请参阅 [创建 UWP 设备应用](step-1--create-a-uwp-device-app.md) 了解相关信息。
4. 为打印机创建将其与应用程序关联的设备元数据。 有关详细信息，请参阅 [创建设备元数据](step-2--create-device-metadata.md) 。
5. 构建应用程序主页的 UI。 所有 UWP 设备应用都可以从 "开始" 启动，它们将全屏显示。 使用 "开始体验" 以与设备的特定品牌和功能匹配的方式突出显示你的产品或服务。 它可以使用的 UI 控件类型没有任何特殊限制。 若要开始设计全屏体验，请参阅 [Microsoft Store 设计原则](https://go.microsoft.com/fwlink/p/?LinkID=299845)。
6. 如果正在编写的是用 c # 或 JavaScript 编写应用，请将 **PrinterExtensionLibrary** 项目添加到 UWP 设备应用解决方案。 可以在 [打印作业管理和打印机维护](https://go.microsoft.com/fwlink/p/?LinkID=299829) 示例中找到此项目。

>[!NOTE]
>由于 c + + 可以直接访问 COM，因此，c + + 应用不需要单独的库即可使用基于 COM 的打印机设备上下文。

## <a name="step-1-prepare-bidi-request"></a>步骤1：准备双向请求

设备维护接口要求双向请求为字符串形式的 XML 数据。 可以在应用中有意义的地方构造双向请求。 例如，可以将双向请求保存为字符串常量，或根据用户输入动态创建它们。 [打印作业管理和打印机维护](https://go.microsoft.com/fwlink/p/?LinkID=299829)示例在方法中构建默认请求时发生 `OnNavigatedTo` 。 有关双向的详细信息，请参阅 [双向通信](../print/bidirectional-communication.md)。

此示例来自 `OnNavigatedTo` **DeviceMaintenance.xaml.cs** 文件的方法。

```CSharp
string defaultBidiQuery =
    "<bidi:Set xmlns:bidi=\"http://schemas.microsoft.com/windows/2005/03/printing/bidi\">\r\n" +
    "    <Query schema='\\Printer.Maintenance:CleanHead'>\r\n" +
    "        <BIDI_BOOL>false</BIDI_BOOL>\r\n" +
    "    </Query>\r\n" +
    "</bidi:Set>";
```

## <a name="step-2-find-printer"></a>步骤2：查找打印机

在您的应用程序可以将命令发送到打印机之前，必须先找到打印机。 为此， [打印作业管理和打印机维护](https://go.microsoft.com/fwlink/p/?LinkID=299829) 示例在 `PrinterEnumeration` **PrinterEnumeration.cs** 文件) 中包含一个名为 (的便利类。 此类通过设备元数据查找与应用程序关联的所有打印机，并返回一个 `PrinterInfo` 对象列表，其中包含每个打印机的名称和设备 id。

此示例来自 `EnumeratePrinters_Click` **DeviceMaintenance.xaml.cs** 文件的方法。 其中显示了该示例如何使用 `PrinterEnumeration` 类获取关联打印机的列表。

```CSharp
private async void EnumeratePrinters_Click(object sender, RoutedEventArgs e)
{
    try
    {
        rootPage.NotifyUser("Enumerating printers. Please wait", NotifyType.StatusMessage);

        // Retrieve the running app's package family name, and enumerate associated printers.
        string currentPackageFamilyName = Windows.ApplicationModel.Package.Current.Id.FamilyName;

        // Enumerate associated printers.
        PrinterEnumeration pe = new PrinterEnumeration(currentPackageFamilyName);
        List<PrinterInfo> associatedPrinters = await pe.EnumeratePrintersAsync();

        // Update the data binding source on the combo box that displays the list of printers.
        PrinterComboBox.ItemsSource = associatedPrinters;
        if (associatedPrinters.Count > 0)
        {
            PrinterComboBox.SelectedIndex = 0;
            rootPage.NotifyUser(associatedPrinters.Count + " printers enumerated", NotifyType.StatusMessage);
        }
        else
        {
            rootPage.NotifyUser(DisplayStrings.NoPrintersEnumerated, NotifyType.ErrorMessage);
        }
    }
    catch (Exception exception)
    {
        rootPage.NotifyUser("Caught an exception: " + exception.Message, NotifyType.ErrorMessage);
    }
}
```

**提示**  有关和类的详细 `PrinterEnumeration` 信息 `PrinterInfo` ，请参阅 **PrinterEnumeration.cs** 文件。

## <a name="step-3-send-bidi-request"></a>步骤3：发送双向请求

若要发送双向请求，设备维护接口需要双向字符串和回调。 在 `SendBidiRequest_Click` 方法中，示例首先使用 `PrinterInfo` 对象来创建一个名为的打印机扩展上下文对象 `context` 。 然后 `PrinterBidiSetRequestCallback` ，将创建一个对象，并添加一个事件处理程序来处理回调的 `OnBidiResponseReceived` 事件。 最后，使用打印机扩展上下文的 `SendBidiSetRequestAsync` 方法发送双向字符串和回调。

此示例来自 `SendBidiRequest_Click` **DeviceMaintenance.xaml.cs** 文件的方法。

```CSharp
private void SendBidiRequest_Click(object sender, RoutedEventArgs e)
{
    try
    {
        PrinterInfo queue = (PrinterInfo)PrinterComboBox.SelectedItem;

        // Retrieve a COM IPrinterExtensionContext object, using the static WinRT factory.
        // Then instantiate one "PrinterExtensionContext" object that allows operations on the COM object.
        Object comComtext = Windows.Devices.Printers.Extensions.PrintExtensionContext.FromDeviceId(queue.DeviceId);
        PrinterExtensionContext context = new PrinterExtensionContext(comComtext);

        // Create an instance of the callback object, and perform an asynchronous 'bidi set' operation.
        PrinterBidiSetRequestCallback callback = new PrinterBidiSetRequestCallback();

        // Add an event handler to the callback object's OnBidiResponseReceived event.
        // The event handler will be invoked once the Bidi response is received.
        callback.OnBidiResponseReceived += OnBidiResponseReceived;

        // Send the Bidi "Set" query asynchronously.
        IPrinterExtensionAsyncOperation operationContext
            = context.Queue.SendBidiSetRequestAsync(BidiQueryInput.Text, callback);

        // Note: The 'operationContext' object can be used to cancel the operation if required.
    }
    catch (Exception exception)
    {
        rootPage.NotifyUser("Caught an exception: " + exception.Message, NotifyType.ErrorMessage);
    }
}
```

## <a name="step-4-receive-bidi-response"></a>步骤4：接收双向响应

当双向 "set" 操作完成时，将调用类型为的回调对象 `PrinterBidiSetRequestCallback` 。 此回调负责处理 HRESULT 响应中的错误，然后 `OnBidiResponseReceived` 通过事件参数来触发事件，从而发送双向响应。

此示例显示了 `PrinterBidiSetRequestCallback` **DeviceMaintenance.xaml.cs** 文件中的类定义。

```CSharp
internal class PrinterBidiSetRequestCallback : IPrinterBidiSetRequestCallback
{
    /// <summary>
    /// This method is invoked when the asynchronous Bidi "Set" operation is completed.
    /// </summary>
    public void Completed(string response, int statusHResult)
    {
        string result;

        if (statusHResult == (int)HRESULT.S_OK)
        {
            result = "The response is \r\n" + response;
        }
        else
        {
            result = "The HRESULT received is: 0x" + statusHResult.ToString("X") + "\r\n" +
                     "No Bidi response was received";
        }

        // Invoke the event handlers when the Bidi response is received.
        OnBidiResponseReceived(null, result);
    }

    /// <summary>
    /// This event will be invoked when the Bidi 'set' response is received.
    /// </summary>
    public event EventHandler<string> OnBidiResponseReceived;
}
```

然后，将双向响应发送到 `OnBidiResponseReceived` 方法，其中用于在 `Dispatcher` UI 线程上显示结果。

此示例来自 `OnBidiResponseReceived` **DeviceMaintenance.xaml.cs** 文件的方法。

```CSharp
internal async void OnBidiResponseReceived(object sender, string bidiResponse)
{
    await Dispatcher.RunAsync(Windows.UI.Core.CoreDispatcherPriority.Normal, () =>
    {
        BidiResponseOutput.Text = bidiResponse;
    });
}
```

## <a name="testing"></a>正在测试

在可以测试 UWP 设备应用之前，必须使用设备元数据将其链接到您的打印机。

- 你需要打印机的设备元数据包的副本，以便向其添加设备应用信息。 如果没有设备元数据，可以使用 **设备元数据创作向导** 生成它，如主题为 [UWP 设备应用创建设备元数据](./step-2--create-device-metadata.md)中所述。

  >[!NOTE]
  >若要使用 **设备元数据创作向导**，在完成本主题中的步骤之前，必须安装 Microsoft Visual Studio Professional、Microsoft Visual Studio Ultimate 或 [独立的 SDK for Windows 8.1](https://go.microsoft.com/fwlink/p/?linkid=309209)。 为 Windows 安装 Microsoft Visual Studio Express 会安装不包括向导的 SDK 版本。

以下步骤生成应用并安装设备元数据。

1. 启用测试签名。
    1. 双击 "DeviceMetadataWizard.exe，从 *% ProgramFiles (x86) %* Windows 工具包 8.1 bin **X86 启动设备元数据创作向导** \\ \\ \\ \\ **DeviceMetadataWizard.exe**
    2. 从 " **工具** " 菜单中，选择 " **启用测试签名**"。

2. 重新启动计算机
3. 通过打开解决方案 ( .sln) 文件来生成解决方案。 加载示例后，按 F7 或从顶部菜单中转到 " **生成- &gt; 生成解决方案** "。

4. 断开连接并卸载打印机。 此步骤是必需的，以便 Windows 将在下一次检测到设备时读取更新的设备元数据。
5. 编辑并保存设备元数据。 若要将设备应用链接到设备，你必须将设备应用关联到设备。 **注意：** 如果尚未创建设备元数据，请参阅 [为 UWP 设备应用创建设备元数据](./step-2--create-device-metadata.md)。
    1. 如果 **设备元数据创作向导** 尚未打开，请通过双击 "DeviceMetadataWizard.exe" 从 *% ProgramFiles (x86) %* \\ Windows 工具包 \\ 8.1 \\ bin \\ x86 **DeviceMetadataWizard.exe** 启动它。
    2. 单击 " **编辑设备元数据**"。 这将允许你编辑现有的设备元数据包。
    3. 在 " **打开** " 对话框中，找到与 UWP 设备应用关联的设备元数据包。  (其文件扩展名为 **devicemetadata** 。 ) 
    4. 在 " **指定 uwp 设备应用信息** " 页上，在 " **UWP 设备应用** " 框中输入 Microsoft Store 应用信息。 单击 " **导入 UWP 应用程序清单文件** " 以自动输入 **包名称**、 **发布者名称** 和 **UWP 应用 ID**。
    5. 如果你的应用正在注册打印机通知，请填写 **通知处理程序** 框。 在 " **事件 ID**" 中，输入打印事件处理程序的名称。 在 " **事件资产**" 中，输入代码所在的文件的名称。
    6. 完成后，单击 " **下一步** "，直到到达 " **完成** " 页。
    7. 在 " **查看设备元数据包** " 页上，确保所有设置均正确，并选中 "将 **设备元数据包复制到本地计算机上的元数据存储区** " 复选框。 然后单击“保存”  。
6. 重新连接打印机，以便 Windows 在连接设备时读取更新的设备元数据。

## <a name="related-topics"></a>相关主题

[设备维护 (v4 打印机驱动程序) ](../print/device-maintenance.md)

[开发 v4 打印驱动程序](../print/v4-printer-driver.md)

[双向通信](../print/bidirectional-communication.md)

[UWP 应用入门](getting-started.md)

[ (分步指南创建 UWP 设备应用) ](step-1--create-a-uwp-device-app.md)

[ (分步指南创建 UWP 设备应用的设备元数据) ](step-2--create-device-metadata.md)
