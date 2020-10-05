---
title: 如何在 UWP 设备应用中显示打印机状态
description: '本主题使用 "打印设置" 和 "打印通知" 示例的 c # 版本来演示如何查询打印机状态并显示该状态。'
ms.assetid: 91AD1B3B-0D0B-4FB6-8A0F-4943143D8FCE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dc5ebad4eb16539478b09a6e2e647b74c420eb1e
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91732921"
---
# <a name="how-to-display-printer-status-in-a-uwp-device-app"></a>如何在 UWP 设备应用中显示打印机状态


在 Windows 8.1 中，用户可以从 UWP 设备应用的新式 UI 检查其打印机状态。 本主题使用 " [打印设置" 和 "打印通知](https://go.microsoft.com/fwlink/p/?LinkID=242862) " 示例的 c # 版本来演示如何查询打印机状态并显示该状态。 若要详细了解 UWP 设备应用的详细信息，请参阅了解 [uwp 设备应用](meet-uwp-device-apps.md)。

C # 版本的 " [打印设置" 和 "打印通知](https://go.microsoft.com/fwlink/p/?LinkID=242862) " 示例使用 " **InkLevel** " 页演示如何 (在这种情况下，墨迹级别) 并显示打印机状态。 打印帮助程序类用于创建设备上下文 (IPrinterExtensionContext) 并执行设备查询。 **PrinterHelperClass.cs**文件在**DeviceAppForPrintersLibrary**项目中，并使用**PrinterExtensionLibrary**项目中定义的 api。 打印机扩展库提供了一种便捷的方式来访问 v4 打印驱动程序的打印机扩展接口。 有关详细信息，请参阅 [打印机扩展库概述](printer-extension-library-overview.md)。

**注意**   本主题中所示的代码示例基于 c # 版本的[打印设置和打印通知](https://go.microsoft.com/fwlink/p/?LinkID=242862)示例。 此示例在 JavaScript 和 c + + 中也可用。 请注意，由于 c + + 可以直接访问 COM，因此该示例的 c + + 版本不包括代码库项目。 下载示例以查看最新版本的代码。

 

## <a name="span-idprerequisitesspanspan-idprerequisitesspanspan-idprerequisitesspanprerequisites"></a><span id="Prerequisites"></span><span id="prerequisites"></span><span id="PREREQUISITES"></span>先决条件


准备工作：

1.  请确保您的打印机是使用 v4 打印驱动程序安装的。 有关详细信息，请参阅 [开发 v4 打印驱动程序](../print/v4-printer-driver.md)。
2.  设置开发 PC。 有关下载工具和创建开发人员帐户的信息[，请参阅入门。](getting-started.md)
3.  将应用与应用商店相关联。 请参阅 [步骤1：创建 UWP 设备应用](step-1--create-a-uwp-device-app.md) 了解相关信息。
4.  为打印机创建将其与应用程序关联的设备元数据。 有关详细信息，请参阅 [步骤2：创建设备元数据](step-2--create-device-metadata.md) 。
5.  如果正在编写的是用 c # 或 JavaScript 编写应用，请将 **PrinterExtensionLibrary** 和 **DeviceAppForPrintersLibrary** 项目添加到 UWP 设备应用解决方案。 可以在 " [打印设置" 和 "打印通知](https://go.microsoft.com/fwlink/p/?LinkID=242862) " 示例中找到这些项目。
    **注意**   由于 c + + 可以直接访问 COM，因此，c + + 应用不需要单独的库即可使用基于 COM 的打印机设备上下文。

     

## <a name="span-idstep_1__find_the_printerspanspan-idstep_1__find_the_printerspanspan-idstep_1__find_the_printerspanstep-1-find-the-printer"></a><span id="Step_1__Find_the_printer"></span><span id="step_1__find_the_printer"></span><span id="STEP_1__FIND_THE_PRINTER"></span>步骤1：查找打印机


在可以创建设备上下文之前，应用需要确定打印机的设备 ID。 为此，该示例使用 `EnumerateAssociatedPrinters` 方法来搜索附加到电脑的所有打印机。 然后，它会检查每个打印机的容器，并通过比较每个容器的 PackageFamilyName 属性来查找关联。

**注意**   与应用关联的设备的 AppPackageFamilyName 可以在 Microsoft Visual Studio 中的清单设计器的 "**打包**" 选项卡下找到。

 

此示例显示了 `EnumerateAssociatedPrinters` **InkLevel.xaml.cs** 文件中的方法：

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

