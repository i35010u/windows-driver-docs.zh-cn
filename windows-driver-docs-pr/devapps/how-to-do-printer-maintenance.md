---
title: 如何执行 UWP 设备应用中的打印机维护
description: 在 Windows 8.1 UWP 设备应用程序可以执行打印机维护，如对齐打印头和清洗喷嘴。
ms.assetid: 52141F66-872A-4381-92C8-B04ABDABA7AD
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e1288d4566c91c52f74a8e31cab779be386144df
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369356"
---
# <a name="how-to-do-printer-maintenance-in-a-uwp-device-app"></a>如何执行 UWP 设备应用中的打印机维护


在 Windows 8.1 UWP 设备应用程序可以执行打印机维护，如对齐打印头和清洗喷嘴。 本主题使用C#的版本[打印作业管理和打印机维护](https://go.microsoft.com/fwlink/p/?LinkID=299829)示例，用于演示如何使用双向通信 (Bidi) 来执行此类设备的维护。 若要在一般情况下了解有关 UWP 的设备应用程序的详细信息，请参阅[满足 UWP 设备应用](meet-uwp-device-apps.md)。

C#的版本[打印作业管理和打印机维护](https://go.microsoft.com/fwlink/p/?LinkID=299829)示例演示如何使用打印机维护**DeviceMaintenance.xaml.cs**中的文件**DeviceAppForPrinters2**项目。 若要使用 Bidi，该示例使用的打印机扩展库中**PrinterExtensionLibrary**项目。 打印机扩展库提供了方便地访问 v4 打印驱动程序的打印机扩展插件接口。 有关详细信息，请参阅[打印机扩展库概述](printer-extension-library-overview.md)。

**请注意**  本主题中所示的代码示例基于C#的版本[打印作业管理和打印机维护](https://go.microsoft.com/fwlink/p/?LinkID=299829)示例。 此示例也会出现在 JavaScript 和C++。 请注意，由于C++可以直接访问 COMC++示例的版本不包括代码库项目。 下载示例，请参阅最新版本的代码。

 

## <a name="span-idprintermaintenancespanspan-idprintermaintenancespanspan-idprintermaintenancespanprinter-maintenance"></a><span id="Printer_maintenance"></span><span id="printer_maintenance"></span><span id="PRINTER_MAINTENANCE"></span>打印机的维护


