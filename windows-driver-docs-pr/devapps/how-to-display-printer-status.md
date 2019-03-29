---
title: 如何在 UWP 设备应用中显示打印机状态
description: 本主题使用C#版本的打印设置和打印通知示例来演示如何进行查询的打印机状态并将其显示。
ms.assetid: 91AD1B3B-0D0B-4FB6-8A0F-4943143D8FCE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b8770e6e44f9433c009bcac80e5b26c2e13d1b76
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57350350"
---
# <a name="how-to-display-printer-status-in-a-uwp-device-app"></a>如何在 UWP 设备应用中显示打印机状态


在 Windows 8.1，用户可以查看从 UWP 设备应用的现代 UI 其打印机状态。 本主题使用C#的版本[打印设置和打印通知](https://go.microsoft.com/fwlink/p/?LinkID=242862)示例，用于演示如何查询打印机状态并将其显示。 若要在一般情况下了解有关 UWP 的设备应用程序的详细信息，请参阅[满足 UWP 设备应用](meet-uwp-device-apps.md)。

C#的版本[打印设置和打印通知](https://go.microsoft.com/fwlink/p/?LinkID=242862)的示例使用**InkLevel.xaml**页后，可以演示如何获取打印机状态 （在此情况下，墨迹级别） 并将其显示。 打印帮助器类用于创建设备上下文 (IPrinterExtensionContext)，并执行设备查询。 **PrinterHelperClass.cs**文件位于**DeviceAppForPrintersLibrary**项目，然后使用 Api 中定义**PrinterExtensionLibrary**项目。 打印机扩展库提供了方便地访问 v4 打印驱动程序的打印机扩展插件接口。 有关详细信息，请参阅[打印机扩展库概述](printer-extension-library-overview.md)。

**请注意**  本主题中所示的代码示例基于C#的版本[打印设置和打印通知](https://go.microsoft.com/fwlink/p/?LinkID=242862)示例。 此示例也是在 JavaScript 和 c + + 中可用。 请注意由于 c + + 可以直接访问 COM，该示例的 c + + 版本不包括代码库项目。 下载示例，请参阅最新版本的代码。

 

## <a name="span-idprerequisitesspanspan-idprerequisitesspanspan-idprerequisitesspanprerequisites"></a><span id="Prerequisites"></span><span id="prerequisites"></span><span id="PREREQUISITES"></span>先决条件


开始之前：