`FindAssociation`方法（由调用 `EnumerateAssociatedPrinters` ）检查打印机是否与当前应用程序关联。 换句话说，此方法检查应用是否为 UWP 设备应用。 当在本地 PC 上的设备元数据中定义了应用和打印机时，就存在此关联。

此示例显示了 `FindAssociation` **InkLevel.xaml.cs** 文件中的方法：

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

找到关联时， `FindAssociation` 方法使用 `AddToList` 方法将设备 id 添加到关联的设备 id 列表。 这些 Id 存储在名为的组合框中 `AssociatedPrinters` 。

此示例显示了 `AddToList` **InkLevel.xaml.cs** 文件中的方法：

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

## <a name="span-idstep_2__display_the_statusspanspan-idstep_2__display_the_statusspanspan-idstep_2__display_the_statusspanstep-2-display-the-status"></a><span id="Step_2__Display_the_status"></span><span id="step_2__display_the_status"></span><span id="STEP_2__DISPLAY_THE_STATUS"></span>步骤2：显示状态


`GetInkStatus`方法使用基于事件的异步模式来请求打印机的信息。 此方法使用关联的设备 ID 来获取可用于获取设备状态的设备上下文。 对方法的调用将 `printHelper.SendInkLevelQuery()` 启动设备查询。 当响应返回时，将 `OnInkLevelReceived` 调用方法并更新 UI。

**注意**   此 c # 示例遵循的模式与 JavaScript 示例不同，因为 c # 允许向 PrintHelperClass 发送调度程序，以便它可以将事件消息回发到 UI 线程。

 

此示例显示了 `GetInkStatus` `OnInkLevelReceived` **InkLevel.xaml.cs** 文件中的和方法：

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

Print helper 类负责向设备发送双向查询并接收响应。

此示例显示了 `SendInkLevelQuery` **PrintHelperClass.cs** 文件中的方法和其他方法。 请注意，此处只显示某些打印帮助程序类方法。 下载 " [打印设置" 和 "打印通知](https://go.microsoft.com/fwlink/p/?LinkID=242862) " 示例以查看完整代码。

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


在可以测试 UWP 设备应用之前，必须使用设备元数据将其链接到您的打印机。

