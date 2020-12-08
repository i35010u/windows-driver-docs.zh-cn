---
title: 已分配访问最佳实践的展台应用
description: 已分配访问最佳实践的展台应用
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ded10274b1dfccb9622a614eb6c9131dad650351
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96806069"
---
# <a name="kiosk-apps-for-assigned-access-best-practices"></a>分配有访问权限的展台应用：最佳实践

在 Windows 10 中，可以使用已分配的访问权限来创建展台设备，这样用户就可以只与单个通用 Windows 应用交互。 本主题介绍如何实现展台应用和最佳实践。

分配的访问权限提供了两种不同的体验：

1. 单应用展台体验
    1. 向帐户分配一个应用。 当用户登录时，他们将只能访问此应用和系统上的任何其他内容。 在此期间，kiosk 设备会锁定，并在锁屏界面上运行展台应用。 此体验通常用于面向公众的展台计算机。 有关详细信息，请参阅 [在 Windows 10 专业版、企业版或教育版上设置展台](/windows/configuration/set-up-a-kiosk-for-windows-10-for-desktop-editions) 。

2. Windows 10 版本1709及更高版本中提供了多应用展台体验 () 
    1. 可以将一个或多个应用分配给帐户。 当用户登录时，设备将在受限 shell 体验中启动，只允许访问所选应用。 有关详细信息，请参阅 [创建运行多个应用程序的 Windows 10 展台](/windows/configuration/lock-down-windows-10-to-specific-apps) 。

> [!NOTE]
> 本文仅介绍单应用展台体验。 在多应用体验中，所选应用在常规桌面上下文中运行，无需特殊处理或修改。

## <a name="terms"></a>术语

|术语|描述|
|----|----|
|分配的访问权限|一项功能，该功能允许系统管理员通过限制公开给设备用户的应用程序入口点来管理用户的体验。 例如，你可以限制企业中的客户使用一个应用程序，使你的电脑充当展台。 当有人使用指定的帐户登录时，他们只能使用一个应用。 它们无法切换应用或使用触摸手势、鼠标、键盘或硬件按钮关闭应用。 它们也看不到任何应用通知。|
|锁定屏幕应用 (或锁定应用) |利用功能设置动态墙纸或利用新的锁定扩展性框架的应用程序。|
|以上锁屏应用 (或以上锁定应用) |在锁定屏幕应用运行时，在锁定屏幕上方启动的应用程序 (例如，桌面锁定) 。|
|锁定应用|在未锁定的 Windows 上下文中正常运行的应用程序。|
|LockApplicationHost|一种 WinRT 类，可用于在设备开始解锁时允许锁定屏幕应用程序请求设备解锁，并允许应用程序注册通知。|
|视图或应用程序视图|每个视图都是一个单独的应用程序窗口。 应用可以具有主视图，并按需创建多个和辅助视图。 有关详细信息，请参阅 [w](/uwp/api/Windows.UI.ViewManagement.ApplicationView) 。|

## <a name="the-windowsabovelockscreen-extension"></a>AboveLockScreen 扩展

Windows 10 中分配的访问权限利用了锁框架。 当分配的访问权限用户登录时，后台任务会锁定桌面并在锁定之上启动展台应用。 应用的行为可能不同，具体取决于它是否使用 aboveLockScreen 扩展名。

使用 **aboveLockScreen** ，kiosk 应用程序可以访问 [LockApplicationHost](/uwp/api/Windows.ApplicationModel.LockScreen.LockApplicationHost) 运行时类，这使应用程序能够了解其在锁定 (以上运行的时间，并以展台体验) 运行。 如果无法返回实例，则该应用将在常规桌面上下文中运行。

当 lock framework 在锁定之上启动展台应用并且应用具有 **aboveLockScreen** 扩展名时，lock framework 会自动在锁定之上创建新的辅助视图。 主视图位于锁定下。 此辅助视图将包含应用的内容以及用户看到的内容。 此附加视图可与扩展结合使用，以定制展台体验。 例如，你能够：

