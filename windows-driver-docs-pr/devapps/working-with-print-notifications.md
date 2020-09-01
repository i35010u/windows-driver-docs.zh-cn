---
title: 在 UWP 设备应用中使用打印通知
description: '本主题介绍打印通知，并演示 c # 版本的打印设置和打印通知示例如何使用后台任务来响应打印通知。'
ms.assetid: 39A06A8A-5603-44AB-8884-C12B8E2F1A45
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 094815c1d939061a81d60553ea6ee6f71af233ee
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89097183"
---
# <a name="working-with-print-notifications-in-a-uwp-device-app"></a>在 UWP 设备应用中使用打印通知

在 Windows 8.1 中，UWP 设备应用可以响应从 v4 打印驱动程序发送的双向通信 (双向通信) 事件。 本主题介绍打印通知，并演示 c # 版本的 [打印设置和打印通知](https://go.microsoft.com/fwlink/p/?LinkID=242862) 示例如何使用后台任务来响应打印通知。 后台任务演示了如何将通知详细信息保存在本地应用程序数据存储区中，发送 toast 并更新磁贴和徽章。 若要详细了解 UWP 设备应用的详细信息，请参阅了解 [uwp 设备应用](meet-uwp-device-apps.md)。

"[打印设置" 和 "打印通知](https://go.microsoft.com/fwlink/p/?LinkID=242862)" 示例的 c # 版本演示了**BackgroundTask**项目中*后台任务*) 的 (应用的背景部分。 后台任务的代码位于 **PrintBackgroundTask.cs** 文件中。 *前台应用*（可从开始启动的全屏应用）位于**DeviceAppForPrinters**项目中。 **InkLevel.xaml.cs**文件显示了一种可从前台应用程序访问通知详细信息的方法。 若要使用打印通知，示例将在 **PrinterExtensionLibrary** 项目中使用打印机扩展库。 打印机扩展库提供了一种便捷的方式来访问 v4 打印驱动程序的打印机扩展接口。 有关详细信息，请参阅 [打印机扩展库概述](printer-extension-library-overview.md)。

>[!NOTE]
>本主题中所示的代码示例基于 c # 版本的 [打印设置和打印通知](https://go.microsoft.com/fwlink/p/?LinkID=242862) 示例。 此示例在 JavaScript 和 c + + 中也可用。 请注意，由于 c + + 可以直接访问 COM，因此该示例的 c + + 版本不包括代码库项目。 下载示例以查看最新版本的代码。

## <a name="print-notifications"></a>打印通知

打印通知让 UWP 设备应用在打印时通知用户重要的打印机事件，例如卡纸、打开打印机门、墨水不足或打印机缺纸错误。 当打印机触发通知时，系统事件代理会运行应用的后台任务。 后台任务可保存通知详细信息、发送 toast、更新磁贴、更新徽章或不执行任何操作。 通过保存通知详细信息，你的应用程序可以提供一种体验，帮助用户了解和修复其打印机问题。

