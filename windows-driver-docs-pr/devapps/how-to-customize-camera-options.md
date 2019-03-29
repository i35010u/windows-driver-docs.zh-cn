---
title: 如何自定义 UWP 设备应用使用照相机选项
description: 在 Windows 8.1 UWP 设备应用程序允许设备制造商自定义某些相机应用中显示更多的照相机选项浮出控件。
ms.assetid: 4BA34A3F-3C0D-4DDC-BA0A-E62AE9A6A93A
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a715334377e827f67d42361fad6d39538b801fec
ms.sourcegitcommit: 56599ec634b3a731f2d13dff686be3b7b95390e4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/25/2019
ms.locfileid: "58419585"
---
# <a name="how-to-customize-camera-options-with-a-uwp-device-app"></a>如何自定义 UWP 设备应用使用照相机选项

在 Windows 8.1 UWP 设备应用程序允许设备制造商自定义某些相机应用中显示更多的照相机选项浮出控件。 本主题介绍**更多选项**浮出控件，显示由 CameraCatureUI API，并显示如何将C#的版本[UWP 用于相机的设备应用程序](https://go.microsoft.com/fwlink/p/?LinkID=227865)示例将替换与默认浮出控件自定义浮出控件。 若要在一般情况下了解有关 UWP 的设备应用程序的详细信息，请参阅[满足 UWP 设备应用](meet-uwp-device-apps.md)。

