---
title: 展台应用的分配访问权限的最佳做法
description: 展台应用的分配访问权限的最佳做法
ms.assetid: 2405B5BB-2214-4B40-B3A1-C47073390B21
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3d6e3f27183154851e6d7d84cf78200c995f7a0a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63357788"
---
# <a name="kiosk-apps-for-assigned-access-best-practices"></a>涉及分配的访问权限的展台应用：最佳做法


在 Windows 10 中，可以使用已分配的访问以展台设备，它可以使用户只需单个通用 Windows 应用程序与之交互。 本主题介绍如何实现展台应用和最佳实践。

有两个不同体验，提供了已分配的访问：

1. 单应用展台体验
    1. 向帐户分配一个应用。 当用户记录时，它们将在系统上有权只有此应用程序和其他任何内容。 在此期间，网亭设备被锁定，与展台应用在锁定屏幕上运行。 这种体验通常用于面向公共的网亭计算机。 请参阅[设置 Windows 10 专业版、 企业版或教育版上的网亭](https://docs.microsoft.com/windows/configuration/set-up-a-kiosk-for-windows-10-for-desktop-editions)有关详细信息。

2. 多应用展台体验 （适用于 Windows 10 版本 1709年及更高版本）
    1. 您可以将一个或多个应用分配到帐户。 当用户记录时，将在与仅所选应用的访问权限的受限制的 shell 体验中启动设备。 请参阅[创建运行多个应用的 Windows 10 展台](https://docs.microsoft.com/windows/configuration/lock-down-windows-10-to-specific-apps)有关详细信息。

> [!NOTE]
> 本文介绍的单应用展台体验。 多应用体验，在所选的应用的常规桌面上下文中运行并不需要任何特殊处理或修改。

## <a name="terms"></a>术语


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>术语</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><span id="assigned_access"></span><span id="ASSIGNED_ACCESS"></span>已分配的访问</p></td>
<td><p>一种功能可以让系统管理员通过限制应用程序入口点公开给设备的用户来管理用户的体验。 例如，可以限制在你的业务客户对使用一个应用，因此您的 PC 的作用类似于作为网亭。 每当有人使用指定的帐户登录，他们将只能使用一个应用。 他们将不能切换应用程序或关闭应用程序使用触摸手势、 鼠标、 键盘或硬件按钮。 它们还不会看到任何应用内通知。</p></td>
</tr>
<tr class="even">
<td><p><span id="lock_screen_app__or_lock_app_"></span><span id="LOCK_SCREEN_APP__OR_LOCK_APP_"></span>锁定屏幕应用 （或锁定应用）</p></td>
<td><p>应用程序可以充分利用能够设置动态墙纸或充分利用新的锁可扩展性框架。</p></td>
</tr>
<tr class="odd">
<td><p><span id="above_lock_screen_app__or_above_lock_app_"></span><span id="ABOVE_LOCK_SCREEN_APP__OR_ABOVE_LOCK_APP_"></span>上面锁屏应用 （或更高版本锁定应用）</p></td>
<td><p>锁屏应用 （例如，当锁定桌面） 运行时在锁定屏幕上启动应用程序。</p></td>
</tr>
<tr class="even">
<td><p><span id="under_lock_app"></span><span id="UNDER_LOCK_APP"></span>锁定应用下</p></td>
<td><p>通常情况下，运行在解锁 Windows 上下文中的应用程序。</p></td>
</tr>
<tr class="odd">
<td><p><span id="LockApplicationHost"></span><span id="lockapplicationhost"></span><span id="LOCKAPPLICATIONHOST"></span><a href="https://go.microsoft.com/fwlink/?LinkId=691219" data-raw-source="[LockApplicationHost](https://go.microsoft.com/fwlink/?LinkId=691219)">LockApplicationHost</a></p></td>
<td><p>WinRT 类，该类允许以上锁定屏幕应用请求的设备解锁，并允许应用以注册设备开始进行解锁时收到通知。</p></td>
</tr>
<tr class="even">
<td><p><span id="View_or_Application_View"></span><span id="view_or_application_view"></span><span id="VIEW_OR_APPLICATION_VIEW"></span>视图或应用程序视图</p></td>
<td><p>每个视图是应用到一个单独的窗口。 应用可以查看和创建多个主和辅助数据库视图按需。 请参阅<a href="https://go.microsoft.com/fwlink/?LinkId=691220" data-raw-source="[ApplicationView]( https://go.microsoft.com/fwlink/?LinkId=691220)">ApplicationView</a>有关详细信息。</p></td>
</tr>
</tbody>
</table>



## <a name="the-windowsabovelockscreen-extension"></a>Windows.aboveLockScreen 扩展

Windows 10 中的已分配的访问利用锁框架中。 当已分配的访问用户记录时，后台任务锁定桌面，并启动上面锁展台应用。 应用程序的行为可能会有所不同，具体取决于是否使用 windows.aboveLockScreen 扩展。

使用**windows.aboveLockScreen**让你网亭的应用访问[LockApplicationHost](https://docs.microsoft.com/uwp/api/Windows.ApplicationModel.LockScreen.LockApplicationHost)运行时类，以使应用程序以了解何时运行上面锁 （并且因此以运行作为网亭体验）。 如果不能返回一个实例，常规的桌面上下文中运行应用程序。 

当锁 framework 启动上面锁展台应用，并应用了**windows.aboveLockScreen**扩展，锁框架会自动创建新的辅助视图上面锁。 主视图位于该锁。 此辅助视图将包含应用程序的内容，并为用户看到的内容。 此附加视图可以使用扩展，用于定制您的网亭体验。 例如，你可以：

* [保护你的网亭体验](#secureinfo)通过创建单独的页以显示仅限网亭的内容。

* 调用**LockApplicationHost.RequestUnlock()** 方法从你的应用[退出分配的访问权限模式](#addaway)并返回到登录屏幕。   

* [添加事件处理程序](#eventhandler)到 **LockApplicationHost.Unlocking*用户按 Ctrl + Alt + Del 退出展台体验时激发的事件。 处理还可用于在退出之前保存的任何数据。



如果应用不具有**windows.aboveLockScreen**扩展，则会创建任何辅助视图并像正常运行，该应用将启动。 此外，因为应用将无权访问的 LockApplicationHost 实例它将无法确定是否运行的在正则上下文中，或展台体验。 不包含扩展名有好处，例如能够支持[多个监视器](#multiplemonitors)


无论您的应用程序使用该扩展，请确保保护其数据。 请参阅[指导原则的应用程序分配的访问](https://docs.microsoft.com/windows/configuration/guidelines-for-assigned-access-app#secure-your-information)有关详细信息。

> [!NOTE]
> 从 Windows 10，版本 1607 中，开始没有不再限制通用 Windows 平台 (UWP) 扩展，因此，大多数应用程序可以显示在**设置**时配置用户分配访问权限。

## <a name="best-practices"></a>最佳做法


> [!NOTE]
> 本部分适用于使用的网亭应用程序**windows.aboveLockScreen**扩展。



### 保护信息 <a name="secureinfo"></a>

如果展台应用旨在运行在这两个以上锁分配访问权限，并且还在解锁 Windows 上下文中，可能想要创建其他页面，以便呈现之上锁定和锁下的其他页来。 这将允许您以避免由于展台模式通常意味着匿名访问在展台模式下显示的敏感信息。 下面是使用两个不同页、 一个用于锁定和锁的上述应遵循的步骤：

1.  内的重写**OnLaunched**函数在 App.xaml.cs 中，尝试获取的实例[LockApplicationHost](https://go.microsoft.com/fwlink/?LinkId=691219) rootFrame 导航前的类。
2.  如果调用失败，展台应用应启动通常情况下，在锁下。
3.  如果调用成功，展台应用应启动上面锁在已分配的访问模式下运行。 你可能想要具有不同的主页面，以隐藏敏感信息的展台应用的此版本。

下面的示例演示如何执行此操作。 AssignedAccessPage.xaml 预定义，并且应用将转到 AssignedAccessPage.xaml 后检测到在上面的锁模式运行。 常规页将显示结果，仅在锁方案下。

可以使用此方法来确定应用是否正在运行应用程序生命周期中随时锁屏界面上方并做出相应响应。
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

### 多个视图、 windows 和线程 <a name="multiplemonitors"></a>

从 Windows 10，版本 1803，开始[多个视图](https://docs.microsoft.com/windows/uwp/design/layout/show-multiple-views)中的不具有的应用的展台体验支持**windows.aboveLockScreen**扩展。 若要使用多个视图，请确保网亭设备**多个显示器**选项设置为**扩展这些显示器**。

当具有多个视图应用 (和而无需**windows.aboveLockScreen**) 启动在展台体验期间应用的主视图将呈现在第一个监视器上。 如果应用使用创建新视图[CreateNewView()](https://docs.microsoft.com/uwp/api/windows.applicationmodel.core.coreapplication)，它将在第二个监视器上呈现。 如果应用创建另一个视图，它将转到第三个监视器中，依次类推。

> [!IMPORTANT]
> 网亭设备只能显示每个监视器的一个视图。 例如，如果展台设备具有只在一个监视器，它将始终显示展台应用的主视图。 将不会显示新创建的应用程序的视图。

当展台应用具有**windows.aboveLockScreen**扩展，并且正在运行上面锁，它将初始化以不同的方式。 其主视图位于其上方的辅助视图使用锁。 此辅助视图将是用户将看到的内容。 请注意，即使不需要显式创建任何新的视图，您将仍有两个视图中将应用程序实例。  

![当在锁定模式下运行应用时，视图的 z 顺序](images/assignedaccesssamplelayout.png)

可以在你的应用 （在已分配的访问模式下） 的主窗口中运行以下代码以查看视图计数以及当前屏幕是主视图。

```cpp
using Windows.ApplicationModel.Core;

CoreApplication.GetCurrentView().IsMain //false
CoreApplication.Views.Count //2
```

### <a name="dispatcher"></a>调度程序

每个视图或窗口都有其自己的调度程序。 由于主视图向用户隐藏的因此使用**GetCurrentView()** 访问应用的辅助视图而不是 MainView() 锁之上运行。 

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

应用具有 windows.aboveLockScreen、 运行作为网亭体验时, 创建新视图将导致在应用中的引发异常：

```cpp
Windows.ApplicationModel.Core.CoreApplication.CreateNewView(); //causes exception
```

正因为如此，不能具有多个视图，或在多个监视器上运行。 如果您的应用程序需要支持，需要从您的应用程序中删除 windows.aboveLockScreen 扩展。


### 添加带已分配的访问方式 <a name="addaway"></a>

在某些情况下，电源按钮、 转义按钮或其他按钮用于停止应用程序可能无法启用或在键盘上提供。 在这些情况下，提供一种方法来停止已分配的访问，例如软件密钥。 以下事件处理程序演示如何停止已分配的访问模式通过响应按钮单击事件无法被触发的软件密钥。

```cpp
LockApplicationHost^ lockHost = LockApplicationHost::GetForCurrentView();
    if (lockHost != nullptr)
    {
        lockHost->RequestUnlock();
    }
```

### 生命周期管理 <a name="eventhandler"></a>

展台应用的生命周期是由已分配的访问框架处理的。 如果应用程序意外结束，框架将尝试重新启动它。 但是，用户按 Ctrl + Alt + Del 以显示登录屏幕，如果解锁事件时触发。 已分配的访问 framework 侦听事件，并将尝试终止应用程序。

展台应用还可以注册此事件的处理程序，并在退出之前执行的操作。 保存任何数据是此示例。 请参阅下面有关注册的处理程序的示例的代码。

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

用户按下 Ctrl + Alt + Del，并显示登录屏幕后，可能发生两件事：

1.  用户知道的已分配的访问帐户密码并解锁桌面。 已分配的访问 framework 启动时，锁定桌面和锁定屏幕应用启动反过来后将展台应用启动。
2.  用户不知道密码，或者不采取任何进一步的操作。 登录屏幕超时和桌面 relocks;后者又将启动展台应用锁定屏幕应用启动。

### <a name="span-iddontcreatenewwindowsorviewsinassignedaccessmodespanspan-iddontcreatenewwindowsorviewsinassignedaccessmodespanspan-iddontcreatenewwindowsorviewsinassignedaccessmodespandont-create-new-windows-or-views-in-assigned-access-mode"></a><span id="Don_t_create_new_windows_or_views_in_assigned_access_mode"></span><span id="don_t_create_new_windows_or_views_in_assigned_access_mode"></span><span id="DON_T_CREATE_NEW_WINDOWS_OR_VIEWS_IN_ASSIGNED_ACCESS_MODE"></span>不在已分配的访问模式下创建新窗口或视图

以下函数调用将最终的运行时异常如果在已分配的访问模式下调用。 如果同一应用时使用在锁，调用函数时，它不会导致运行时异常。 最好使用[LockApplicationHost](https://go.microsoft.com/fwlink/?LinkId=691219)来确定应用程序的已分配的访问模式，并相应地，代码您的应用程序，例如，如果应用在已分配的访问模式下不创建新的视图。

```cpp
Windows.ApplicationModel.Core.CoreApplication.CreateNewView(); //causes exception
```

## <a name="span-idappendix1uwpextensionspanspan-idappendix1uwpextensionspanspan-idappendix1uwpextensionspanappendix-1-uwp-extension"></a><span id="Appendix_1__UWP_extension"></span><span id="appendix_1__uwp_extension"></span><span id="APPENDIX_1__UWP_EXTENSION"></span>附录 1:UWP 扩展


下面的示例应用程序清单使用**windows.aboveLockScreen**UWP 扩展。 

> [!NOTE]
> 从 Windows 10，版本 1607 中，开始没有不再限制通用 Windows 平台 (UWP) 扩展，因此，大多数应用程序可以显示在**设置**时配置用户分配访问权限。


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

## <a name="span-idappendix2troubleshootingspanspan-idappendix2troubleshootingspanspan-idappendix2troubleshootingspanappendix-2-troubleshooting"></a><span id="Appendix_2__troubleshooting"></span><span id="appendix_2__troubleshooting"></span><span id="APPENDIX_2__TROUBLESHOOTING"></span>附录 2： 故障排除


通常情况下，如果无法激活上面锁屏应用展台应用，你可以在锁定屏幕中找到激活错误代码。 使用错误代码来通过查找 Windows 发现问题[系统错误代码](https://msdn.microsoft.com/library/windows/desktop/ms681381)。 此外，事件查看器包含激活故障的详细信息。 为此，请执行以下操作：

1.  打开**事件查看器**。 有两个可能位置查找激活错误。
2.  在中**事件查看器 （本地）** 窗格中，展开**Windows 日志**，然后单击**应用程序**。
3.  此外，在**事件查看器 （本地）**，展开**应用程序和服务日志**，展开**Windows**，展开**应用**，然后单击**Microsoft-Windows-TWinUI/操作**。

请注意，因为未在全屏幕模式下，运行已分配的访问与展台应用**ApplicationView.GetForCurrentView()。IsFullScreenMode**将返回 false。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[已分配的访问](https://msdn.microsoft.com/library/windows/hardware/mt620040)

[显示应用多个视图]( https://go.microsoft.com/fwlink/?LinkId=708251)