>[!NOTE]
>打印机制造商必须在其 v4 打印驱动程序中实现双向和 DriverEvent XML 文件，才能在其 UWP 设备应用中使用打印通知。 有关详细信息，请参阅 [双向通信](https://go.microsoft.com/fwlink/p/?LinkId=317192)。

如果发生 DriverEvent，并启动了 UWP 设备应用的后台任务，则该应用具有几个选项来执行此操作。 有关导致任务启动的流的更多详细信息，请参阅 [自定义 UI 的驱动程序支持](../print/driver-support-for-customized-ui.md)。

后台任务可以选择：

- 不执行任何操作
- 将通知详细信息保存到 [本地应用数据存储](https://go.microsoft.com/fwlink/p/?LinkId=317216)
- 更新 [UWP 应用磁贴通知](https://go.microsoft.com/fwlink/p/?LinkId=317195)
- 更新 [UWP 应用通知徽章](https://go.microsoft.com/fwlink/p/?LinkId=317196)
- 发送 [UWP 应用 toast 通知](https://go.microsoft.com/fwlink/p/?LinkId=317197)

磁贴通知或 toast 通知可以让用户方便地启动前景应用。 启动前台应用时，它可以使用 `OnLaunched` **App.xaml.cs** 中的方法来检查磁贴或 toast 是否已启动。 如果是，则前景应用可以访问 [本地应用程序数据存储](https://go.microsoft.com/fwlink/p/?LinkId=317216)中的任何打印通知详细信息。

## <a name="prerequisites"></a>先决条件

准备工作：

1. 请确保您的打印机是使用 v4 打印驱动程序安装的。 有关详细信息，请参阅 [开发 v4 打印驱动程序](https://go.microsoft.com/fwlink/p/?LinkId=314231)。
2. 设置开发 PC。 有关下载工具和创建开发人员帐户的信息[，请参阅入门。](getting-started.md)
3. 将应用与应用商店相关联。 请参阅 [创建 UWP 设备应用](step-1--create-a-uwp-device-app.md) 了解相关信息。
4. 为打印机创建将其与应用程序关联的设备元数据。 有关详细信息，请参阅 [创建设备元数据](step-2--create-device-metadata.md) 。
5. 构建应用程序主页的 UI。 所有 UWP 设备应用都可以从 "开始" 启动，它们将全屏显示。 使用 "开始体验" 以与设备的特定品牌和功能匹配的方式突出显示你的产品或服务。 它可以使用的 UI 控件类型没有任何特殊限制。 若要开始设计全屏体验，请参阅 [Microsoft Store 设计原则](https://go.microsoft.com/fwlink/p/?LinkID=299845)。
6. 如果正在编写的是用 c # 或 JavaScript 编写应用，请将 **PrinterExtensionLibrary** 和 **DeviceAppForPrintersLibrary** 项目添加到 UWP 设备应用解决方案。 可以在 " [打印设置" 和 "打印通知](https://go.microsoft.com/fwlink/p/?LinkID=242862) " 示例中找到这些项目。

>[!NOTE]
>由于 c + + 可以直接访问 COM，因此，c + + 应用不需要单独的库即可使用基于 COM 的打印机设备上下文。

## <a name="step-1-register-background-task"></a>步骤1：注册后台任务

为了使 Windows 能够识别应用程序可以处理打印通知，它必须注册打印通知的后台任务扩展。 此扩展在元素中声明 `Extension` ， `Category` 并将特性设置为， `windows.backgroundTasks` 并将 `EntryPoint` 特性设置为 `BackgroundTask.PrintBackgroundTask` 。 该扩展插件还包括一个 `Task` 元素，用于指示它支持 `systemEvent` 任务类型。

可以在 Microsoft Visual Studio 中的清单设计器的 " **声明** " 选项卡上添加 "打印后台任务" 扩展。 你还可以使用 XML (文本) 编辑器手动编辑应用包清单 XML。 右键单击**解决方案资源管理器**中的**appxmanifest.xml**文件以编辑选项。

此示例显示元素中的后台任务扩展 `Extension` ，因为它显示在应用包清单文件 **appxmanifest.xml**中。

```XML
<?xml version="1.0" encoding="utf-8"?>
<Package xmlns="http://schemas.microsoft.com/appx/2010/manifest">
  <Identity Name="Microsoft.SDKSamples.DeviceAppForPrinters.CS" Publisher="CN=Microsoft Corporation, O=Microsoft Corporation, L=Redmond, S=Washington, C=US" Version="1.0.0.0" />
  <Properties>
    <DisplayName>Device App For Printers C# sample</DisplayName>
    <PublisherDisplayName>Microsoft Corporation</PublisherDisplayName>
    <Logo>Assets\storeLogo-sdk.png</Logo>
  </Properties>
  <Prerequisites>
    <OSMinVersion>6.3.0</OSMinVersion>
    <OSMaxVersionTested>6.3.0</OSMaxVersionTested>
  </Prerequisites>
  <Resources>
    <Resource Language="x-generate" />
  </Resources>
  <Applications>
    <Application Id="DeviceAppForPrinters" Executable="$targetnametoken$.exe" EntryPoint="DeviceAppForPrinters.App">
      <VisualElements DisplayName="Device App For Printers C# sample" Logo="Assets\squareTile-sdk.png"
                      SmallLogo="Assets\smallTile-sdk.png" Description="DeviceAppForPrinters C# sample"
                      ForegroundText="light" BackgroundColor="#00b2f0" ToastCapable="true">
        <DefaultTile ShowName="allLogos" ShortName="App4PrinterCS" WideLogo="Assets\tile-sdk.png" />
        <SplashScreen Image="Assets\splash-sdk.png" BackgroundColor="#00b2f0" />
      </VisualElements>
      <Extensions>
        <Extension Category="windows.backgroundTasks" EntryPoint="BackgroundTask.PrintBackgroundTask">
          <BackgroundTasks>
            <Task Type="systemEvent" />
          </BackgroundTasks>
        </Extension>
        <Extension Category="windows.printTaskSettings" Executable="$targetnametoken$.exe" EntryPoint="DeviceAppForPrinters.App" />
      </Extensions>
    </Application>
  </Applications>
</Package>
```

## <a name="step-2-configure-device-metadata"></a>步骤2：配置设备元数据

当你使用**设备元数据创作向导**将你的应用程序与设备关联时，请确保完成 "**指定 UWP 设备应用信息**" 页上的 "**通知处理程序**" 框。 这有助于确保在打印通知期间调用应用的后台任务。

有关如何编辑设备元数据的分步说明，请参阅 [测试](#testing) 部分。

## <a name="step-3-build-the-ui"></a>步骤3：生成 UI

在构建你的应用程序之前，你应与你的设计人员和营销团队合作来设计用户体验。 用户体验应投影公司的品牌方面，并帮助你建立与用户的连接。

### <a name="design-guidelines"></a>设计准则

在设计磁贴和徽章体验之前，请务必查看 Microsoft Store 应用准则。 本指南可帮助确保你的应用程序提供与其他 UWP 应用一致的直观体验。

- [磁贴和锁屏提醒指南](https://go.microsoft.com/fwlink/p/?LinkId=317194)
- [Toast 通知指南](https://go.microsoft.com/fwlink/p/?LinkId=317193)

在应用程序的主页上，请记住，Windows 8.1 可以在单个监视器上以各种大小显示多个应用。 请参阅以下准则，详细了解应用程序如何在屏幕大小、窗口大小和方向之间进行适当的重新排列。

- [窗口大小和屏幕缩放的准则](https://go.microsoft.com/fwlink/p/?LinkId=311830)
- [将窗口调整为高度和缩小布局的准则](https://go.microsoft.com/fwlink/p/?LinkId=311831)

### <a name="best-practices"></a>最佳做法

- **请勿在通知中包含操作词。** 在通知消息上，不要使用通知用户的文本推送、按或单击 "通知"。 用户已经了解，他们可以按 toast 来了解更多信息。 例如，只需编写 "打印机墨水不足，而不是" 打印机墨水不足。 按进行故障排除。

- **保持交互简单。** 通知体验上显示的所有内容都应与通知相关。 例如，有关卡纸的通知页应该只包含有关解决该问题的链接和信息。 它不应包含相关体验的链接，例如购买墨迹或其他支持信息。

- **使用多媒体。** 使用设备的实际照片、视频或插图，帮助用户快速解决其设备问题。

- **将用户保留在应用的上下文中。** 提供有关问题的信息时，请不要链接到联机或其他支持材料。 将用户保留在应用的上下文中。

## <a name="step-4-create-background-task"></a>步骤4：创建后台任务

如果你的应用程序注册了用于打印通知的后台任务，则它必须为后台任务激活提供处理程序。 在 [打印设置和打印通知](https://go.microsoft.com/fwlink/p/?LinkID=242862) 示例中， `PrintBackgroundTask` 类处理打印通知。

>[!NOTE]
>如果打印机状态不需要立即用户干预，请更新磁贴，而不是显示 toast。 例如，对于墨水不足的情况，磁贴更新就足够了。 但如果打印机完全不使用墨迹，应用可能会显示 toast 通知。

### <a name="saving-notification-details"></a>正在保存通知详细信息

后台任务不能直接启动前景应用，只有用户可以：从磁贴、toast 或开始。 因此，为了确保前景应用可以访问打印通知的详细信息，后台任务会将其保存到本地存储中。 有关使用本地存储的详细信息，请参阅 [快速入门：本地应用数据](https://go.microsoft.com/fwlink/p/?LinkId=317216)。

当触发打印通知时，Windows 通过调用其方法来运行后台任务 `Run` 。 通过必须强制转换为类型 PrintNotificationEventDetails 的方法参数，将通知数据传递给后台任务。 `PrinterName` `EventData` 该对象的和属性分别携带打印机名称和双向消息。

此示例显示了 `Run` **PrintBackgroundTask.cs** 文件中的后台任务方法，其中打印通知详细信息在调用 toast、磁贴和徽章方法之前保存到应用设置。

```CSharp
public void Run(Windows.ApplicationModel.Background.IBackgroundTaskInstance taskInstance)
{
    // Save notification details to local storage
    PrintNotificationEventDetails details = (PrintNotificationEventDetails)taskInstance.TriggerDetails;
    settings.Values[keyPrinterName] = details.PrinterName;
    settings.Values[keyAsyncUIXML] = details.EventData;

    // Demonstrate possible actions
    ShowToast(details.PrinterName, details.EventData);
    UpdateTile(details.PrinterName, details.EventData);
    UpdateBadge();
}
```

### <a name="updating-a-tile"></a>更新磁贴

将打印通知详细信息发送到方法时 `UpdateTile` ，示例的后台任务演示如何在磁贴上显示它们。 有关磁贴的详细信息，请参阅 [磁贴和磁贴通知概述](https://go.microsoft.com/fwlink/p/?LinkId=317195)。

此示例显示了 `UpdateTile` **PrintBackgroundTask.cs** 文件中的后台任务的方法。

```CSharp
void UpdateTile(string printerName, string bidiMessage)
{
    TileUpdater tileUpdater = TileUpdateManager.CreateTileUpdaterForApplication();
    tileUpdater.Clear();

    XmlDocument tileXml = TileUpdateManager.GetTemplateContent(TileTemplateType.TileWide310x150Text09);
    XmlNodeList tileTextAttributes = tileXml.GetElementsByTagName("text");
    tileTextAttributes[0].InnerText = printerName;
    tileTextAttributes[1].InnerText = bidiMessage;

    TileNotification tileNotification = new TileNotification(tileXml);
    tileNotification.Tag = "tag01";
    tileUpdater.Update(tileNotification);
}
```

### <a name="updating-a-badge"></a>更新徽章

`UpdateBadge`方法演示如何使用 BadgeNotification 类更新徽章。 有关磁贴的详细信息，请参阅 [徽章概述](https://go.microsoft.com/fwlink/p/?LinkId=317196)。

此示例显示了 `UpdateBadge` **PrintBackgroundTask.cs** 文件中的后台任务的方法。

```CSharp
void UpdateBadge()
{
    XmlDocument badgeXml = BadgeUpdateManager.GetTemplateContent(BadgeTemplateType.BadgeGlyph);
    XmlElement badgeElement = (XmlElement)badgeXml.SelectSingleNode("/badge");
    badgeElement.SetAttribute("value", "error");

    var badgeNotification = new BadgeNotification(badgeXml);
    BadgeUpdateManager.CreateBadgeUpdaterForApplication().Update(badgeNotification);
}
```

### <a name="raising-a-toast"></a>引发 toast

Toast 通知是用户的一条暂时性消息，其中包含相关的、区分时间的信息，并提供对应用中相关内容的快速访问。 应向用户查看 Toast 通知，以返回到你的应用程序，使其继续关注感兴趣的内容。 有关详细信息，请参阅 [Toast 通知概述](https://go.microsoft.com/fwlink/p/?LinkId=317197)。

若要启用 toast 通知，应用程序需要在应用程序包清单中注册该应用程序支持 toast 功能。 在 `VisualElements` 元素中，将 `ToastCapable` 属性设置为 true。

>[!IMPORTANT]
>建议不要始终显示 toast，尤其是对于无法操作的事件。 这可能会给用户带来麻烦，导致用户无法从应用中关闭所有 toast。 对于不需要用户立即关注的事件，我们建议仅更新磁贴和徽章，而不显示 toast。

此示例显示元素中的 `ToastCapable` 属性 `VisualElements` ，因为它显示在应用包清单文件 **appxmanifest.xml**中。

```XML
<VisualElements DisplayName="Device App For Printers C# sample" Logo="Assets\squareTile-sdk.png"
                SmallLogo="Assets\smallTile-sdk.png" Description="DeviceAppForPrinters C# sample"
                ForegroundText="light" BackgroundColor="#00b2f0" ToastCapable="true">
  <DefaultTile ShowName="allLogos" ShortName="App4PrinterCS" WideLogo="Assets\tile-sdk.png" />
  <SplashScreen Image="Assets\splash-sdk.png" BackgroundColor="#00b2f0" />
</VisualElements>
```

此示例来自 `ShowToast` **PrintBackgroundTask.cs** 文件的方法。 它演示了如何根据两个名为和的字符串引发 `title` toast `body` 。

```CSharp
void ShowToast(string title, string body)
{
    //
    // Get Toast template
    //
    XmlDocument toastXml = ToastNotificationManager.GetTemplateContent(ToastTemplateType.ToastText02);

    //
    // Pass to app as eventArgs.detail.arguments
    //
    ((XmlElement)toastXml.SelectSingleNode("/toast")).SetAttribute("launch", title);

    //
    // The ToastText02 template has 2 text nodes (a header and a body)
    // Assign title to the first one, and body to the second one
    //
    XmlNodeList textList = toastXml.GetElementsByTagName("text");
    textList[0].AppendChild(toastXml.CreateTextNode(title));
    textList[1].AppendChild(toastXml.CreateTextNode(body));

    //
    // Show the Toast
    //
    ToastNotification toast = new ToastNotification(toastXml);
    ToastNotificationManager.CreateToastNotifier().Show(toast);
}
```

## <a name="step-5-handle-activation"></a>步骤5：处理激活

打印通知触发后台任务后，可以通过点击 toast 通知或磁贴来启动应用。 如果你的应用已从任一激活，则通过属性将参数传递给应用 `LaunchActivatedEventArgs.arguments` 。 有关激活和 Microsoft Store 应用生命周期的详细信息，请参阅 [应用程序生命](https://go.microsoft.com/fwlink/p/?LinkId=317387)周期。

若要确定应用程序是否已在这种情况下激活，请处理 `OnLaunched` 事件，并检查传递给事件处理程序的事件参数。 如果事件参数为 null，则该应用程序已由用户从开始激活。 如果事件参数不为 null，则从 toast 或磁贴启动应用。

此示例来自 `OnLaunched` **App.xaml.cs** 文件的方法。 它演示如何处理来自 toast 或磁贴的激活。

```CSharp
protected override async void OnLaunched(LaunchActivatedEventArgs args)
{
    Frame rootFrame = Window.Current.Content as Frame;

    // Do not repeat app initialization when the Window already has content,
    // just ensure that the window is active

    if (rootFrame == null)
    {
        // Create a Frame to act as the navigation context and navigate to the first page
        rootFrame = new Frame();
        // Associate the frame with a SuspensionManager key
        SuspensionManager.RegisterFrame(rootFrame, "AppFrame");

        if (args.PreviousExecutionState == ApplicationExecutionState.Terminated)
        {
            // Restore the saved session state only when appropriate
            try
            {
                await SuspensionManager.RestoreAsync();
            }
            catch (SuspensionManagerException)
            {
                //Something went wrong restoring state.
                //Assume there is no state and continue
            }
        }

        // Place the frame in the current Window
        Window.Current.Content = rootFrame;
    }
    if (rootFrame.Content == null || !String.IsNullOrEmpty(args.Arguments))
    {
        // When the navigation stack isn't restored or there are launch arguments
        // indicating an alternate launch (e.g.: via toast or secondary tile),
        // navigate to the appropriate page, configuring the new page by passing required
        // information as a navigation parameter
        if (!rootFrame.Navigate(typeof(MainPage), args.Arguments))
        {
            throw new Exception("Failed to create initial page");
        }
    }
    // Ensure the current window is active
    Window.Current.Activate();
}
```

## <a name="step-6-access-notification-details"></a>步骤6：访问通知详细信息

由于后台任务不能直接启动前景应用，因此需要将打印通知详细信息保存到应用的设置，以便前景应用可以访问它们。 有关使用本地存储的详细信息，请参阅 [快速入门：本地应用数据](https://go.microsoft.com/fwlink/p/?LinkId=317216)。

此示例显示如何从 " [打印设置" 和 "打印通知](https://go.microsoft.com/fwlink/p/?LinkID=242862) " 示例的 "应用设置" 中检索打印机名称和双向消息。 此代码来自 `DisplayBackgroundTaskTriggerDetails` **InkLevel.xaml.cs** 文件的方法。 请注意，键索引值 `keyPrinterName` 和 `keyAsyncUIXML` 是在后台任务 **PrintBackgroundTask.cs**中使用的字符串常量。

```CSharp
void DisplayBackgroundTaskTriggerDetails()
{
    String outputText = "\r\n";

    try
    {
        string printerName = settings.Values[keyPrinterName].ToString();
        outputText += ("Printer name from background task triggerDetails: " + printerName);
    }
    catch (Exception)
    {
        outputText += ("No printer name retrieved from background task triggerDetails ");
    }

    outputText += "\r\n";
    try
    {
        string asyncUIXML = settings.Values[keyAsyncUIXML].ToString();
        outputText += ("AsyncUI xml from background task triggerDetails: " + asyncUIXML);
    }
    catch (Exception)
    {
        outputText += ("No asyncUI xml retrieved from background task triggerDetails ");
    }

    ToastOutput.Text += outputText;
}
```

## <a name="testing"></a>测试

在可以测试 UWP 设备应用之前，必须使用设备元数据将其链接到您的打印机。

- 你需要打印机的设备元数据包的副本，以便向其添加设备应用信息。 如果没有设备元数据，可以使用 **设备元数据创作向导** 生成它，如主题为 [UWP 设备应用创建设备元数据](https://go.microsoft.com/fwlink/p/?LinkId=313644)中所述。

>[!NOTE]
>若要使用 **设备元数据创作向导**，在完成本主题中的步骤之前，必须安装 Microsoft Visual Studio Professional、Microsoft Visual Studio Ultimate 或 [独立的 SDK for Windows 8.1](https://go.microsoft.com/fwlink/p/?linkid=309209)。 为 Windows 安装 Microsoft Visual Studio Express 会安装不包括向导的 SDK 版本。

以下步骤生成应用并安装设备元数据。

1. 启用测试签名。
    1. 双击 "DeviceMetadataWizard.exe，从 *% ProgramFiles (x86) %* Windows 工具包 8.1 bin **X86 启动设备元数据创作向导** \\ \\ \\ \\ **DeviceMetadataWizard.exe**
    2. 从 " **工具** " 菜单中，选择 " **启用测试签名**"。

2. 重新启动计算机
3. 通过打开解决方案 ( .sln) 文件来生成解决方案。 加载示例后，按 F7 或从顶部菜单中转到 " **生成- &gt; 生成解决方案** "。

4. 断开连接并卸载打印机。 此步骤是必需的，以便 Windows 将在下一次检测到设备时读取更新的设备元数据。
5. 编辑并保存设备元数据。 若要将设备应用链接到设备，你必须将设备应用关联到设备。
    >[!NOTE]
    >如果尚未创建设备元数据，请参阅 [为 UWP 设备应用创建设备元数据](https://go.microsoft.com/fwlink/p/?LinkId=313644)。

    1. 如果**设备元数据创作向导**尚未打开，请通过双击 "DeviceMetadataWizard.exe" 从 *% ProgramFiles (x86) %* \\ Windows 工具包 \\ 8.1 \\ bin \\ x86 **DeviceMetadataWizard.exe**启动它。
    2. 单击 " **编辑设备元数据**"。 这将允许你编辑现有的设备元数据包。
    3. 在 " **打开** " 对话框中，找到与 UWP 设备应用关联的设备元数据包。  (其文件扩展名为 **devicemetadata** 。 ) 
    4. 在 " **指定 uwp 设备应用信息** " 页上，在 " **UWP 设备应用** " 框中输入 Microsoft Store 应用信息。 单击 " **导入 UWP 应用程序清单文件** " 以自动输入 **包名称**、 **发布者名称**和 **UWP 应用 ID**。
    5. 如果你的应用正在注册打印机通知，请填写 **通知处理程序** 框。 在 " **事件 ID**" 中，输入打印事件处理程序的名称。 在 " **事件资产**" 中，输入代码所在的文件的名称。

    6. 完成后，单击 " **下一步** "，直到到达 " **完成** " 页。
    7. 在 " **查看设备元数据包** " 页上，确保所有设置均正确，并选中 "将 **设备元数据包复制到本地计算机上的元数据存储区** " 复选框。 然后单击“保存”  。

6. 重新连接打印机，以便 Windows 在连接设备时读取更新的设备元数据。

## <a name="troubleshooting"></a>故障排除

### <a name="issue-no-default-toast-notification-appears"></a>问题：未显示默认 toast 通知

如果在预期时未出现默认打印通知 .。。

- **可能的原因：** 未启用测试签名。 请参阅本主题中的调试部分，了解有关如何打开它的信息。

- **可能的原因：** 域策略已禁用 toast 通知。 离开域，然后重试。

- **可能的原因：** 打印机未实现 DriverEvents。 检查 v4 驱动程序是否支持双向和 DriverEvents。 有关详细信息，请参阅 [自定义 UI 的驱动程序支持](../print/driver-support-for-customized-ui.md)。

- **可能的原因：** 计算机在打印机队列中没有最近的作业。 请确保在屏幕右下角显示 "打印机" 图标。 否则，请发送另一个打印作业。

- **可能的原因：** 后台任务 () 的入口点 `IBackgroundTask` 与前台应用在同一项目中。 这是不允许的。 分离出用于后台任务处理程序的一个全新的类。

- **可能的原因：** 作为应用中的通知入口点的类在清单或设备元数据中不正确地给定，导致应用在 backgroundhost 内崩溃，而不显示任何 toast。 查看以下内容：

  - 请确保在清单设计器的 " **声明** " 选项卡中正确地提供了入口点。 它应采用命名空间. 类的形式，适用于 c # 和 c + +。 对于 JavaScript，它应为 .js 文件的相对目录路径。
  - JavaScript 应用在完成后应调用 close ( # A1。
  - C # 类必须实现 Windows.applicationmodel.resources.core，并且必须具有公共 void `Run(Windows.ApplicationModel.Background.IBackgroundTaskInstance taskInstance)` 方法。
  - C + + 类必须实现 Windows：： Windows.applicationmodel.resources.core：： Background：： IBackgroundTask，并且必须有一个 `virtual void Run(Windows::ApplicationModel::Background::IBackgroundTaskInstance^ taskInstance)` 方法。

## <a name="related-topics"></a>相关主题

[UWP 应用 (徽章概述) ](/previous-versions/windows/apps/hh779719(v=win.10))

[ (UWP 应用的磁贴和磁贴通知概述) ](/previous-versions/windows/apps/hh779724(v=win.10))

[磁贴和徽章 (UWP 应用的指南和清单) ](https://go.microsoft.com/fwlink/p/?LinkId=317194)

[UWP 通知概述 (UWP 应用) ](https://go.microsoft.com/fwlink/p/?LinkId=317197)

[ (UWP 应用的 toast 通知的指导原则和清单) ](https://go.microsoft.com/fwlink/p/?LinkId=317193)

[自定义 UI 的驱动程序支持](../print/driver-support-for-customized-ui.md)

[开发 v4 打印驱动程序](https://go.microsoft.com/fwlink/p/?LinkId=314231)

[ (v4 打印驱动程序的打印机扩展接口) ](https://go.microsoft.com/fwlink/p/?LinkID=299887)

[双向通信](https://go.microsoft.com/fwlink/p/?LinkId=317192)

[UWP 应用入门](getting-started.md)

[ (分步指南创建 UWP 设备应用) ](step-1--create-a-uwp-device-app.md)

[ (分步指南创建 UWP 设备应用的设备元数据) ](step-2--create-device-metadata.md)