> [!NOTE]
> 在 Windows 8.1 中的内置相机应用程序不会显示**更多选项**按钮，因此不能显示一个 UWP 设备应用来显示更多的照相机选项。 但是， [CameraCaptureUI 类](https://go.microsoft.com/fwlink/p/?LinkId=317985)，，适用于所有 UWP 应用，确实有**更多选项**按钮，然后可以显示从它的 UWP 设备应用程序。

C#的版本[UWP 用于相机的设备应用程序](https://go.microsoft.com/fwlink/p/?LinkID=227865)的示例使用**DeviceAppPage.xaml**页以显示自定义的浮出控件，有关更多的相机选项 UI。 此示例也适用照相机效果使用照相机驱动程序 MFT （媒体基础转换）。 有关的详细信息，请参阅[创建照相机驱动程序 MFT](creating-a-camera-driver-mft.md)。

> [!NOTE]
> 本主题中所示的代码示例基于C#的版本[UWP 用于相机的设备应用程序](https://go.microsoft.com/fwlink/p/?LinkID=227865)示例。 此示例也是在 JavaScript 和 c + + 中可用。 下载示例，请参阅最新版本的代码。

## <a name="more-options-for-cameras"></a>用于相机的更多选项

体验是 UWP 设备应用提供了另一个应用，UWP 应用，捕获或通过使用预览视频从摄像机时的功能的多个照相机选项[CameraCaptureUI](https://go.microsoft.com/fwlink/p/?LinkId=317985) API。 它是可通过访问**更多选项**照相机选项窗口中的链接。 它不是全屏幕，但显示中弹出一个窗口，也就是用于显示用户单击或点击外部时关闭的轻量、 上下文的用户界面的控件。

这种体验可以突出显示不同的功能使用照相机，如应用自定义视频效果的能力。

当照相机不安装 UWP 设备应用时，Windows 提供默认值更多照相机选项体验。 如果 Windows 检测到为照相机、 安装的 UWP 设备应用程序和应用程序具有中选择的`windows.cameraSettings`扩展，您的应用程序取代了 Windows 提供的默认体验。

若要调用的更多的照相机选项浮出控件：

1. 打开使用的 UWP 应用[CameraCaptureUI](https://go.microsoft.com/fwlink/p/?LinkId=317985) API ( [CameraCaptureUI 示例](https://go.microsoft.com/fwlink/p/?linkid=228589)，例如)
2. 点击**选项**在 UI 中的按钮
3. 这将打开**照相机选项**设置分辨率和视频防抖动选项显示基本的浮出控件
4. 上**照相机选项**浮出控件，点击**更多选项**
5. **更多选项**浮出控件打开
    - *默认浮出控件*安装照相机无 UWP 设备应用会出现
    - 一个*自定义浮出控件*安装 UWP 相机的设备应用会出现

![有关更多的照相机选项默认浮出控件和自定义的浮出控件的-同时图像](images/372745-cameraoptionslaunching.png)

此图显示了有关更多的照相机选项旁边的自定义的浮出控件示例默认浮出控件。

## <a name="prerequisites"></a>先决条件

开始之前：

1. 获取对开发计算机设置。 请参阅[入门](getting-started.md)有关下载工具和创建开发人员帐户信息。
2. 将你的应用与应用商店相关联。 请参阅[创建 UWP 设备应用](step-1--create-a-uwp-device-app.md)有关的信息。
3. 创建设备元数据为您将其与您的应用程序关联的打印机。 请参阅[创建设备元数据](step-2--create-device-metadata.md)有关的详细信息。
4. 构建您的应用程序的主页上的 UI。 可以从开始，它们将显示的全屏启动所有 UWP 设备应用程序。 使用入门体验突出显示你的产品或匹配特定品牌的方式和你的设备的功能中的服务。 没有任何特殊限制可以使用 UI 控件的类型。 若要开始使用的设计的全屏体验，请参阅[Microsoft Store 设计原则](https://go.microsoft.com/fwlink/p/?LinkID=299845)。

## <a name="step-1-register-the-extension"></a>第 1 步：注册扩展

为了使 Windows 能够识别应用程序可以提供有关更多的照相机选项自定义浮出控件，它必须注册相机设置扩展。 此扩展中声明`Extension`元素中，使用`Category`属性设置为值为`windows.cameraSettings`。 在C#和 c + + 示例`Executable`属性设置为`DeviceAppForWebcam.exe`并`EntryPoint`属性设置为`DeviceAppForWebcam.App`。

可以添加照相机设置扩展**声明**清单设计器在 Microsoft Visual Studio 中的选项卡。 您还可以编辑的应用程序包清单 XML 手动，使用 XML （文本） 编辑器。 右键单击**Package.appxmanifest**中的文件**解决方案资源管理器**的编辑选项。

此示例演示中的照相机设置扩展`Extension`元素，因为它在应用包清单文件中，将出现**Package.appxmanifest**。

```XML
<?xml version="1.0" encoding="utf-8"?>
<Package xmlns="http://schemas.microsoft.com/appx/2010/manifest">
  <Identity Name="Microsoft.SDKSamples.DeviceAppForWebcam.CPP" Publisher="CN=Microsoft Corporation, O=Microsoft Corporation, L=Redmond, S=Washington, C=US" Version="1.0.0.0" />
  <Properties>
    <DisplayName>DeviceAppForWebcam CPP sample</DisplayName>
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
    <Application Id="DeviceAppForWebcam.App" Executable="$targetnametoken$.exe" EntryPoint="DeviceAppForWebcam.App">
      <VisualElements DisplayName="DeviceAppForWebcam CPP sample" Logo="Assets\squareTile-sdk.png" SmallLogo="Assets\smallTile-sdk.png" Description="DeviceAppForWebcam CPP sample" ForegroundText="light" BackgroundColor="#00b2f0">
        <DefaultTile ShortName="DeviceApp CPP" ShowName="allLogos" />
        <SplashScreen Image="Assets\splash-sdk.png" BackgroundColor="#00b2f0" />
      </VisualElements>
      <Extensions>
        <Extension Category="windows.cameraSettings" Executable="DeviceAppForWebcam.exe" EntryPoint="DeviceAppForWebcam.App" />
      </Extensions>
    </Application>
  </Applications>
</Package>
```

## <a name="step-2-build-the-ui"></a>步骤 2：生成 UI

生成你的应用之前, 应适用于您的设计人员和营销团队设计用户体验。 用户体验应项目贵公司的品牌方面，并帮助您构建与你的用户的连接。

### <a name="design-guidelines"></a>设计指南

务必要查看[UWP 应用浮出控件准则](https://go.microsoft.com/fwlink/p/?LinkId=317078)设计自定义的浮出控件之前。 指导帮助确保在浮出控件提供直观的体验与其他 UWP 应用一致的。

为您的应用程序的主页，请注意 Windows 8.1，可以在一台监视器上的各种大小显示多个应用。 请参阅以下指南以了解有关如何应用可以重排正常之间屏幕尺寸、 窗口大小和方向详细信息。

- [窗口大小和扩展到屏幕的准则](https://go.microsoft.com/fwlink/p/?LinkId=311830)
- [重设大小、 高和窄布局的 windows 的准则](https://go.microsoft.com/fwlink/p/?LinkId=311831)

### <a name="flyout-dimensions"></a>浮出控件维度

显示更多的照相机选项浮出控件是 625 像素高和宽 340 像素。 包含的区域**更多选项**顶部的文本由 Windows 提供，为自定义浮出控件的可视区域的高、 离开 560 像素的大约 65 像素。 自定义的浮出控件不应超过 340 像素宽。

![有关更多的照相机选项浮出控件尺寸。](images/372776-camera-options-layout.png)

> [!NOTE]
> 如果自定义的浮出控件是多个 560 像素高，用户可能会滑动或向下滚动以查看的浮出控件是高于还是低于可视区域的部分。

### <a name="suggested-effects"></a>建议的效果

- 颜色效果。 例如，灰度、 棕褐色调或 solarizing 整个图片。
- 人脸跟踪效果。 在其上添加其中图片和一个覆盖区，如乘幂号的或眼镜，一对中标识人脸。
- 场景模式。 这些是不同的光照条件的预设的曝光和焦点模式。

### <a name="suggested-settings"></a>建议设置

- 在 UWP 设备应用的自定义的浮出控件可以提供一个开关，用于启用硬件实现的设置，例如制造商提供的颜色校正方案。
- 实现补充公开的 UWP 设备应用的其他设置的基本属性。 例如，多个设备可能会公开控件用于调整亮度、 对比度、 闪烁、 焦点和风险，但实现真彩色自动调整亮度和对比度的设备可能不需要提供这些设置。

### <a name="restrictions"></a>限制

- 不要从主应用程序打开 UWP 设备应用的自定义的浮出控件 (通过调用`CameraOptionsUI.Show`方法) 时应用未流式处理或捕获。

- 执行不提供预览，或使 UWP 设备应用的自定义的浮出控件内的视频流的所有权。 自定义浮出控件旨在捕获视频的另一个应用的助手函数。 捕获应用程序具有视频流的所有权。 不应尝试访问使用低级别 Api 的视频流。 这可能会导致意外的行为，在其中捕获应用程序丢失了到流的访问权限。

- 不调整自定义浮出控件中的解决方法。

- 不要尝试显示弹出窗口、 通知或适用于自定义浮出控件的区域之外的对话框。 不允许这些类型的对话框。

- 不能启动自定义浮出控件内的音频或视频捕获。 自定义浮出控件旨在扩展另一个应用程序捕获视频中，而不是启动捕获本身。 此外，捕获音频或视频可能会触发一个系统对话框中，并在自定义浮出控件内不允许使用弹出对话框。

## <a name="step-3-handle-activation"></a>步骤 3:处理激活

如果您的应用程序已声明相机设置扩展，它必须实现`OnActivated`方法以处理应用程序激活事件。 此事件触发时的 UWP 应用，使用[CameraCaptureUI](https://go.microsoft.com/fwlink/p/?LinkId=317985)类，调用[CameraOptionsUI.Show](https://go.microsoft.com/fwlink/p/?LinkId=317995)方法。 应用程序激活时，您的应用程序可以选择哪一页将为该应用启动时启动。 对于具有声明相机设置扩展的应用程序，Windows 将 Activated 事件参数中传递的视频设备：Windows.ApplicationModel.Activation.IActivatedEventArgs.

UWP 设备应用程序可以确定激活旨在用于相机设置 (的人只是点击**更多选项**上**照相机选项**对话框) 时将事件参数的`kind`属性等于 Windows.ApplicationModel.Activation.ActivationKind.CameraSettings。

此示例演示中的激活事件处理程序`OnActivated`方法，因为它将出现在**App.xaml.cs**文件。 然后，事件自变量都强制转换为 Windows.ApplicationModel.Activation.CameraSettingsActivatedEventArgs 并且发送到`Initialize`方法的自定义浮出控件 (**DeviceAppPage.xaml.cs**)。

```CSharp
protected override void OnActivated(IActivatedEventArgs args)
{
    if (args.Kind == ActivationKind.CameraSettings)
    {
        base.OnActivated(args);
        DeviceAppPage page = new DeviceAppPage();
        Window.Current.Content = page;
        page.Initialize((CameraSettingsActivatedEventArgs)args);

        Window.Current.Activate();
    }
}
```

## <a name="step-4-control-settings-and-effects"></a>步骤 4：控制设置和效果

当`Initialize`方法的自定义浮出控件 (**DeviceAppPage.xaml.cs**) 调用时，视频设备通过事件参数传递给浮出控件。 这些自变量公开用于控制照相机的属性：

- **参数。VideoDeviceController**属性提供类型 Windows.Media.Devices.VideoDeviceController 的对象。 此对象提供用于调整标准设置方法。
- **参数。VideoDeviceExtension**属性是指向照相机驱动程序 MFT 的指针。 此属性将为 null，如果没有驱动程序 MFT 接口的公开方式。 有关照相机的驱动程序 Mft 的详细信息，请参阅[创建照相机驱动程序 MFT](creating-a-camera-driver-mft.md)。

此示例显示了部分`Initialize`方法，因为它将出现在**DeviceAppPage.xaml.cs**文件。 在这里，创建视频设备控制器 （videoDevController 对象） 和照相机驱动程序 MFT （lcWrapper 对象），并且使用当前照相机设置填充浮出控件。

```CSharp
public void Initialize(CameraSettingsActivatedEventArgs args)
{
    videoDevController = (VideoDeviceController)args.VideoDeviceController;

    if (args.VideoDeviceExtension != null)
    {
        lcWrapper = new WinRTComponent();
        lcWrapper.Initialize(args.VideoDeviceExtension);
    }

    bool bAuto = false;
    double value = 0.0;

    if (videoDevController.Brightness.Capabilities.Step != 0)
    {
        slBrt.Minimum = videoDevController.Brightness.Capabilities.Min;
        slBrt.Maximum = videoDevController.Brightness.Capabilities.Max;
        slBrt.StepFrequency = videoDevController.Brightness.Capabilities.Step;
        videoDevController.Brightness.TryGetValue(out value);
        slBrt.Value = value;
    }
    else
    {
        slBrt.IsEnabled = false;
    }
    if (videoDevController.Brightness.Capabilities.AutoModeSupported)
    {
        videoDevController.Brightness.TryGetAuto(out bAuto);
        tsBrtAuto.IsOn = bAuto;
    }
    else
    {
        tsBrtAuto.IsOn = false;
        tsBrtAuto.IsEnabled = false;
    }

    if (videoDevController.Contrast.Capabilities.Step != 0)
    {
        slCrt.Minimum = videoDevController.Contrast.Capabilities.Min;
        slCrt.Maximum = videoDevController.Contrast.Capabilities.Max;
        slCrt.StepFrequency = videoDevController.Contrast.Capabilities.Step;
        videoDevController.Contrast.TryGetValue(out value);
        slCrt.Value = value;
    }
    else
    {
        slCrt.IsEnabled = false;
    }
    // . . .
    // . . .
    // . . .
```

照相机的驱动程序中演示 MFT[驱动程序 MFT](https://go.microsoft.com/fwlink/p/?LinkID=251566)示例。 有关照相机的驱动程序 Mft 的详细信息，请参阅[创建照相机驱动程序 MFT](creating-a-camera-driver-mft.md)。

## <a name="step-5-apply-changes"></a>步骤 5：应用更改

Changed 事件的相应的控件时对浮出控件上的控件进行了更改，用于将所做的更改应用于视频设备控制器 （videoDevController 对象） 和照相机驱动程序 MFT （lcWrapper 对象）。

此示例显示了将更改应用于视频设备控制器和照相机驱动程序 MFT，已更改方法，按它们出现在**DeviceAppPage.xaml.cs**文件。

```CSharp
protected void OnBrtAutoToggleChanged(object sender, RoutedEventArgs e)
{
    videoDevController.Brightness.TrySetAuto(tsBrtAuto.IsOn);
    slBrt.IsEnabled = !tsBrtAuto.IsOn;
}

protected void OnBrtSliderValueChanged(object sender, RoutedEventArgs e)
{
    videoDevController.Brightness.TrySetValue(slBrt.Value);
}

protected void OnCrtAutoToggleChanged(object sender, RoutedEventArgs e)
{
    videoDevController.Contrast.TrySetAuto(tsCrtAuto.IsOn);
    slCrt.IsEnabled = !tsCrtAuto.IsOn;
}

protected void OnCrtSliderValueChanged(object sender, RoutedEventArgs e)
{
    videoDevController.Contrast.TrySetValue(slCrt.Value);
}

protected void OnFocusAutoToggleChanged(object sender, RoutedEventArgs e)
{
    videoDevController.Focus.TrySetAuto(tsFocusAuto.IsOn);
    slFocus.IsEnabled = !tsFocusAuto.IsOn;
}

protected void OnFocusSliderValueChanged(object sender, RoutedEventArgs e)
{
    videoDevController.Focus.TrySetValue(slFocus.Value);
}

protected void OnExpAutoToggleChanged(object sender, RoutedEventArgs e)
{
    videoDevController.Exposure.TrySetAuto(tsExpAuto.IsOn);
    slExp.IsEnabled = !tsExpAuto.IsOn;
}

protected void OnExpSliderValueChanged(object sender, RoutedEventArgs e)
{
    videoDevController.Exposure.TrySetValue(slExp.Value);
}

protected void OnEffectEnabledToggleChanged(object sender, RoutedEventArgs e)
{
    if (tsEffectEnabled.IsOn)
    {
        lcWrapper.Enable();
    }
    else
    {
        lcWrapper.Disable();
    }
    slEffect.IsEnabled = tsEffectEnabled.IsOn;
}

protected void OnEffectSliderValueChanged(object sender, RoutedEventArgs e)
{
    lcWrapper.UpdateDsp(Convert.ToInt32(slEffect.Value));
}
```

## <a name="testing-your-app"></a>测试您的应用程序

本部分介绍如何安装 UWP 设备应用提供的自定义浮出控件**更多选项**的照相机，如中所示[UWP 用于相机的设备应用程序](https://go.microsoft.com/fwlink/p/?LinkID=227865)示例。

你可以测试 UWP 设备应用之前，它必须链接到您的照相机使用设备元数据。

- 需要打印机的位置，若要向其中添加设备应用信息的设备元数据包的副本。 如果没有设备元数据，您可以使用生成它**设备元数据创建向导**主题中所述[创建 UWP 设备应用的设备元数据](https://go.microsoft.com/fwlink/p/?LinkId=313644)。

    > [!NOTE]
    > 若要使用**设备元数据创建向导**，则必须安装 Microsoft Visual Studio Professional，Microsoft Visual Studio Ultimate，或[独立 SDK 的 Windows 8.1](https://go.microsoft.com/fwlink/p/?linkid=309209)，完成之前本主题中的步骤。 安装 Microsoft Visual Studio Express 的 Windows 安装不包括在向导的 sdk 版本。

以下步骤生成您的应用程序并安装设备元数据。

1. 启用测试签名。
    1. 启动**设备元数据创建向导**从 *%programfiles （x86） %*\\Windows 工具包\\8.1\\bin\\x86，通过双击**DeviceMetadataWizard.exe**
    2. 从**工具**菜单中，选择**启用测试签名**。

2. 重新启动计算机
3. 通过打开解决方案 (.sln) 文件生成解决方案。 按 F7，或转至**生成-&gt;生成解决方案**从顶部菜单中加载示例之后。

4. 断开连接并卸载打印机。 此步骤是必需的以便 Windows 将在下一次检测到设备读取更新的设备元数据。
5. 编辑并保存设备元数据。 要链接到你的设备的设备应用，必须将设备应用与你的设备进行关联。
    > [!NOTE]
    > 如果尚未创建设备元数据，请参阅[创建 UWP 设备应用的设备元数据](https://go.microsoft.com/fwlink/p/?LinkId=313644)。

    1. 如果**设备元数据创建向导**未打开，启动从 *%programfiles （x86） %*\\Windows 工具包\\8.1\\bin\\x86，也可由双击**DeviceMetadataWizard.exe**。
    2. 单击**编辑设备元数据**。 这样就可以编辑现有的设备元数据包。
    3. 在中**打开**对话框框中，找到与 UWP 设备应用程序相关联的设备元数据包。 (它具有**devicemetadata ms**文件扩展名。)
    4. 上**指定 UWP 设备应用信息**页上，输入中的 Microsoft Store 应用信息**UWP 设备应用**框。 单击**导入 UWP 应用程序清单文件**自动输入**包名称**，**发布服务器的名称**，以及**UWP 应用程序 ID**。
    5. 完成后，单击**下一步**直至到达**完成**页。
    6. 上**查看设备元数据包**页面上，确保所有设置都正确，然后选择**复制到本地计算机上的元数据存储设备元数据包**复选框。 然后单击**保存**。

6. 重新连接你的设备，以便在设备连接时，该 Windows 读取更新的设备元数据。
    - 如果有外部照相机，则只需将照相机连接。
    - 如果你有内部照相机，刷新 PC 设备和打印机文件夹中。 使用设备管理器扫描检测硬件改动。 检测到设备时，Windows 应读取更新的元数据。

> [!NOTE]
> 有关安装摄像头驱动程序 MFT 的信息，请参阅中的测试部分[创建照相机驱动程序 MFT](creating-a-camera-driver-mft.md)。

## <a name="testing-the-samples"></a>测试示例

若要测试相机选项体验，请首先下载这些示例：

- [用于相机示例的 UWP 设备应用程序](https://go.microsoft.com/fwlink/p/?LinkID=227865)
- [相机捕捉 UI 示例](https://go.microsoft.com/fwlink/p/?linkid=228589)
- [驱动程序 MFT 示例](https://go.microsoft.com/fwlink/p/?LinkID=251566)

然后，按照示例测试上提供的说明进行操作[驱动程序 MFT 示例](https://go.microsoft.com/fwlink/p/?LinkID=251566)页。
