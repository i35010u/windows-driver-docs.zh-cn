---
title: 如何使用 UWP 设备应用自定义相机选项
description: 在 Windows 8.1 中，UWP 设备应用允许设备制造商自定义在某些照相机应用中显示更多相机选项的弹出窗口。
ms.assetid: 4BA34A3F-3C0D-4DDC-BA0A-E62AE9A6A93A
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ae77300c18c19746fddb2729c2293001fbc42844
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91732967"
---
# <a name="how-to-customize-camera-options-with-a-uwp-device-app"></a>如何使用 UWP 设备应用自定义相机选项

在 Windows 8.1 中，UWP 设备应用允许设备制造商自定义在某些照相机应用中显示更多相机选项的弹出窗口。 本主题介绍了 CameraCatureUI API 显示的 " **更多选项** " 弹出窗口，并演示了 c # 版本的 [UWP 设备应用程序](/samples/browse/) 示例如何使用自定义浮出控件替换默认浮出控件。 若要详细了解 UWP 设备应用的详细信息，请参阅了解 [uwp 设备应用](meet-uwp-device-apps.md)。

> [!NOTE]
> 在 Windows 8.1 中，内置相机应用不显示 **更多选项** 按钮，因此无法显示 UWP 设备应用以显示更多相机选项。 但是， [CameraCaptureUI 类](/uwp/api/Windows.Media.Capture.CameraCaptureUI)（可用于所有 UWP 应用）有一个 " **更多选项** " 按钮，可以显示 uwp 设备应用。

适用于 [照相机的 UWP 设备应用](/samples/browse/) 示例的 c # 版本使用 **DeviceAppPage** 页来演示自定义浮出控件的 UI，以获取更多相机选项。 该示例还使用照相机驱动程序 MFT (media foundation 转换) 来应用照相机效果。 有关此方面的详细信息，请参阅 [创建照相机驱动程序 MFT](creating-a-camera-driver-mft.md)。

> [!NOTE]
> 本主题中所示的代码示例基于 [适用于照相机的 UWP 设备应用](/samples/browse/) 示例的 c # 版本。 此示例在 JavaScript 和 c + + 中也可用。 下载示例以查看最新版本的代码。

## <a name="more-options-for-cameras"></a>相机的更多选项

相机选项的更多经验在于，当其他应用程序（UWP 应用）使用 [CameraCaptureUI](/uwp/api/Windows.Media.Capture.CameraCaptureUI) API 从相机捕获或预览视频时，uwp 设备应用提供此功能。 可以通过 "相机选项" 窗口中的 " **更多选项** " 链接来访问它。 它不是全屏显示，而是在弹出窗口中显示，它是一个用于显示轻型的上下文用户界面的控件，当用户单击或点击它时，该界面会被消除。

此体验可用于突出显示照相机的特色功能，如应用自定义视频效果的功能。

如果没有为相机安装 UWP 设备应用，Windows 将提供默认的相机选项体验。 如果 Windows 检测到已为照相机安装了 UWP 设备应用，并且该应用已选择使用 `windows.cameraSettings` 扩展，则应用会替换 Windows 提供的默认体验。

若要调用浮出控件以获取更多相机选项：

1. 使用 [CameraCaptureUI](/uwp/api/Windows.Media.Capture.CameraCaptureUI) API 打开一个 UWP 应用 ([CameraCaptureUI 示例](/samples/browse/)，例如) 
2. 点击 UI 中的 " **选项** " 按钮
3. 这将打开 " **相机选项** " 弹出窗口，其中显示了用于设置分辨率和视频抖动的基本选项
4. 在 "**相机选项**" 浮出控件上，点击 "**更多选项**"
5. " **更多选项** " 会打开
    - 如果未安装照相机的 UWP 设备应用，则会显示 *默认的弹出* 窗口
    - 当安装了照相机的 UWP 设备应用时，将显示 *自定义弹出* 窗口

![用于更多相机选项和自定义飞出的默认浮出控件的并排图像](images/372745-cameraoptionslaunching.png)

此图显示了 "自定义" 浮出控件示例旁边的 "其他相机选项" 的默认浮出控件。

## <a name="prerequisites"></a>先决条件