Windows 8.1 引入了新的打印机扩展插件接口，可用于实现设备维护 v4 打印机驱动程序中：[**IPrinterBidiSetRequestCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/printerextension/nn-printerextension-iprinterbidisetrequestcallback)， [ **IPrinterExtensionAsyncOperation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/printerextension/nn-printerextension-iprinterextensionasyncoperation) ，以及[ **IPrinterQueue2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/printerextension/nn-printerextension-iprinterqueue2). 这些接口使能够以异步方式将 Bidi 请求发送到端口监视器，以便他们可以转换为设备和特定于协议的命令，然后发送到打印机。 有关详细信息，请参阅[设备维护 （v4 打印机驱动程序）](https://docs.microsoft.com/windows-hardware/drivers/print/device-maintenance)。

**提示**   C#和 JavaScript 应用程序不能直接使用 COM Api。 如果您要编写C#或 JavaScript UWP 设备应用，使用打印机扩展库来访问这些接口 （如本主题中所示）。

 

## <a name="span-idprerequisitesspanspan-idprerequisitesspanspan-idprerequisitesspanprerequisites"></a><span id="Prerequisites"></span><span id="prerequisites"></span><span id="PREREQUISITES"></span>先决条件


开始之前：

1.  请确保使用 v4 打印驱动程序安装您的打印机。 有关详细信息，请参阅[开发 v4 打印驱动程序](https://go.microsoft.com/fwlink/p/?LinkId=314231)。
2.  获取对开发计算机设置。 请参阅[入门](getting-started.md)有关下载工具和创建开发人员帐户信息。
3.  将你的应用与应用商店相关联。 请参阅[创建 UWP 设备应用](step-1--create-a-uwp-device-app.md)有关的信息。
4.  创建设备元数据为您将其与您的应用程序关联的打印机。 请参阅[创建设备元数据](step-2--create-device-metadata.md)有关的详细信息。
5.  构建您的应用程序的主页上的 UI。 可以从开始，它们将显示的全屏启动所有 UWP 设备应用程序。 使用入门体验突出显示你的产品或匹配特定品牌的方式和你的设备的功能中的服务。 没有任何特殊限制可以使用 UI 控件的类型。 若要开始使用的设计的全屏体验，请参阅[Microsoft Store 设计原则](https://go.microsoft.com/fwlink/p/?LinkID=299845)。
6.  如果您正在编写您编写的应用程序与C#或 JavaScript 中，添加**PrinterExtensionLibrary**到 UWP 设备应用程序解决方案的项目。 您可以找到此项目中的[打印作业管理和打印机维护](https://go.microsoft.com/fwlink/p/?LinkID=299829)示例。
    **请注意**  由于C++可以直接访问 COMC++应用程序不需要单独的库以使用基于 COM 的打印机设备上下文。

     

## <a name="span-idstep1preparebidirequestspanspan-idstep1preparebidirequestspanspan-idstep1preparebidirequestspanstep-1-prepare-bidi-request"></a><span id="Step_1__Prepare_Bidi_request"></span><span id="step_1__prepare_bidi_request"></span><span id="STEP_1__PREPARE_BIDI_REQUEST"></span>步骤 1：准备 Bidi 请求


设备维护接口需要 Bidi 请求是 XML 数据形式的字符串。 适当的时候应用程序中，您可以构建 Bidi 请求。 例如，无法将 Bidi 请求另存为字符串常量或动态创建它们根据用户输入。 [打印作业管理和打印机维护](https://go.microsoft.com/fwlink/p/?LinkID=299829)示例恰好构造中的默认请求`OnNavigatedTo`方法。 Bidi 的详细信息，请参阅[的双向通信](https://go.microsoft.com/fwlink/p/?LinkId=317192)。

此示例摘自`OnNavigatedTo`方法**DeviceMaintenance.xaml.cs**文件。

```CSharp
string defaultBidiQuery =
    "<bidi:Set xmlns:bidi=\"http://schemas.microsoft.com/windows/2005/03/printing/bidi\">\r\n" +
    "    <Query schema='\\Printer.Maintenance:CleanHead'>\r\n" +
    "        <BIDI_BOOL>false</BIDI_BOOL>\r\n" +
    "    </Query>\r\n" +
    "</bidi:Set>";
```

## <a name="span-idstep2findprinterspanspan-idstep2findprinterspanspan-idstep2findprinterspanstep-2-find-printer"></a><span id="Step_2__Find_printer"></span><span id="step_2__find_printer"></span><span id="STEP_2__FIND_PRINTER"></span>步骤 2：查找打印机


您的应用程序可以将命令发送到打印机之前，它首先必须找到打印机。 若要执行此操作，[打印作业管理和打印机维护](https://go.microsoft.com/fwlink/p/?LinkID=299829)示例包含一个名为的方便类`PrinterEnumeration`(在**PrinterEnumeration.cs**文件)。 此类查找与您的应用程序通过设备元数据相关联的所有打印机并返回一系列`PrinterInfo`对象，包含为每个打印机的设备 Id 和名称。

此示例摘自`EnumeratePrinters_Click`方法**DeviceMaintenance.xaml.cs**文件。 它显示如何使用示例`PrinterEnumeration`类，以获取一组相关联的打印机。

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

**提示**  有关详细信息`PrinterEnumeration`并`PrinterInfo`类，请参见**PrinterEnumeration.cs**文件。

 

## <a name="span-idstep3sendbidirequestspanspan-idstep3sendbidirequestspanspan-idstep3sendbidirequestspanstep-3-send-bidi-request"></a><span id="Step_3__Send_Bidi_request"></span><span id="step_3__send_bidi_request"></span><span id="STEP_3__SEND_BIDI_REQUEST"></span>步骤 3：发送 Bidi 请求


若要发送 Bidi 请求，则设备维护接口要求在 Bidi 字符串和一个回调。 在中`SendBidiRequest_Click`方法，该示例首先使用`PrinterInfo`对象来创建一个名为打印机扩展上下文对象`context`。 然后`PrinterBidiSetRequestCallback`创建对象，并添加事件处理程序以处理回调的`OnBidiResponseReceived`事件。 最后，打印机扩展上下文的`SendBidiSetRequestAsync`方法用于发送 Bidi 字符串和回调。

此示例摘自`SendBidiRequest_Click`方法**DeviceMaintenance.xaml.cs**文件。

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

## <a name="span-idstep4receivebidiresponsespanspan-idstep4receivebidiresponsespanspan-idstep4receivebidiresponsespanstep-4-receive-bidi-response"></a><span id="Step_4__Receive_Bidi_response"></span><span id="step_4__receive_bidi_response"></span><span id="STEP_4__RECEIVE_BIDI_RESPONSE"></span>步骤 4：接收 Bidi 响应


完成 Bidi"set"操作时，类型的回调对象， `PrinterBidiSetRequestCallback`，调用。 此回调负责处理的错误处理从 HRESULT 响应，然后触发`OnBidiResponseReceived`事件，发送 Bidi 响应通过事件参数。

此示例演示`PrinterBidiSetRequestCallback`类中的定义**DeviceMaintenance.xaml.cs**文件。

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

Bidi 响应然后发送到`OnBidiResponseReceived`方法，其中`Dispatcher`用于在 UI 线程上显示结果。

此示例摘自`OnBidiResponseReceived`方法**DeviceMaintenance.xaml.cs**文件。

```CSharp
internal async void OnBidiResponseReceived(object sender, string bidiResponse)
{
    await Dispatcher.RunAsync(Windows.UI.Core.CoreDispatcherPriority.Normal, () =>
    {
        BidiResponseOutput.Text = bidiResponse;
    });
}
```

## <a name="span-idtestingspanspan-idtestingspantesting"></a><span id="testing"></span><span id="TESTING"></span>测试


你可以测试 UWP 设备应用之前，它必须链接到您的打印机使用的设备元数据。

-   需要打印机的位置，若要向其中添加设备应用信息的设备元数据包的副本。 如果没有设备元数据，您可以使用生成它**设备元数据创建向导**主题中所述[创建 UWP 设备应用的设备元数据](https://go.microsoft.com/fwlink/p/?LinkId=313644)。

    **请注意**  若要使用**设备元数据创建向导**，则必须安装 Microsoft Visual Studio Professional，Microsoft Visual Studio Ultimate，或[独立 SDK 的 Windows 8.1](https://go.microsoft.com/fwlink/p/?linkid=309209)之前完成本主题中的步骤。 安装 Microsoft Visual Studio Express 的 Windows 安装不包括在向导的 sdk 版本。

     

以下步骤生成您的应用程序并安装设备元数据。

1.  启用测试签名。
    1.  启动**设备元数据创建向导**从 *%programfiles （x86） %* \\Windows 工具包\\8.1\\bin\\x86，通过双击**DeviceMetadataWizard.exe**
    2.  从**工具**菜单中，选择**启用测试签名**。

2.  重新启动计算机
3.  通过打开解决方案 (.sln) 文件生成解决方案。 按 F7，或转至**生成-&gt;生成解决方案**从顶部菜单中加载示例之后。

4.  断开连接并卸载打印机。 此步骤是必需的以便 Windows 将在下一次检测到设备读取更新的设备元数据。
5.  编辑并保存设备元数据。 要链接到你的设备的设备应用，必须将设备应用与你的设备进行关联。
    **请注意**  如果尚未创建设备元数据，请参阅[创建 UWP 设备应用的设备元数据](https://go.microsoft.com/fwlink/p/?LinkId=313644)。

     

    1.  如果**设备元数据创建向导**未打开，启动从 *%programfiles （x86） %* \\Windows 工具包\\8.1\\bin\\x86，也可由双击**DeviceMetadataWizard.exe**。
    2.  单击**编辑设备元数据**。 这样就可以编辑现有的设备元数据包。
    3.  在中**打开**对话框框中，找到与 UWP 设备应用程序相关联的设备元数据包。 (它具有**devicemetadata ms**文件扩展名。)
    4.  上**指定 UWP 设备应用信息**页上，输入中的 Microsoft Store 应用信息**UWP 设备应用**框。 单击**导入 UWP 应用程序清单文件**自动输入**包名称**，**发布服务器的名称**，以及**UWP 应用程序 ID**。
    5.  如果您的应用程序注册的打印机通知，填写**通知处理程序**框。 在中**事件 ID**，输入打印事件处理程序的名称。 在中**事件资产**，输入该代码所在的位置的文件的名称。

    6.  完成后，单击**下一步**直至到达**完成**页。
    7.  上**查看设备元数据包**页面上，确保所有设置都正确，然后选择**复制到本地计算机上的元数据存储设备元数据包**复选框。 然后单击**保存**。

6.  重新连接您的打印机，以便在设备连接时，该 Windows 读取更新的设备元数据。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[设备维护 （v4 打印机驱动程序）](https://docs.microsoft.com/windows-hardware/drivers/print/device-maintenance)

[开发 v4 打印驱动程序](https://go.microsoft.com/fwlink/p/?LinkId=314231)

[双向通信](https://go.microsoft.com/fwlink/p/?LinkId=317192)

[UWP 应用入门](getting-started.md)

[创建 UWP 设备应用程序 （分步指南）](step-1--create-a-uwp-device-app.md)

[创建设备元数据对 UWP 设备应用 （分步指南）](step-2--create-device-metadata.md)

 

 