* 通过创建单独的页面来显示仅限展台的内容，[保护展台体验](#secure-your-information)。

* 从应用程序中调用 **LockApplicationHost. RequestUnlock ( # B1** 方法，以 [添加超出分配的访问模式的方式](#add-a-way-out-of-assigned-access) 并返回到登录屏幕。

* [将事件处理程序添加](#add-a-way-out-of-assigned-access) 到在用户按下 Ctrl + Alt + Del 退出展台体验时触发的 **LockApplicationHost* 事件中。 处理程序还可用于在退出前保存任何数据。

如果应用没有 **aboveLockScreen** 扩展，则不会创建辅助视图，并且应用程序将以正常运行的方式启动。 此外，由于应用程序将无法访问 LockApplicationHost 实例，因此无法确定它是在常规上下文中运行，还是用于展台体验。 不包含扩展的优点，如能够支持 [多个监视器](#dispatcher)

无论你的应用程序是否使用扩展，都一定要保护其数据。 有关详细信息，请参阅 [分配的访问应用的指南](/windows/configuration/guidelines-for-assigned-access-app#secure-your-information) 。

> [!NOTE]
> 从 Windows 10 版本1607开始，对通用 Windows 平台 (UWP) 扩展不再有限制，因此，当用户配置分配的访问权限时，大多数应用程序都可以在 " **设置** " 中显示。

## <a name="best-practices"></a>最佳做法

> [!NOTE]
> 本部分适用于使用 **aboveLockScreen** 扩展的展台应用程序。

### <a name="secure-your-information"></a>保护你的信息

如果展台应用程序要同时运行上面的锁定并在未锁定的 Windows 上下文中运行，你可能需要创建一个在锁定之前呈现的不同页面，并在锁下创建另一个页面。 这将允许你避免在展台模式下显示敏感信息，因为展台模式通常意味着匿名访问。 下面是使用两个不同页面的步骤，一个用于锁定下，另一个用于锁定：

1. 在 App.xaml.cs 中 **OnLaunched** 函数的重写中，尝试在 rootFrame 导航之前获取 [LockApplicationHost](/uwp/api/Windows.ApplicationModel.LockScreen.LockApplicationHost) 类的实例。
2. 如果调用失败，kiosk 应用应在锁定下正常启动。
3. 如果调用成功，kiosk 应用应启动在已分配访问模式下运行的锁定之上。 你可能希望此版本的展台应用具有不同的主页，以隐藏敏感信息。

下面的示例演示如何执行此操作。 AssignedAccessPage 是预定义的，应用程序在检测到在上面的锁定模式下运行后，会导航到 AssignedAccessPage。 因此，普通页面将仅在锁定方案下显示。

你可以使用此方法来确定应用程序是否在应用生命周期中的任何时间运行在锁屏界面上，并做出相应的响应。

```cpp
using Windows.ApplicationModel.LockScreen;

// inside the override OnLaunched function in App.xaml.cs

if (rootFrame.Content == null)
{
    LockApplicationHost host = LockApplicationHost.GetForCurrentView();
    if (host == null)
    {
        // if call to LockApplicationHost is null, this app is running under lock
        // render MainPage normally
        rootFrame.Navigate(typeof(MainPage), e.Arguments);
    }
    else
    {
        // If LockApplicationHost was successfully obtained
        // this app is running as a lock screen app, or above lock screen app
        // render a different page for assigned access use
        // to avoid showing regular main page to keep secure information safe
        rootFrame.Navigate(typeof(AssignedAccessPage), e.Arguments);
    }
}
```

### <a name="multiple-views-windows-and-threads"></a>多个视图、窗口和线程

从 Windows 10 1803 版开始，在没有 **aboveLockScreen** 扩展的应用程序的展台体验中支持 [多个视图](/windows/uwp/design/layout/show-multiple-views)。 若要使用多个视图，请确保将展台设备的 " **多个显示** " 选项设置为 **扩展这些显示**。

如果有多个视图的应用程序 (，而没有 **aboveLockScreen**) 在展台体验期间启动，则会在第一台监视器上呈现应用程序的主视图。 如果使用 CreateNewView 的应用创建了新视图 [ ( # B1 ](/uwp/api/windows.applicationmodel.core.coreapplication)，则将在第二个监视器上呈现。 如果应用创建另一个视图，它将会跳到第三个监视器，依此类推。

> [!IMPORTANT]
> 展台设备每个监视器只能显示一个视图。 例如，如果展台设备只有一个监视器，它将始终显示展台应用的主视图。 将不显示应用创建的新视图。

如果展台应用具有 **aboveLockScreen** 扩展，并且运行在该锁的上方，则会以不同的方式对其进行初始化。 其主视图位于锁定下，其上方有一个辅助视图。 此辅助视图将是用户将看到的内容。 请注意，即使没有显式创建任何新视图，应用程序实例中仍有两个视图。  

![z-在锁定模式下运行应用时的视图顺序](images/assignedaccesssamplelayout.png)

您可以在应用程序的主窗口中运行以下代码 (处于分配的访问模式) 查看视图计数以及当前屏幕是否为主视图。

```cpp
using Windows.ApplicationModel.Core;

CoreApplication.GetCurrentView().IsMain //false
CoreApplication.Views.Count //2
```

### <a name="dispatcher"></a>调度程序

每个视图或窗口都有自己的调度程序。 由于主视图对用户是隐藏的，因此请使用 **GetCurrentView ( # B1** 来访问在锁定之前运行的应用的辅助视图，而不是 MainView ( # A3。

```cpp
using Windows.ApplicationModel.Core;

private async void Button_Click(object sender, RoutedEventArgs e)
{
    button.IsEnabled = false;

    // start a background task and update UI periodically (every 1 second)
    // using MainView dispatcher in below code will end up with app crash
    // in assigned access mode, use GetCurrentView().Dispatcher instead
    await CoreApplication.GetCurrentView().Dispatcher.RunAsync(
        CoreDispatcherPriority.Normal,
        async () =>
        {
            for (int i = 0; i < 60; ++i)
            {
                // do some background work, here we use Task.Delay to sleep
                await Task.Delay(1000);
                // update UI
                textBlock1.Text = "   " + i.ToString();
            }
            button.IsEnabled = true;
        });
}
```

当应用具有 aboveLockScreen 并以展台体验运行时，创建新视图将导致应用中出现异常：

```cpp
Windows.ApplicationModel.Core.CoreApplication.CreateNewView(); //causes exception
```

因此，不能有多个视图，也不能在多个监视器上运行。 如果你的应用程序需要支持这两者，你将需要从应用程序中删除 aboveLockScreen 扩展。

### <a name="add-a-way-out-of-assigned-access"></a>添加超出分配的访问权限

在某些情况下，可能未在键盘上启用或使用用于停止应用程序的 "电源" 按钮、"取消" 按钮或其他按钮。 在这些情况下，提供一种停止分配的访问权限（例如软件密钥）的方法。 下面的事件处理程序演示如何通过响应按钮选择可能由软件密钥触发的事件来停止分配的访问模式。

```cpp
LockApplicationHost^ lockHost = LockApplicationHost::GetForCurrentView();
    if (lockHost != nullptr)
    {
        lockHost->RequestUnlock();
    }
```

### <a name="lifecycle-management"></a>生命周期管理

展台应用的生命周期由分配的访问框架处理。 如果应用意外结束，框架将尝试重新启动该应用。 但是，如果用户按 "Ctrl + Alt + Del" 打开登录屏幕，则会触发解除锁定事件。 分配的访问框架侦听事件，并尝试终止应用。

展台应用还可以注册此事件的处理程序，并在退出之前执行操作。 保存任何数据就是一个示例。 有关注册处理程序的示例，请参阅下面的代码。

```cpp
using Windows.ApplicationModel.LockScreen;

public AssignedAccessPage()
{
    this.InitializeComponent();

    LockApplicationHost lockHost = LockApplicationHost.GetForCurrentView();
    if (lockHost != null)
    {
        lockHost.Unlocking += LockHost_Unlocking;
}
}

private void LockHost_Unlocking(LockApplicationHost sender, LockScreenUnlockingEventArgs args)
{
    // save any unsaved work and gracefully exit the app
    App.Current.Exit();
}
```

用户按下 Ctrl + Alt + Del 并显示登录屏幕后，可能会发生两种情况：

1. 用户知道分配的访问帐户密码并解锁桌面。 已分配的访问框架将启动、锁定桌面和锁屏界面应用启动，从而启动展台应用。
2. 用户不知道密码，或者不采取任何进一步操作。 登录屏幕超时和桌面 relocks;锁屏界面应用会启动，然后启动展台应用。

### <a name="dont-create-new-windows-or-views-in-assigned-access-mode"></a>不在分配的访问模式下创建新的窗口或视图

如果在指定的访问模式下调用，则以下函数调用最终会出现运行时异常。 如果同一应用在锁下使用时调用函数，则不会导致运行时异常。 使用 [LockApplicationHost](/uwp/api/Windows.ApplicationModel.LockScreen.LockApplicationHost) 来确定应用程序的已分配访问模式，并对应用程序进行相应的编码（例如，如果应用程序处于分配的访问模式，则不会创建新的视图）会很有帮助。

```cpp
Windows.ApplicationModel.Core.CoreApplication.CreateNewView(); //causes exception
```

## <a name="appendix-1-uwp-extension"></a>附录1： UWP 扩展

下面的示例应用程序清单使用 **aboveLockScreen** UWP 扩展。

> [!NOTE]
> 从 Windows 10 版本1607开始，对通用 Windows 平台 (UWP) 扩展不再有限制，因此，当用户配置分配的访问权限时，大多数应用程序都可以在 " **设置** " 中显示。

```cpp
<Package xmlns="http://schemas.microsoft.com/appx/manifest/foundation/windows10" xmlns:mp="http://schemas.microsoft.com/appx/2014/phone/manifest" xmlns:uap="http://schemas.microsoft.com/appx/manifest/uap/windows10" IgnorableNamespaces="uap mp">
  <Identity Name="bd4df68b-dc18-4748-a14e-bc21dac13736" Publisher="Contoso" Version="1.0.0.0" />
  <mp:PhoneIdentity PhoneProductId="bd4df68b-dc18-4748-a14e-bc21dac13736" PhonePublisherId="00000000-0000-0000-0000-000000000000" />
  <Properties>
    <DisplayName>AboveLock</DisplayName>
    <PublisherDisplayName>Contoso</PublisherDisplayName>
    <Logo>Assets\StoreLogo.png</Logo>
  </Properties>
  <Dependencies>
    <TargetDeviceFamily Name="Windows.Universal" MinVersion="10.0.0.0" MaxVersionTested="10.0.0.0" />
  </Dependencies>
  <Resources>
    <Resource Language="x-generate" />
  </Resources>
  <Applications>
    <Application Id="App" Executable="$targetnametoken$.exe" EntryPoint="AboveLock.App">
      <uap:VisualElements DisplayName="AboveLock" Square150x150Logo="Assets\Square150x150Logo.png" Square44x44Logo="Assets\Square44x44Logo.png" Description="AboveLock" BackgroundColor="transparent">
        <uap:DefaultTile Wide310x150Logo="Assets\Wide310x150Logo.png">
        </uap:DefaultTile>
        <uap:SplashScreen Image="Assets\SplashScreen.png" />
      </uap:VisualElements>
      <Extensions>
        <uap:Extension Category="windows.lockScreenCall" />
        <uap:Extension Category="windows.aboveLockScreen" />
      </Extensions>
    </Application>
  </Applications>
  <Capabilities>
    <Capability Name="internetClient" />
  </Capabilities>
</Package>
```

## <a name="appendix-2-troubleshooting"></a>附录2：疑难解答

通常，如果展台应用无法在锁屏界面应用上方激活，可以在锁定屏幕中找到激活错误代码。 使用错误代码通过查找 Windows [系统错误代码](/windows/desktop/Debug/system-error-codes)来发现问题。 此外事件查看器包含有关激活失败的详细信息。 为此，请执行以下操作：

1. 打开“**事件查看器**”。 查找激活错误有两个可能的位置。
2. 在 " **事件查看器 (本地)** " 窗格中，展开 " **Windows 日志**"，然后选择 " **应用程序**"。
3. 此外，在 **事件查看器 (本地)**，展开 " **应用程序和服务日志**"，展开 " **Windows**"，展开 " **应用**"，然后选择 " **TWinUI/操作**"。

请注意，由于具有分配的访问权限的展台应用不会在全屏模式下运行，因此 **w. GetForCurrentView ( # A1。IsFullScreenMode** 将返回 false。

## <a name="related-topics"></a>相关主题

[已分配的访问权限](/windows-hardware/customize/enterprise/assigned-access)

[显示应用的多个视图](/windows/uwp/design/layout/show-multiple-views)
