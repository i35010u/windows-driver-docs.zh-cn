---
title: 使用 UWP 设备应用中的打印通知
description: 本主题介绍打印通知，并演示如何将C#版本的打印设置和打印示例使用后台任务响应打印通知的通知。
ms.assetid: 39A06A8A-5603-44AB-8884-C12B8E2F1A45
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 408ce806e8141cd26fa03b983ddb5b5827261dee
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369341"
---
# <a name="working-with-print-notifications-in-a-uwp-device-app"></a>使用 UWP 设备应用中的打印通知


在 Windows 8.1 中 UWP 设备应用程序可以响应从 v4 打印驱动程序发送的双向通信 (Bidi) 事件。 本主题介绍打印通知，并演示如何将C#的版本[打印设置和打印通知](https://go.microsoft.com/fwlink/p/?LinkID=242862)示例使用后台任务响应打印通知。 后台任务演示如何保存通知中的本地应用程序数据的详细信息存储、 发送 toast，和更新磁贴和徽章。 若要在一般情况下了解有关 UWP 的设备应用程序的详细信息，请参阅[满足 UWP 设备应用](meet-uwp-device-apps.md)。

C#的版本[打印设置和打印通知](https://go.microsoft.com/fwlink/p/?LinkID=242862)示例演示应用程序的背景部分 (*后台任务*) 中**BackgroundTask**项目。 后台任务的代码位于**PrintBackgroundTask.cs**文件。 *前台应用程序*，可以从开始，启动该全屏应用位于**DeviceAppForPrinters**项目。 **InkLevel.xaml.cs**文件显示了一种方法，可从前台应用程序访问通知的详细信息。 若要使用打印通知，该示例使用的打印机扩展库中**PrinterExtensionLibrary**项目。 打印机扩展库提供了方便地访问 v4 打印驱动程序的打印机扩展插件接口。 有关详细信息，请参阅[打印机扩展库概述](printer-extension-library-overview.md)。

**请注意**  本主题中所示的代码示例基于C#的版本[打印设置和打印通知](https://go.microsoft.com/fwlink/p/?LinkID=242862)示例。 此示例也会出现在 JavaScript 和C++。 请注意，由于C++可以直接访问 COMC++示例的版本不包括代码库项目。 下载示例，请参阅最新版本的代码。

 

## <a name="span-idprintnotificationsspanspan-idprintnotificationsspanspan-idprintnotificationsspanprint-notifications"></a><span id="Print_notifications"></span><span id="print_notifications"></span><span id="PRINT_NOTIFICATIONS"></span>打印通知


打印通知允许 UWP 设备应用程序时打印，例如纸，打开打印机门、 较低的墨水量或打印机纸张扩展错误通知的重要打印机事件的用户。 当打印机触发通知时，系统事件代理将运行您的应用程序的后台任务。 在这里，后台任务可以保存通知的详细信息、 发送 toast 通知、 更新磁贴、 更新锁屏提醒，或不执行任何操作。 通过保存通知的详细信息，您的应用程序可以提供可帮助用户了解和解决打印机问题的体验。