1.  请确保使用 v4 打印驱动程序安装您的打印机。 有关详细信息，请参阅[开发 v4 打印驱动程序](https://go.microsoft.com/fwlink/p/?LinkId=314231)。
2.  获取对开发计算机设置。 请参阅[入门](getting-started.md)有关下载工具和创建开发人员帐户信息。
3.  将你的应用与应用商店相关联。 请参阅本主题中的[步骤 1：创建 UWP 设备应用](step-1--create-a-uwp-device-app.md)有关的信息。
4.  创建设备元数据为您将其与您的应用程序关联的打印机。 请参阅[步骤 2:创建设备元数据](step-2--create-device-metadata.md)有关的详细信息。
5.  如果您正在编写您编写的应用程序与C#或 JavaScript 中，添加**PrinterExtensionLibrary**并**DeviceAppForPrintersLibrary**到您 UWP 设备应用程序解决方案的项目。 您可以找到这些项目中的每个[打印设置和打印通知](https://go.microsoft.com/fwlink/p/?LinkID=242862)示例。
    **请注意**  因为 c + + 可以直接访问 COM，c + + 应用程序不需要单独的库以使用基于 COM 的打印机设备上下文。

     

## <a name="span-idstep1findtheprinterspanspan-idstep1findtheprinterspanspan-idstep1findtheprinterspanstep-1-find-the-printer"></a><span id="Step_1__Find_the_printer"></span><span id="step_1__find_the_printer"></span><span id="STEP_1__FIND_THE_PRINTER"></span>步骤 1：查找打印机


可以创建设备上下文之前，应用程序需要确定打印机的设备 ID。 若要执行此操作，该示例使用`EnumerateAssociatedPrinters`方法搜索通过连接到 PC 的所有打印机。 然后它会检查每个打印机的容器，并通过比较每个容器 PackageFamilyName 属性查找的关联。

**请注意**  可以下找到与您的应用程序相关联的设备的 System.Devices.AppPackageFamilyName**打包**在清单设计器在 Microsoft Visual Studio 中的选项卡。

 

此示例演示`EnumerateAssociatedPrinters`方法从**InkLevel.xaml.cs**文件：

```CSharp
async void EnumerateAssociatedPrinters(object sender, RoutedEventArgs e)
{
    // Reset output text and associated printer array.
    AssociatedPrinters.Items.Clear();
    BidiOutput.Text = "";

    // GUID string for printers.
    string printerInterfaceClass = "{0ecef634-6ef0-472a-8085-5ad023ecbccd}";
    string selector = "System.Devices.InterfaceClassGuid:=\"" + printerInterfaceClass + "\"";

    // By default, FindAllAsync does not return the containerId for the device it queries.
    // We have to add it as an additonal property to retrieve. 
    string containerIdField = "System.Devices.ContainerId";
    string[] propertiesToRetrieve = new string[] { containerIdField };

    // Asynchronously find all printer devices.
    DeviceInformationCollection deviceInfoCollection = await DeviceInformation.FindAllAsync(selector, propertiesToRetrieve);

    // For each printer device returned, check if it is associated with the current app.
    for (int i = 0; i < deviceInfoCollection.Count; i++)
    {
        DeviceInformation deviceInfo = deviceInfoCollection[i];
        FindAssociation(deviceInfo, deviceInfo.Properties[containerIdField].ToString());
    }
}
```

`FindAssociation`调用的方法`EnumerateAssociatedPrinters`，检查打印机是否与当前应用程序相关联。 换而言之，此方法检查该应用程序是否 UWP 设备应用。 在本地 PC 上的设备元数据中定义的应用程序和打印机时存在此关联。

此示例演示`FindAssociation`方法从**InkLevel.xaml.cs**文件：

```CSharp
async void FindAssociation(DeviceInformation deviceInfo, string containerId)
{

    // Specifically telling CreateFromIdAsync to retrieve the AppPackageFamilyName. 
    string packageFamilyName = "System.Devices.AppPackageFamilyName";
    string[] containerPropertiesToGet = new string[] { packageFamilyName };

    // CreateFromIdAsync needs braces on the containerId string.
    string containerIdwithBraces = "{" + containerId + "}";

    // Asynchoronously getting the container information of the printer.
    PnpObject containerInfo = await PnpObject.CreateFromIdAsync(PnpObjectType.DeviceContainer, containerIdwithBraces, containerPropertiesToGet);

    // Printers could be associated with other device apps, only the ones with package family name
    // matching this app's is associated with this app. The packageFamilyName for this app will be found in this app's packagemanifest
    string appPackageFamilyName = "Microsoft.SDKSamples.DeviceAppForPrinters.CS_8wekyb3d8bbwe";
    var prop = containerInfo.Properties;

    // If the packageFamilyName of the printer container matches the one for this app, the printer is associated with this app.
    string[] packageFamilyNameList = (string[])prop[packageFamilyName];
    if (packageFamilyNameList != null)
    {
        for (int j = 0; j < packageFamilyNameList.Length; j++)
        {
            if (packageFamilyNameList[j].Equals(appPackageFamilyName))
            {
                AddToList(deviceInfo);
            }
        }
    }
}
```

当找到关联时，`FindAssociation`方法使用`AddToList`方法将设备 ID 添加到一组相关联的设备 Id。 这些 Id 存储在名为一个组合框`AssociatedPrinters`。

此示例演示`AddToList`方法从**InkLevel.xaml.cs**文件：

```CSharp
void AddToList(DeviceInformation deviceInfo)
{
    // Creating a new display item so the user sees the friendly name instead of the interfaceId.
    ComboBoxItem item = new ComboBoxItem();
    item.Content = deviceInfo.Properties["System.ItemNameDisplay"] as string;
    item.DataContext = deviceInfo.Id;
    AssociatedPrinters.Items.Add(item);

    // If this is the first printer to be added to the combo box, select it.
    if (AssociatedPrinters.Items.Count == 1)
    {
        AssociatedPrinters.SelectedIndex = 0;
    }
}
```

## <a name="span-idstep2displaythestatusspanspan-idstep2displaythestatusspanspan-idstep2displaythestatusspanstep-2-display-the-status"></a><span id="Step_2__Display_the_status"></span><span id="step_2__display_the_status"></span><span id="STEP_2__DISPLAY_THE_STATUS"></span>步骤 2：显示的状态


`GetInkStatus`方法使用异步基于事件的模式以请求信息从打印机。 此方法使用关联的设备 ID 以获取可用于获取设备状态的设备上下文。 对调用`printHelper.SendInkLevelQuery()`方法启动设备查询。 当响应返回时，则`OnInkLevelReceived`调用方法和 UI 更新。

**请注意**  此C#示例遵循比 JavaScript 示例中，不同的模式，因为C#可让你需要将调度程序发送到 PrintHelperClass，以便它可以发送到 UI 线程上的事件消息。

 

此示例演示`GetInkStatus`并`OnInkLevelReceived`方法从**InkLevel.xaml.cs**文件：

```CSharp
void GetInkStatus(object sender, RoutedEventArgs e)
{
    if (AssociatedPrinters.Items.Count > 0)
    {
        // Get the printer that the user has selected to query.
        ComboBoxItem selectedItem = AssociatedPrinters.SelectedItem as ComboBoxItem;

        // The interfaceId is retrieved from the detail field.
        string interfaceId = selectedItem.DataContext as string;

        try
        {
            // Unsubscribe existing ink level event handler, if any.
            if (printHelper != null)
            {
                printHelper.OnInkLevelReceived -= OnInkLevelReceived;
                printHelper = null;
            }

            object context = Windows.Devices.Printers.Extensions.PrintExtensionContext.FromDeviceId(interfaceId);printHelper.SendInkLevelQuery()

            // Use the PrinterHelperClass to retrieve the bidi data and display it.
            printHelper = new PrintHelperClass(context);
            try
            {
                printHelper.OnInkLevelReceived += OnInkLevelReceived;
                printHelper.SendInkLevelQuery();

                rootPage.NotifyUser("Ink level query successful", NotifyType.StatusMessage);
            }
            catch (Exception)
            {
                rootPage.NotifyUser("Ink level query unsuccessful", NotifyType.ErrorMessage);
            }
        }
        catch (Exception)
        {
            rootPage.NotifyUser("Error retrieving PrinterExtensionContext from InterfaceId", NotifyType.ErrorMessage);
        }
    }
}

private void OnInkLevelReceived(object sender, string response)
{
    BidiOutput.Text = response;
}
```

打印帮助器类负责将 Bidi 查询发送到设备和接收响应。

此示例演示`SendInkLevelQuery`方法和其他人，从**PrintHelperClass.cs**文件。 请注意，只有一部分打印帮助器类方法如下所示。 下载[打印设置和打印通知](https://go.microsoft.com/fwlink/p/?LinkID=242862)示例，请参阅完整代码。

```CSharp
public void SendInkLevelQuery()
{
    printerQueue.OnBidiResponseReceived += OnBidiResponseReceived;

    // Send the query.
    string queryString = "\\Printer.Consumables";
    printerQueue.SendBidiQuery(queryString);
}

private void OnBidiResponseReceived(object sender, PrinterQueueEventArgs responseArguments)
{
    // Invoke the ink level event with appropriate data.
    dispatcher.RunAsync(
        Windows.UI.Core.CoreDispatcherPriority.Normal,
        () =>
        {
            OnInkLevelReceived(sender, ParseResponse(responseArguments));
        });
}

private string ParseResponse(PrinterQueueEventArgs responseArguments)
{
    if (responseArguments.StatusHResult == (int)HRESULT.S_OK)
        return responseArguments.Response;
    else
        return InvalidHResult(responseArguments.StatusHResult);
}

private string InvalidHResult(int result)
{
    switch (result)
    {
        case unchecked((int)HRESULT.E_INVALIDARG):
            return "Invalid Arguments";
        case unchecked((int)HRESULT.E_OUTOFMEMORY):
            return "Out of Memory";
        case unchecked((int)HRESULT.ERROR_NOT_FOUND):
            return "Not found";
        case (int)HRESULT.S_FALSE:
            return "False";
        case (int)HRESULT.S_PT_NO_CONFLICT:
            return "PT No Conflict";
        default:
            return "Undefined status: 0x" + result.ToString("X");
    }
}
```

## <a name="span-idtestingspanspan-idtestingspanspan-idtestingspantesting"></a><span id="Testing"></span><span id="testing"></span><span id="TESTING"></span>测试


你可以测试 UWP 设备应用之前，它必须链接到您的打印机使用的设备元数据。

-   需要打印机的位置，若要向其中添加设备应用信息的设备元数据包的副本。 如果没有设备元数据，您可以使用生成它**设备元数据创建向导**主题中所述[步骤 2:创建 UWP 设备应用的设备元数据](https://go.microsoft.com/fwlink/p/?LinkId=313644)。

    **请注意**  若要使用**设备元数据创建向导**，则必须安装 Microsoft Visual Studio Professional，Microsoft Visual Studio Ultimate，或[独立 SDK 的 Windows 8.1](https://go.microsoft.com/fwlink/p/?linkid=309209)之前完成本主题中的步骤。 安装 Microsoft Visual Studio Express 的 Windows 安装不包括在向导的 sdk 版本。

     

以下步骤生成您的应用程序并安装设备元数据。

1.  启用测试签名。
    1.  启动**设备元数据创建向导**从 *%programfiles （x86） %*\\Windows 工具包\\8.1\\bin\\x86，通过双击**DeviceMetadataWizard.exe**
    2.  从**工具**菜单中，选择**启用测试签名**。

2.  重新启动计算机
3.  通过打开解决方案 (.sln) 文件生成解决方案。 按 F7，或转至**生成-&gt;生成解决方案**从顶部菜单中加载示例之后。

4.  断开连接并卸载打印机。 此步骤是必需的以便 Windows 将在下一次检测到设备读取更新的设备元数据。
5.  编辑并保存设备元数据。 要链接到你的设备的设备应用，必须将设备应用与你的设备进行关联。
    **请注意**  如果尚未创建设备元数据，请参阅[步骤 2:创建 UWP 设备应用的设备元数据](https://go.microsoft.com/fwlink/p/?LinkId=313644)。

     

    1.  如果**设备元数据创建向导**未打开，启动从 *%programfiles （x86） %*\\Windows 工具包\\8.1\\bin\\x86，也可由双击**DeviceMetadataWizard.exe**。
    2.  单击**编辑设备元数据**。 这样就可以编辑现有的设备元数据包。
    3.  在中**打开**对话框框中，找到与 UWP 设备应用程序相关联的设备元数据包。 (它具有**devicemetadata ms**文件扩展名。)
    4.  上**指定 UWP 设备应用信息**页上，输入中的 Microsoft Store 应用信息**UWP 设备应用**框。 单击**导入 UWP 应用程序清单文件**自动输入**包名称**，**发布服务器的名称**，以及**UWP 应用程序 ID**。
    5.  如果您的应用程序注册的打印机通知，填写**通知处理程序**框。 在中**事件 ID**，输入打印事件处理程序的名称。 在中**事件资产**，输入该代码所在的位置的文件的名称。

    6.  完成后，单击**下一步**直至到达**完成**页。
    7.  上**查看设备元数据包**页面上，确保所有设置都正确，然后选择**复制到本地计算机上的元数据存储设备元数据包**复选框。 然后单击**保存**。

6.  重新连接您的打印机，以便在设备连接时，该 Windows 读取更新的设备元数据。

## <a name="span-idtroubleshootingspanspan-idtroubleshootingspanspan-idtroubleshootingspantroubleshooting"></a><span id="Troubleshooting"></span><span id="troubleshooting"></span><span id="TROUBLESHOOTING"></span>故障排除


### <a name="span-idissuecantfindprinterwhenenumeratingdevicesassociatedwiththeappspanspan-idissuecantfindprinterwhenenumeratingdevicesassociatedwiththeappspanspan-idissuecantfindprinterwhenenumeratingdevicesassociatedwiththeappspanissue-cant-find-printer-when-enumerating-devices-associated-with-the-app"></a><span id="Issue__Can_t_find_printer_when_enumerating_devices_associated_with_the_app"></span><span id="issue__can_t_find_printer_when_enumerating_devices_associated_with_the_app"></span><span id="ISSUE__CAN_T_FIND_PRINTER_WHEN_ENUMERATING_DEVICES_ASSOCIATED_WITH_THE_APP"></span>问题：枚举与应用关联的设备时找不到打印机

如果您的打印机枚举关联的打印机时找不到...

-   **可能的原因：** 未打开测试签名。 请参阅本主题了解如何将其打开的调试部分。

-   **可能的原因：** 应用程序不查询的正确包系列名称。 检查你的代码中的包系列名称。 打开**package.appxmanifest** Microsoft Visual Studio 并确保在包系列名称要查询的匹配中的一个**打包**选项卡上，包系列名称字段中的。

-   **可能的原因：** 设备元数据所关联的包系列名称。 使用**设备元数据创建向导**要打开设备元数据并检查包系列名称。 从启动该向导 *%programfiles （x86） %*\\Windows 工具包\\8.1\\bin\\x86，通过双击**DeviceMetadataWizard.exe**。

### <a name="span-idissuefoundprinterassociatedwiththeappbutcantquerybidiinfospanspan-idissuefoundprinterassociatedwiththeappbutcantquerybidiinfospanspan-idissuefoundprinterassociatedwiththeappbutcantquerybidiinfospanissue-found-printer-associated-with-the-app-but-cant-query-bidi-info"></a><span id="Issue__Found_printer_associated_with_the_app__but_can_t_query_Bidi_info"></span><span id="issue__found_printer_associated_with_the_app__but_can_t_query_bidi_info"></span><span id="ISSUE__FOUND_PRINTER_ASSOCIATED_WITH_THE_APP__BUT_CAN_T_QUERY_BIDI_INFO"></span>问题：找到与应用关联的打印机，但不能查询 Bidi 信息

如果找到了您的打印机时枚举关联的打印机，但 Bidi 查询将返回错误...

-   **可能的原因：** 错误的包系列名称。 检查你的代码中的包系列名称。 打开**package.appxmanifest**在 Visual Studio 并确保包系列名称要查询的匹配中的一个**打包**选项卡上，包系列名称字段中的。

-   **可能的原因：** 使用 v3 打印机，而不是 v4 打印机安装打印机。 若要查看安装的版本，请打开 PowerShell 并键入以下命令：

    ```PowerShell
    get-printer | Select Name, {(get-printerdriver -Name $_.DriverName).MajorVersion}
    ```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[开发 v4 打印驱动程序](https://go.microsoft.com/fwlink/p/?LinkId=314231)

[打印机扩展插件接口 （v4 打印驱动程序）](https://go.microsoft.com/fwlink/p/?LinkID=299887)

[双向通信](https://go.microsoft.com/fwlink/p/?LinkId=317192)

[UWP 应用入门](getting-started.md)

[创建 UWP 设备应用程序 （分步指南）](step-1--create-a-uwp-device-app.md)

[创建设备元数据对 UWP 设备应用 （分步指南）](step-2--create-device-metadata.md)

 

 