准备工作：

1. 设置开发 PC。 有关下载工具和创建开发人员帐户的信息[，请参阅入门。](getting-started.md)
2. 将应用与应用商店相关联。 请参阅 [创建 UWP 设备应用](step-1--create-a-uwp-device-app.md) 了解相关信息。
3. 为打印机创建将其与应用程序关联的设备元数据。 有关详细信息，请参阅 [创建设备元数据](step-2--create-device-metadata.md) 。
4. 构建应用程序主页的 UI。 所有 UWP 设备应用都可以从 "开始" 启动，它们将全屏显示。 使用 "开始体验" 以与设备的特定品牌和功能匹配的方式突出显示你的产品或服务。 它可以使用的 UI 控件类型没有任何特殊限制。 若要开始设计全屏体验，请参阅 [Microsoft Store 设计原则](https://go.microsoft.com/fwlink/p/?LinkID=299845)。

## <a name="step-1-register-the-extension"></a>步骤1：注册扩展

为了使 Windows 能够识别应用程序可以为更多相机选项提供自定义浮出控件，它必须注册照相机设置扩展。 此扩展在元素中声明 `Extension` ， `Category` 特性设置为的值 `windows.cameraSettings` 。 在 c # 和 c + + 示例中， `Executable` 特性设置为 `DeviceAppForWebcam.exe` ， `EntryPoint` 特性设置为 `DeviceAppForWebcam.App` 。

可以在 Microsoft Visual Studio 中的清单设计器的 " **声明** " 选项卡上添加 "相机设置" 扩展。 你还可以使用 XML (文本) 编辑器手动编辑应用包清单 XML。 右键单击**解决方案资源管理器**中的**appxmanifest.xml**文件以编辑选项。

此示例显示元素中的相机设置扩展 `Extension` ，因为它显示在应用包清单文件 **appxmanifest.xml**中。

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

## <a name="step-2-build-the-ui"></a>步骤2：生成 UI

在构建你的应用程序之前，你应与你的设计人员和营销团队合作来设计用户体验。 用户体验应投影公司的品牌方面，并帮助你建立与用户的连接。

### <a name="design-guidelines"></a>设计准则

在设计自定义浮出控件之前，请务必查看 [UWP 应用飞出指南](/windows/uwp/design/controls-and-patterns/dialogs-and-flyouts/) 。 本指南可帮助确保你的浮出控件提供与其他 UWP 应用一致的直观体验。

在应用程序的主页上，请记住，Windows 8.1 可以在单个监视器上以各种大小显示多个应用。 请参阅以下准则，详细了解应用程序如何在屏幕大小、窗口大小和方向之间进行适当的重新排列。

- [窗口大小和屏幕缩放的准则](https://go.microsoft.com/fwlink/p/?LinkId=311830)
- [将窗口调整为高度和缩小布局的准则](/previous-versions/windows/hh465371(v=win.10))

### <a name="flyout-dimensions"></a>飞出尺寸

显示更多相机选项的浮出控件的高度为625像素，宽为340像素。 在顶部包含 " **更多选项** " 文本的区域由 Windows 提供，约为65像素，为自定义飞出的可查看区域保留560像素。 自定义浮出控件的宽度不应超过340像素。

![更多相机选项的飞出尺寸。](images/372776-camera-options-layout.png)

> [!NOTE]
> 如果自定义浮出控件的高度超过560像素，则用户可以滑动或滚动查看可查看区域上方或下方的弹出窗口部分。

### <a name="suggested-effects"></a>建议的效果

- 颜色效果。 例如，灰度、棕色色调或 solarizing 整个图片。
- 面部跟踪效果。 在图片中识别人脸并在其顶部添加覆盖物，如帽子或一对眼镜。
- 场景模式。 这些是针对不同照明条件的预设曝光和焦点模式。

### <a name="suggested-settings"></a>建议的设置

- UWP 设备应用的自定义浮出控件可以提供开关来启用硬件实现的设置，如制造商提供的颜色校正方案。
- 实现基本属性来补充 UWP 设备应用公开的其他设置。 例如，许多设备可能会公开控制以调整亮度、对比度、闪烁、焦点和曝光度，但实现 "自动调整亮度和对比度" 的 "自动调整亮度和对比度" 的设备可能不需要提供这些设置。

### <a name="restrictions"></a>限制

- 不要通过在应用未进行 `CameraOptionsUI.Show` 流式处理或捕获时调用方法) ，从主应用 (打开 UWP 设备应用的自定义弹出窗口。

- 不要提供预览，或以其他方式从 UWP 设备应用的自定义浮出控件中取得视频流的所有权。 自定义飞出旨在充当捕获视频的其他应用。 捕获应用具有视频流的所有权。 不应尝试使用低级别 Api 访问视频流。 这可能会导致意外的行为，而捕获应用会失去对流的访问权限。

- 不要在自定义浮出控件中调整分辨率。

- 不要尝试在用于自定义浮出控件的区域之外显示弹出窗口、通知或对话框。 不允许使用这些类型的对话框。

- 不要在自定义浮出控件内启动音频或视频捕获。 自定义弹出窗口旨在扩展正在捕获视频的其他应用，而不是启动捕获本身。 此外，捕获音频或视频可能会触发系统对话框，并且不允许在自定义浮出控件内使用弹出式对话框。

## <a name="step-3-handle-activation"></a>步骤3：处理激活

如果你的应用已声明照相机设置扩展，则它必须实现一个 `OnActivated` 方法来处理应用激活事件。 当 UWP 应用使用 [CameraCaptureUI](/uwp/api/Windows.Media.Capture.CameraCaptureUI) 类调用 [CameraOptionsUI](/uwp/api/Windows.Media.Capture.CameraOptionsUI) 方法时，将触发此事件。 应用程序激活是指当应用程序启动时，应用程序可以选择要启动的页面。 对于声明了照相机设置扩展的应用程序，Windows 会将视频设备传递到激活的事件参数： Windows.applicationmodel.resources.core. IActivatedEventArgs。

UWP 设备应用可以确定激活适用于照相机设置 (如果某个人只是在 "**相机选项**" 对话框) 了**更多选项**，则当事件参数的 `kind` 属性等于 windows.applicationmodel.resources.core. CameraSettings。

此示例显示方法中的激活事件处理程序 `OnActivated` ，如 **App.xaml.cs** 文件中所示。 然后，将事件参数强制转换为 CameraSettingsActivatedEventArgs，并将其发送到 `Initialize` 自定义浮出控件 (**DeviceAppPage.xaml.cs**) 的方法。

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

## <a name="step-4-control-settings-and-effects"></a>步骤4：控制设置和效果

在 `Initialize` 调用自定义弹出窗口 (**DeviceAppPage.xaml.cs**) 的方法时，视频设备将通过事件参数传递到浮出控件。 这些参数公开用于控制照相机的属性：

- **参数。VideoDeviceController**属性提供 VideoDeviceController 类型的对象。 此对象提供用于调整标准设置的方法。
- **参数。VideoDeviceExtension**属性是指向照相机驱动程序 MFT 的指针。 如果未公开任何驱动程序 MFT 接口，此属性将为 null。 有关相机驱动程序 MFTs 的详细信息，请参阅 [创建照相机驱动程序 MFT](creating-a-camera-driver-mft.md)。

此示例显示方法的一部分 `Initialize` ，如 **DeviceAppPage.xaml.cs** 文件中所示。 在这里，视频设备控制器 (videoDevController 对象) ，并且创建了照相机驱动程序 MFT (lcWrapper 对象) ，并填充了当前相机设置。

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

[驱动程序 mft](/samples/browse/)示例演示了照相机驱动程序 mft。 有关相机驱动程序 MFTs 的详细信息，请参阅 [创建照相机驱动程序 MFT](creating-a-camera-driver-mft.md)。

## <a name="step-5-apply-changes"></a>步骤5：应用更改

对浮出控件上的控件进行更改时，相应控件的 Changed 事件用于将更改应用于视频设备控制器 (videoDevController 对象) ，照相机驱动程序 MFT (lcWrapper 对象) 。

此示例显示将更改应用于视频设备控制器和照相机驱动程序 MFT 的已更改方法，因为它们显示在 **DeviceAppPage.xaml.cs** 文件中。

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

## <a name="testing-your-app"></a>测试应用程序

本部分介绍如何安装 UWP 设备应用，该应用为相机的 **更多选项** 提供自定义浮出控件，如 [照相机设备应用程序](/samples/browse/) 示例中所示。

在可以测试 UWP 设备应用之前，必须使用设备元数据将其链接到相机。

- 你需要打印机的设备元数据包的副本，以便向其添加设备应用信息。 如果没有设备元数据，可以使用 **设备元数据创作向导** 生成它，如主题为 [UWP 设备应用创建设备元数据](./step-2--create-device-metadata.md)中所述。

    > [!NOTE]
    > 若要使用 **设备元数据创作向导**，在完成本主题中的步骤之前，必须安装 Microsoft Visual Studio Professional、Microsoft Visual Studio Ultimate 或 [独立的 SDK for Windows 8.1](https://go.microsoft.com/fwlink/p/?linkid=309209)。 为 Windows 安装 Microsoft Visual Studio Express 会安装不包括向导的 SDK 版本。

以下步骤生成应用并安装设备元数据。

1. 启用测试签名。
    1. 双击 "DeviceMetadataWizard.exe，从 *% ProgramFiles (x86) %* Windows 工具包 8.1 bin **X86 启动设备元数据创作向导** \\ \\ \\ \\ **DeviceMetadataWizard.exe**
    2. 从 " **工具** " 菜单中，选择 " **启用测试签名**"。

2. 重新启动计算机
3. 通过打开解决方案 ( .sln) 文件来生成解决方案。 加载示例后，按 F7 或从顶部菜单中转到 " **生成- &gt; 生成解决方案** "。

4. 断开连接并卸载打印机。 此步骤是必需的，以便 Windows 将在下一次检测到设备时读取更新的设备元数据。
5. 编辑并保存设备元数据。 若要将设备应用链接到设备，你必须将设备应用关联到设备。
    > [!NOTE]
    > 如果尚未创建设备元数据，请参阅 [为 UWP 设备应用创建设备元数据](./step-2--create-device-metadata.md)。

    1. 如果**设备元数据创作向导**尚未打开，请通过双击 "DeviceMetadataWizard.exe" 从 *% ProgramFiles (x86) %* \\ Windows 工具包 \\ 8.1 \\ bin \\ x86 **DeviceMetadataWizard.exe**启动它。
    2. 单击 " **编辑设备元数据**"。 这将允许你编辑现有的设备元数据包。
    3. 在 " **打开** " 对话框中，找到与 UWP 设备应用关联的设备元数据包。  (其文件扩展名为 **devicemetadata** 。 ) 
    4. 在 " **指定 uwp 设备应用信息** " 页上，在 " **UWP 设备应用** " 框中输入 Microsoft Store 应用信息。 单击 " **导入 UWP 应用程序清单文件** " 以自动输入 **包名称**、 **发布者名称**和 **UWP 应用 ID**。
    5. 完成后，单击 " **下一步** "，直到到达 " **完成** " 页。
    6. 在 " **查看设备元数据包** " 页上，确保所有设置均正确，并选中 "将 **设备元数据包复制到本地计算机上的元数据存储区** " 复选框。 然后单击“保存”  。

6. 重新连接设备，以便 Windows 在连接设备时读取更新的设备元数据。
    - 如果有外置相机，只需连接相机即可。
    - 如果有内部照相机，请在 "设备和打印机" 文件夹中刷新 PC。 使用设备管理器扫描硬件更改。 检测到设备时，Windows 应读取更新的元数据。

> [!NOTE]
> 有关安装照相机驱动程序 MFT 的信息，请参阅 [创建照相机驱动程序 mft](creating-a-camera-driver-mft.md)中的 "测试" 部分。

## <a name="testing-the-samples"></a>测试示例

若要测试相机选项体验，请先下载以下示例：

- [适用于照相机的 UWP 设备应用示例](/samples/browse/)
- [相机捕获 UI 示例](/samples/browse/)
- [驱动程序 MFT 示例](/samples/browse/)

然后，按照 " [驱动程序 MFT 示例](/samples/browse/) " 页上提供的示例测试说明进行操作。