**请注意**  打印机制造商必须在其 v4 打印驱动程序用于打印通知使用其 UWP 设备应用程序中实现 Bidi 和 DriverEvent XML 文件。 有关详细信息，请参阅[的双向通信](https://go.microsoft.com/fwlink/p/?LinkId=317192)。

 

当 DriverEvent 发生，并且启动 UWP 设备应用的后台任务时，应用具有多个选项，则会继续运行指定。 有关任务的启动会导致流的更多详细信息，请参阅[驱动程序支持自定义 UI](https://docs.microsoft.com/windows-hardware/drivers/print/driver-support-for-customized-ui)。

可以选择的后台任务：

-   不执行任何操作
-   保存通知的详细信息中[本地应用程序数据存储区](https://go.microsoft.com/fwlink/p/?LinkId=317216)
-   更新[UWP 应用磁贴通知](https://go.microsoft.com/fwlink/p/?LinkId=317195)
-   更新[UWP 应用通知徽章](https://go.microsoft.com/fwlink/p/?LinkId=317196)
-   发送[UWP 应用的 toast 通知](https://go.microsoft.com/fwlink/p/?LinkId=317197)

磁贴通知或 toast 通知可以让用户方便地启动前台应用程序。 前台应用程序启动时，它可以使用`OnLaunched`中的方法**App.xaml.cs**检查如果它启动的磁贴或 toast。 如果是，前台应用程序可以访问在任何打印通知的详细信息[本地应用程序数据存储区](https://go.microsoft.com/fwlink/p/?LinkId=317216)。

## <a name="span-idprerequisitesspanspan-idprerequisitesspanspan-idprerequisitesspanprerequisites"></a><span id="Prerequisites"></span><span id="prerequisites"></span><span id="PREREQUISITES"></span>先决条件


开始之前：

1.  请确保使用 v4 打印驱动程序安装您的打印机。 有关详细信息，请参阅[开发 v4 打印驱动程序](https://go.microsoft.com/fwlink/p/?LinkId=314231)。
2.  获取对开发计算机设置。 请参阅[入门](getting-started.md)有关下载工具和创建开发人员帐户信息。
3.  将你的应用与应用商店相关联。 请参阅[创建 UWP 设备应用](step-1--create-a-uwp-device-app.md)有关的信息。
4.  创建设备元数据为您将其与您的应用程序关联的打印机。 请参阅[创建设备元数据](step-2--create-device-metadata.md)有关的详细信息。
5.  构建您的应用程序的主页上的 UI。 可以从开始，它们将显示的全屏启动所有 UWP 设备应用程序。 使用入门体验突出显示你的产品或匹配特定品牌的方式和你的设备的功能中的服务。 没有任何特殊限制可以使用 UI 控件的类型。 若要开始使用的设计的全屏体验，请参阅[Microsoft Store 设计原则](https://go.microsoft.com/fwlink/p/?LinkID=299845)。
6.  如果您正在编写您编写的应用程序与C#或 JavaScript 中，添加**PrinterExtensionLibrary**并**DeviceAppForPrintersLibrary**到您 UWP 设备应用程序解决方案的项目。 您可以找到这些项目中的每个[打印设置和打印通知](https://go.microsoft.com/fwlink/p/?LinkID=242862)示例。
    **请注意**  由于C++可以直接访问 COMC++应用程序不需要单独的库以使用基于 COM 的打印机设备上下文。

     

## <a name="span-idstep1registerbackgroundtaskspanspan-idstep1registerbackgroundtaskspanspan-idstep1registerbackgroundtaskspanstep-1-register-background-task"></a><span id="Step_1__Register_background_task"></span><span id="step_1__register_background_task"></span><span id="STEP_1__REGISTER_BACKGROUND_TASK"></span>步骤 1：注册后台任务


为了使 Windows 能够识别应用程序可以处理打印通知，它必须注册适用于打印通知的后台任务扩展。 此扩展中声明`Extension`元素中，使用`Category`属性设置为`windows.backgroundTasks`和一个`EntryPoint`属性设置为`BackgroundTask.PrintBackgroundTask`。 扩展插件还包括`Task`元素以指示它支持`systemEvent`任务类型。

可以在添加打印后台任务扩展**声明**清单设计器在 Microsoft Visual Studio 中的选项卡。 您还可以编辑的应用程序包清单 XML 手动，使用 XML （文本） 编辑器。 右键单击**Package.appxmanifest**中的文件**解决方案资源管理器**的编辑选项。

此示例演示中的后台任务扩展`Extension`元素，因为它在应用包清单文件中，将出现**Package.appxmanifest**。

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

## <a name="span-idstep2configuredevicemetadataspanspan-idstep2configuredevicemetadataspanspan-idstep2configuredevicemetadataspanstep-2-configure-device-metadata"></a><span id="Step_2__Configure_device_metadata"></span><span id="step_2__configure_device_metadata"></span><span id="STEP_2__CONFIGURE_DEVICE_METADATA"></span>步骤 2：配置设备元数据


当使用**设备元数据创建向导**若要将您的应用程序与你的设备相关联，为确保完整**通知处理程序**框**指定 UWP 设备应用程序信息**页。 这有助于确保打印通知期间调用您的应用程序的后台任务。

有关如何编辑设备元数据的分步说明，请参阅[测试](#testing)部分。

## <a name="span-idstep3buildtheuispanspan-idstep3buildtheuispanspan-idstep3buildtheuispanstep-3-build-the-ui"></a><span id="Step_3__Build_the_UI"></span><span id="step_3__build_the_ui"></span><span id="STEP_3__BUILD_THE_UI"></span>步骤 3：生成 UI


生成你的应用之前, 应适用于您的设计人员和营销团队设计用户体验。 用户体验应项目贵公司的品牌方面，并帮助您构建与你的用户的连接。

### <a name="span-iddesignguidelinesspanspan-iddesignguidelinesspanspan-iddesignguidelinesspandesign-guidelines"></a><span id="Design_guidelines"></span><span id="design_guidelines"></span><span id="DESIGN_GUIDELINES"></span>设计指南

请务必在设计您的磁贴和徽章体验之前查看 Microsoft Store 应用程序准则。 指导帮助确保您的应用程序提供了直观的体验与其他 UWP 应用一致的。

-   [磁贴和徽章准则](https://go.microsoft.com/fwlink/p/?LinkId=317194)
-   [Toast 通知准则](https://go.microsoft.com/fwlink/p/?LinkId=317193)

为您的应用程序的主页，请注意 Windows 8.1，可以在一台监视器上的各种大小显示多个应用。 请参阅以下指南以了解有关如何应用可以重排正常之间屏幕尺寸、 窗口大小和方向详细信息。

-   [窗口大小和扩展到屏幕的准则](https://go.microsoft.com/fwlink/p/?LinkId=311830)
-   [重设大小、 高和窄布局的 windows 的准则](https://go.microsoft.com/fwlink/p/?LinkId=311831)

### <a name="span-idbestpracticesspanspan-idbestpracticesspanspan-idbestpracticesspanbest-practices"></a><span id="Best_practices"></span><span id="best_practices"></span><span id="BEST_PRACTICES"></span>最佳做法

-   **不要包含通知操作单词。** 在通知消息中，不要使用文本，告知用户推送、 按下时，或单击通知。 用户已有所了解，他们可以按 toast 通知来了解详细信息。 例如只需编写"您的打印机墨水不足"而不是"您的打印机是缺墨。 按下以进行故障排除"。

-   **简化的交互。** 通知体验所示的所有内容应与该通知。 例如有关纸通知页应仅包含链接和有关解决该问题的信息。 它不应包含不相关的体验的链接，此类购买手写内容或其他支持信息。

-   **使用多媒体。** 使用实际的照片、 视频或的设备，帮助用户快速说明解决设备问题。

-   **使您的应用程序的上下文中的用户。** 提供有关问题的信息，不链接至联机或其他支持材料。 用户保持在应用程序的上下文中。

## <a name="span-idstep4createbackgroundtaskspanspan-idstep4createbackgroundtaskspanspan-idstep4createbackgroundtaskspanstep-4-create-background-task"></a><span id="Step_4__Create_background_task"></span><span id="step_4__create_background_task"></span><span id="STEP_4__CREATE_BACKGROUND_TASK"></span>步骤 4：创建后台任务


如果您的应用程序注册打印通知的后台任务，它必须提供后台任务激活的处理程序。 在中[打印设置和打印通知](https://go.microsoft.com/fwlink/p/?LinkID=242862)示例中，`PrintBackgroundTask`类处理的打印通知。

**请注意**  如果打印机状态不需要直接用户干预，更新磁贴而不是显示 toast 通知。 例如，对于墨水不足条件时，磁贴更新是足够的。 但是，如果打印机墨水用完完全是，应用可能会显示一条 toast 通知。

 

### <a name="span-idsavingnotificationdetailsspanspan-idsavingnotificationdetailsspanspan-idsavingnotificationdetailsspansaving-notification-details"></a><span id="Saving_notification_details"></span><span id="saving_notification_details"></span><span id="SAVING_NOTIFICATION_DETAILS"></span>正在保存通知详细信息

后台任务不能直接启动前台应用程序，只有用户可以： 从磁贴、 toast 或开始。 因此，若要确保前台应用程序可以访问打印通知的详细信息，后台任务将其保存到本地存储。 有关使用本地存储的详细信息，请参阅[快速入门： 本地应用程序数据](https://go.microsoft.com/fwlink/p/?LinkId=317216)。

打印通知触发时，Windows 将运行后台任务，通过调用其`Run`方法。 通知数据将传递到后台任务必须强制转换为键入 Windows.Devices.Printers.Extensions.PrintNotificationEventDetails 的方法参数。 `PrinterName`和`EventData`对象的属性分别执行的打印机名称和 Bidi 消息。

此示例演示的后台任务`Run`方法，请在**PrintBackgroundTask.cs**文件，其中打印通知的详细信息保存到应用设置，然后 toast，磁贴和徽章方法调用。

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

### <a name="span-idupdatingatilespanspan-idupdatingatilespanspan-idupdatingatilespanupdating-a-tile"></a><span id="Updating_a_tile"></span><span id="updating_a_tile"></span><span id="UPDATING_A_TILE"></span>更新磁贴

当将打印通知的详细信息发送到`UpdateTile`方法，该示例的后台任务演示如何在磁贴上显示它们。 有关图块的详细信息，请参阅[磁贴和磁贴通知概述](https://go.microsoft.com/fwlink/p/?LinkId=317195)。

此示例演示的后台任务`UpdateTile`方法，请在**PrintBackgroundTask.cs**文件。
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

### <a name="span-idupdatingabadgespanspan-idupdatingabadgespanspan-idupdatingabadgespanupdating-a-badge"></a><span id="Updating_a_badge"></span><span id="updating_a_badge"></span><span id="UPDATING_A_BADGE"></span>正在更新徽章

`UpdateBadge`方法演示了如何使用 BadgeNotification 类来更新锁屏提醒。 有关图块的详细信息，请参阅[徽章概述](https://go.microsoft.com/fwlink/p/?LinkId=317196)。

此示例演示的后台任务`UpdateBadge`方法，请在**PrintBackgroundTask.cs**文件。

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

### <a name="span-idraisingatoastspanspan-idraisingatoastspanspan-idraisingatoastspanraising-a-toast"></a><span id="Raising_a_toast"></span><span id="raising_a_toast"></span><span id="RAISING_A_TOAST"></span>引发 toast 通知

Toast 通知是包含时间敏感的相关信息并提供对应用程序中的相关内容的快速访问的用户临时消息。 Toast 通知应被视为向用户返回到你的应用上的相关事情后续跟进的邀请。 有关详细信息，请参阅[Toast 通知概述](https://go.microsoft.com/fwlink/p/?LinkId=317197)。

若要启用的 toast 通知，应用程序需要注册是 toast 支持的应用包清单中。 在中`VisualElements`元素中，设置`ToastCapable`属性为 true。

**重要**  我们不建议始终显示 toast 通知，尤其是对于非可操作事件。 这可能会变得令人讨厌的用户，并导致它们若要关闭应用程序中的所有 toast。 对于不需要用户立即注意的事件，我们建议更新磁贴和徽章，并且不显示 toast 通知。

 

此示例演示`ToastCapable`中的属性`VisualElements`元素，因为它在应用包清单文件中，将显示**Package.appxmanifest**。

```XML
<VisualElements DisplayName="Device App For Printers C# sample" Logo="Assets\squareTile-sdk.png" 
                SmallLogo="Assets\smallTile-sdk.png" Description="DeviceAppForPrinters C# sample" 
                ForegroundText="light" BackgroundColor="#00b2f0" ToastCapable="true">
  <DefaultTile ShowName="allLogos" ShortName="App4PrinterCS" WideLogo="Assets\tile-sdk.png" />
  <SplashScreen Image="Assets\splash-sdk.png" BackgroundColor="#00b2f0" />
</VisualElements>
```

此示例摘自`ShowToast`方法**PrintBackgroundTask.cs**文件。 它演示了如何引发基于两个字符串，名为 toast`title`和`body`。
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

## <a name="span-idstep5handleactivationspanspan-idstep5handleactivationspanspan-idstep5handleactivationspanstep-5-handle-activation"></a><span id="Step_5__Handle_activation"></span><span id="step_5__handle_activation"></span><span id="STEP_5__HANDLE_ACTIVATION"></span>步骤 5：处理激活


打印通知触发后台任务后，可以通过点击 toast 通知或磁贴启动应用。 如果从激活您的应用程序，则参数将传递到通过应用`LaunchActivatedEventArgs.arguments`属性。 关于激活和 Microsoft Store 应用程序生命周期的详细信息，请参阅[应用程序生命周期](https://go.microsoft.com/fwlink/p/?LinkId=317387)。

若要确定是否在这些情况下一个激活您的应用程序，请处理`OnLaunched`事件，并检查传递给事件处理程序的事件参数。 事件参数都为 null，如果用户从开始已激活应用程序。 如果事件自变量都不为 null 时，应用程序被启动从 toast 或磁贴。

此示例摘自`OnLaunched`方法**App.xaml.cs**文件。 它演示如何处理从 toast 或磁贴激活。
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

## <a name="span-idstep6accessnotificationdetailsspanspan-idstep6accessnotificationdetailsspanspan-idstep6accessnotificationdetailsspanstep-6-access-notification-details"></a><span id="Step_6__Access_notification_details"></span><span id="step_6__access_notification_details"></span><span id="STEP_6__ACCESS_NOTIFICATION_DETAILS"></span>步骤 6：访问通知的详细信息


由于后台任务不能直接启动前台应用程序，打印通知的详细信息需要保存对应用的设置，以便前台应用程序可以访问它们。 有关使用本地存储的详细信息，请参阅[快速入门： 本地应用程序数据](https://go.microsoft.com/fwlink/p/?LinkId=317216)。

此示例演示如何打印机名称和 Bidi 消息从检索中的应用设置[打印设置和打印通知](https://go.microsoft.com/fwlink/p/?LinkID=242862)示例。 代码摘自`DisplayBackgroundTaskTriggerDetails`方法**InkLevel.xaml.cs**文件。 请注意，密钥索引值`keyPrinterName`并`keyAsyncUIXML`，将在后台任务中，使用的同一个字符串常量**PrintBackgroundTask.cs**。
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

## <a name="span-idtroubleshootingspanspan-idtroubleshootingspanspan-idtroubleshootingspantroubleshooting"></a><span id="Troubleshooting"></span><span id="troubleshooting"></span><span id="TROUBLESHOOTING"></span>故障排除


### <a name="span-idissuenodefaulttoastnotificationappearsspanspan-idissuenodefaulttoastnotificationappearsspanspan-idissuenodefaulttoastnotificationappearsspanissue-no-default-toast-notification-appears"></a><span id="Issue__No_default_toast_notification_appears"></span><span id="issue__no_default_toast_notification_appears"></span><span id="ISSUE__NO_DEFAULT_TOAST_NOTIFICATION_APPEARS"></span>问题：将出现没有默认 toast 通知

如果没有默认打印通知时应会显示...

-   **可能的原因：** 未打开测试签名。 请参阅本主题了解如何将其打开的调试部分。

-   **可能的原因：** 域策略已禁用了 toast 通知。 将保留在域，然后重试。

-   **可能的原因：** 打印机尚未实施 DriverEvents。 检查 v4 驱动程序支持 Bidi 和 DriverEvents。 有关详细信息，请参阅[驱动程序支持自定义 UI](https://docs.microsoft.com/windows-hardware/drivers/print/driver-support-for-customized-ui)。

-   **可能的原因：** 计算机具有无最新作业在打印队列中。 请确保该打印机图标显示在屏幕的右下角。 否则，将发送另一个打印作业。

-   **可能的原因：** 后台任务的入口点 (`IBackgroundTask`) 是作为前台应用程序在同一项目中。 这不是允许。 单独出一个全新的后台任务处理程序类。

-   **可能的原因：** 清单或设备元数据，从而导致应用内 backgroundhost 崩溃或不显示任何 toast 错误地给出是通知应用程序中的入口点的类。 检查下列项目：

    -   请确保正确地在给定的入口点**声明**清单设计器选项卡。 它应为 Namespace.ClassName 格式为C#和C++。 对于 JavaScript，它应为.js 文件的相对目录路径。
    -   完成后，JavaScript 应用程序应调用 close （）。
    -   C#类必须实现 Windows.ApplicationModel.Background.IBackgroundTask，必须具有公共 void`Run(Windows.ApplicationModel.Background.IBackgroundTaskInstance taskInstance)`方法。
    -   C++类必须实现 Windows::ApplicationModel::Background::IBackgroundTask，必须具有`virtual void Run(Windows::ApplicationModel::Background::IBackgroundTaskInstance^ taskInstance) `方法。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[徽章概述 （UWP 应用）](https://go.microsoft.com/fwlink/p/?LinkId=317196)

[磁贴和磁帖通知概述 （UWP 应用）](https://go.microsoft.com/fwlink/p/?LinkId=317195)

[指南和核对清单磁贴和徽章 （UWP 应用）](https://go.microsoft.com/fwlink/p/?LinkId=317194)

[Toast 通知概述 （UWP 应用）](https://go.microsoft.com/fwlink/p/?LinkId=317197)

[指导原则和清单的 toast 通知 （UWP 应用）](https://go.microsoft.com/fwlink/p/?LinkId=317193)

[自定义 UI 的驱动程序支持](https://docs.microsoft.com/windows-hardware/drivers/print/driver-support-for-customized-ui)

[开发 v4 打印驱动程序](https://go.microsoft.com/fwlink/p/?LinkId=314231)

[打印机扩展插件接口 （v4 打印驱动程序）](https://go.microsoft.com/fwlink/p/?LinkID=299887)

[双向通信](https://go.microsoft.com/fwlink/p/?LinkId=317192)

[UWP 应用入门](getting-started.md)

[创建 UWP 设备应用程序 （分步指南）](step-1--create-a-uwp-device-app.md)

[创建设备元数据对 UWP 设备应用 （分步指南）](step-2--create-device-metadata.md)

 

 