-   你需要打印机的设备元数据包的副本，以便向其添加设备应用信息。 如果没有设备元数据，可以使用 **设备元数据创作向导** 生成它，如 " [步骤2：创建 UWP 设备的设备元数据](./step-2--create-device-metadata.md)" 主题中所述。

    **注意**   若要使用**设备元数据创作向导**，在完成本主题中的步骤之前，必须安装 Microsoft Visual Studio Professional、Microsoft Visual Studio Ultimate 或[独立的 SDK for Windows 8.1](https://go.microsoft.com/fwlink/p/?linkid=309209)。 为 Windows 安装 Microsoft Visual Studio Express 会安装不包括向导的 SDK 版本。

     

以下步骤生成应用并安装设备元数据。

1.  启用测试签名。
    1.  双击 "DeviceMetadataWizard.exe，从 *% ProgramFiles (x86) %* Windows 工具包 8.1 bin **X86 启动设备元数据创作向导** \\ \\ \\ \\ **DeviceMetadataWizard.exe**
    2.  从 " **工具** " 菜单中，选择 " **启用测试签名**"。

2.  重新启动计算机
3.  通过打开解决方案 ( .sln) 文件来生成解决方案。 加载示例后，按 F7 或从顶部菜单中转到 " **生成- &gt; 生成解决方案** "。

4.  断开连接并卸载打印机。 此步骤是必需的，以便 Windows 将在下一次检测到设备时读取更新的设备元数据。
5.  编辑并保存设备元数据。 若要将设备应用链接到设备，你必须将设备应用关联到设备。
    **注意**   如果尚未创建设备元数据，请参阅[步骤2：创建 UWP 设备应用的设备元数据](./step-2--create-device-metadata.md)。

     

    1.  如果**设备元数据创作向导**尚未打开，请通过双击 "DeviceMetadataWizard.exe" 从 *% ProgramFiles (x86) %* \\ Windows 工具包 \\ 8.1 \\ bin \\ x86 **DeviceMetadataWizard.exe**启动它。
    2.  单击 " **编辑设备元数据**"。 这将允许你编辑现有的设备元数据包。
    3.  在 " **打开** " 对话框中，找到与 UWP 设备应用关联的设备元数据包。  (其文件扩展名为 **devicemetadata** 。 ) 
    4.  在 " **指定 uwp 设备应用信息** " 页上，在 " **UWP 设备应用** " 框中输入 Microsoft Store 应用信息。 单击 " **导入 UWP 应用程序清单文件** " 以自动输入 **包名称**、 **发布者名称**和 **UWP 应用 ID**。
    5.  如果你的应用正在注册打印机通知，请填写 **通知处理程序** 框。 在 " **事件 ID**" 中，输入打印事件处理程序的名称。 在 " **事件资产**" 中，输入代码所在的文件的名称。

    6.  完成后，单击 " **下一步** "，直到到达 " **完成** " 页。
    7.  在 " **查看设备元数据包** " 页上，确保所有设置均正确，并选中 "将 **设备元数据包复制到本地计算机上的元数据存储区** " 复选框。 然后单击“保存”  。

6.  重新连接打印机，以便 Windows 在连接设备时读取更新的设备元数据。

## <a name="span-idtroubleshootingspanspan-idtroubleshootingspanspan-idtroubleshootingspantroubleshooting"></a><span id="Troubleshooting"></span><span id="troubleshooting"></span><span id="TROUBLESHOOTING"></span>故障排除


### <a name="span-idissue__can_t_find_printer_when_enumerating_devices_associated_with_the_appspanspan-idissue__can_t_find_printer_when_enumerating_devices_associated_with_the_appspanspan-idissue__can_t_find_printer_when_enumerating_devices_associated_with_the_appspanissue-cant-find-printer-when-enumerating-devices-associated-with-the-app"></a><span id="Issue__Can_t_find_printer_when_enumerating_devices_associated_with_the_app"></span><span id="issue__can_t_find_printer_when_enumerating_devices_associated_with_the_app"></span><span id="ISSUE__CAN_T_FIND_PRINTER_WHEN_ENUMERATING_DEVICES_ASSOCIATED_WITH_THE_APP"></span>问题：枚举与应用关联的设备时找不到打印机

如果在枚举关联的打印机时找不到打印机 .。。

-   **可能的原因：** 未启用测试签名。 请参阅本主题中的调试部分，了解有关如何打开它的信息。

-   **可能的原因：** 应用未查询正确的包系列名称。 在代码中检查包系列名称。 在 Microsoft Visual Studio 中打开 **appxmanifest.xml** ，并确保要查询的包系列名称与 " **打包** " 选项卡上的 "包系列名称" 字段中的相同。

-   **可能的原因：** 设备元数据不与包系列名称关联。 使用 **设备元数据创作向导** 打开设备元数据，并检查包系列名称。 双击DeviceMetadataWizard.exe，从 *% ProgramFiles (x86) %* \\ Windows 工具包 \\ 8.1 \\ bin \\ x86 **DeviceMetadataWizard.exe**启动向导。

### <a name="span-idissue__found_printer_associated_with_the_app__but_can_t_query_bidi_infospanspan-idissue__found_printer_associated_with_the_app__but_can_t_query_bidi_infospanspan-idissue__found_printer_associated_with_the_app__but_can_t_query_bidi_infospanissue-found-printer-associated-with-the-app-but-cant-query-bidi-info"></a><span id="Issue__Found_printer_associated_with_the_app__but_can_t_query_Bidi_info"></span><span id="issue__found_printer_associated_with_the_app__but_can_t_query_bidi_info"></span><span id="ISSUE__FOUND_PRINTER_ASSOCIATED_WITH_THE_APP__BUT_CAN_T_QUERY_BIDI_INFO"></span>问题：找到了与应用关联的打印机，但无法查询双向信息

如果在枚举关联的打印机时找到了您的打印机，但双向查询返回错误 .。。

-   **可能的原因：** 包系列名称错误。 在代码中检查包系列名称。 在 Visual Studio 中打开 **appxmanifest.xml** ，并确保要查询的包系列名称与 " **打包** " 选项卡上的 "包系列名称" 字段中的相同。

-   **可能的原因：** 使用 v3 打印机（而不是 v4 打印机）安装打印机。 若要查看安装的版本，请打开 PowerShell，然后键入以下命令：

    ```PowerShell
    get-printer | Select Name, {(get-printerdriver -Name $_.DriverName).MajorVersion}
    ```

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[开发 v4 打印驱动程序](../print/v4-printer-driver.md)

[ (v4 打印驱动程序的打印机扩展接口) ](/windows-hardware/drivers/ddi/_print/)

[双向通信](../print/bidirectional-communication.md)

[UWP 应用入门](getting-started.md)

[ (分步指南创建 UWP 设备应用) ](step-1--create-a-uwp-device-app.md)

[ (分步指南创建 UWP 设备应用的设备元数据) ](step-2--create-device-metadata.md)

 

