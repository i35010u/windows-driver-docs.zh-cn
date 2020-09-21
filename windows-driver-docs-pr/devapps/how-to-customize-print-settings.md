---
title: '如何自定义 (UWP 设备应用的打印设置) '
description: '本主题介绍 "高级打印设置" 浮出控件，并演示 c # 版本的 "打印设置" 和 "打印通知" 示例如何使用自定义浮出控件替换默认浮出控件。'
ms.assetid: 099BD9B2-1AA6-49A5-AB84-0AF6FA0EFB26
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 30e2ea5b9c8882d80cd41ef205a6c7e7cd04d336
ms.sourcegitcommit: 366a15d68eb58d01a8ca6de7b982f62ac8b7deaf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/19/2020
ms.locfileid: "90811964"
---
# <a name="how-to-customize-print-settings-uwp-device-apps"></a>如何自定义 (UWP 设备应用的打印设置) 

在 Windows 8.1 中，UWP 设备应用允许打印机制造商自定义显示高级打印设置的浮出控件。 本主题介绍 "高级打印设置" 浮出控件，并演示 c # 版本的 " [打印设置" 和 "打印通知](https://go.microsoft.com/fwlink/p/?LinkID=242862) " 示例如何使用自定义浮出控件替换默认浮出控件。 若要详细了解 UWP 设备应用的详细信息，请参阅了解 [uwp 设备应用](meet-uwp-device-apps.md)。

" [打印设置" 和 "打印通知](https://go.microsoft.com/fwlink/p/?LinkID=242862) " 示例的 c # 版本使用 " **首选项 .xaml** " 页演示高级打印设置的自定义浮出控件的 UI。 打印帮助程序类用于创建设备上下文 (IPrinterExtensionContext) 并执行设备查询。 **PrinterHelperClass.cs**文件在**DeviceAppForPrintersLibrary**项目中，并使用**PrinterExtensionLibrary**项目中定义的 api。 打印机扩展库提供了一种便捷的方式来访问 v4 打印驱动程序的打印机扩展接口。 有关详细信息，请参阅 [打印机扩展库概述](printer-extension-library-overview.md)。

>[!NOTE]
>本主题中所示的代码示例基于 c # 版本的 [打印设置和打印通知](https://go.microsoft.com/fwlink/p/?LinkID=242862) 示例。 此示例在 JavaScript 和 c + + 中也可用。 请注意，由于 c + + 可以直接访问 COM，因此该示例的 c + + 版本不包括代码库项目。 下载示例以查看最新版本的代码。

## <a name="advanced-print-settings"></a>高级打印设置

高级打印设置体验是指当用户想要选择 "打印" 窗口中未提供的打印设置时打印机提供的功能。 可以通过 "打印" 窗口中的 " **其他设置** " 链接来访问它。 它不是全屏体验，但在弹出窗口中显示，它是一个控件，用于显示在用户单击或点击它时消除的轻型上下文用户界面。

这种体验可用于突出显示打印机的不同功能，如将水印应用于文档页面、提供安全打印选项或图像增强选项的功能。

当未为打印机安装 UWP 设备应用时，Windows 将提供默认的打印设置体验。 如果 Windows 检测到已为你的打印机安装了 UWP 设备应用，并且该应用已选择 `windows.printTaskSettings` 扩展，则你的应用将替换 Windows 提供的默认体验。

若要为高级打印设置调用浮出控件：

1. 打开支持打印的 UWP 应用
2. 在屏幕右侧 (或使用 Windows 徽标键 + C) 访问超级按钮。
3. 点击 " **设备** " 超级按钮
4. 点击 **打印**
5. 点击打印机
6. " **打印** " 窗口打开
7. 单击 "**打印**" 窗口上的 "**其他设置**" 链接
8. "高级打印设置" 浮出控件随即打开
   - 未安装打印机的 UWP 设备应用时，将显示 *默认的弹出* 窗口
   - 当安装了打印机的 UWP 设备应用时，将显示 *自定义弹出* 窗口

![高级打印设置的默认和自定义浮出控件的示例。](images/373072-printer-settings-launch.png)

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

## <a name="step-1-register-the-extension"></a>步骤1：注册扩展

为了使 Windows 能够识别应用程序可以为高级打印设置提供自定义浮出控件，它必须注册 "打印任务" 设置扩展。 此扩展在元素中声明 `Extension` ， `Category` 特性设置为的值 `windows.printTaskSettings` 。 在 c # 和 c + + 示例中， `Executable` 特性设置为 `$targetnametoken$.exe` ， `EntryPoint` 特性设置为 `DeviceAppForPrinters.App` 。

可以在 Microsoft Visual Studio 中的清单设计器的 " **声明** " 选项卡上添加 "打印任务设置" 扩展。 你还可以使用 XML (文本) 编辑器手动编辑应用包清单 XML。 右键单击**解决方案资源管理器**中的**appxmanifest.xml**文件以编辑选项。

此示例显示元素中的 "打印任务设置" 扩展 `Extension` ，因为它显示在应用包清单文件 **appxmanifest.xml**中。

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
      <VisualElements DisplayName="Device App For Printers C# sample" Logo="Assets\squareTile-sdk.png" SmallLogo="Assets\smallTile-sdk.png" Description="DeviceAppForPrinters C# sample" ForegroundText="light" BackgroundColor="#00b2f0" ToastCapable="true">
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

## <a name="step-2-build-the-ui"></a>步骤2：生成 UI

在构建你的应用程序之前，你应与你的设计人员和营销团队合作来设计用户体验。 用户体验应投影公司的品牌方面，并帮助你建立与用户的连接。

### <a name="design-guidelines"></a>设计准则

在设计自定义浮出控件之前，请务必查看 [UWP 应用飞出指南](https://go.microsoft.com/fwlink/p/?LinkId=317078) 。 本指南可帮助确保你的浮出控件提供与其他 UWP 应用一致的直观体验。

在应用程序的主页上，请记住，Windows 8.1 可以在单个监视器上以各种大小显示多个应用。 请参阅以下准则，详细了解应用程序如何在屏幕大小、窗口大小和方向之间进行适当的重新排列。

- [窗口大小和屏幕缩放的准则](https://go.microsoft.com/fwlink/p/?LinkId=311830)
- [将窗口调整为高度和缩小布局的准则](https://go.microsoft.com/fwlink/p/?LinkId=311831)

### <a name="flyout-dimensions"></a>飞出尺寸

显示高级打印设置的浮出控件的宽度为646像素，且至少768像素 (实际高度取决于用户屏幕) 的分辨率。 弹出窗口标题区域中的 "后退" 按钮由 Windows 提供。 "应用标题" 文本是应用程序清单中的应用程序标题。 标题区域高度为80像素，为自定义浮出控件的可查看区域保留688像素。

![高级打印机设置的飞出尺寸。](images/439446-printer-options-layout.png)

>[!NOTE]
>如果自定义浮出控件的高度超过688像素，则用户可以滑动或滚动查看可查看区域上方或下方的弹出窗口部分。

### <a name="defining-the-app-title-color-and-icon"></a>定义应用程序标题颜色和图标

自定义弹出窗口中的标题、背景色、文本颜色和小徽标取自 `VisualElements` 应用包清单文件中的元素。

此示例显示了 `VisualElements` 应用包清单文件 () 中的元素中定义的标题和图标。 **Package.appxmanifest**

```XML
      <VisualElements DisplayName="Device App For Printers C# sample" Logo="Assets\squareTile-sdk.png" SmallLogo="Assets\smallTile-sdk.png" Description="DeviceAppForPrinters C# sample" ForegroundText="light" BackgroundColor="#00b2f0" ToastCapable="true">
        <DefaultTile ShowName="allLogos" ShortName="App4PrinterCS" WideLogo="Assets\tile-sdk.png" />
        <SplashScreen Image="Assets\splash-sdk.png" BackgroundColor="#00b2f0" />
      </VisualElements>
```

### <a name="best-practices"></a>最佳实践

- **保持相同的外观。** 将您的自定义浮出控件与入门体验的设计保持一致 (您的应用) 程序的主页面，包括字体、颜色和控件等元素。 无论用户在何处调用该应用，都应熟悉该应用。

- **保持交互简单。** 避免使用耗时或复杂的交互。 在大多数情况下，最好在启动体验内完成诸如设置打印机、查看状态、订购墨迹和故障排除等操作。

- **保持导航到最小值。** 避免使用户在自定义飞出的多个页面之间来回导航。 相反，请使用垂直滚动或内联控件，如渐进式公开控件、下拉控件和内联错误消息。

- **请勿使用浅消除浮出控件。** 打印体验已使用轻量 "取消" 弹出窗口。 在自定义浮出控件中包含另一个光源消除元素会使用户感到困惑。

- **禁用导致用户离开打印体验的链接。** 用户打印内容时，应采取措施确保它们保留在打印上下文中。 例如，如果你的应用程序具有可导致应用的其他区域的链接 (例如，到主页或用于购买墨迹) 的页面，则你应禁用这些链接，这样用户就不会意外退出高级打印设置体验。

## <a name="step-3-handle-activation"></a>步骤3：处理激活

如果你的应用已声明打印任务设置扩展，则它必须实现一个 `OnActivated` 方法来处理应用激活事件。 应用程序激活是指当应用程序启动时，应用程序可以选择要启动的页面。 对于已声明打印任务设置扩展的应用程序，Windows 将在激活的事件参数中传递打印任务扩展上下文： Windows.applicationmodel.resources.core. IActivatedEventArgs。

UWP 设备应用可以确定激活适用于高级打印设置 (如果某个人只是在 "打印设置" 对话框中点击了 **更多选项**) 则事件参数的 `kind` 属性等于 windows.applicationmodel.resources.core. printTaskSettings。

>[!NOTE]
>在某些情况下，如果用户在启动后立即关闭应用，则可能会在激活处理程序中引发异常。 为避免出现这种情况，请确保激活处理程序能够高效地完成，而不会占用大量资源。

此示例显示方法中的激活事件处理程序 `OnActivated` ，如 **Constants.cs** 文件中所示。 然后，将事件参数强制转换为 Windows.applicationmodel.resources.core. PrintTaskSettingsActivatedEventArgs。 尽管该示例在 **Constants.cs** 文件中包含此代码，但它实际上是在 **App.xaml.cs** 文件中定义的应用类的一部分。

```CSharp
partial class App : Application
{
    protected override void OnActivated(IActivatedEventArgs args)
    {
        if (args.Kind == ActivationKind.PrintTaskSettings)
        {
            Frame rootFrame = new Frame();
            if (null == Window.Current.Content)
            {
                rootFrame.Navigate(typeof(MainPage));
                Window.Current.Content = rootFrame;
            }
            Window.Current.Activate();

            MainPage mainPage = (MainPage)rootFrame.Content;

            // Load advanced printer preferences scenario
            mainPage.LoadAdvancedPrintSettingsContext((PrintTaskSettingsActivatedEventArgs)args);
        }
    }
}
```

## <a name="step-4-display-settings"></a>步骤4：显示设置

`LoadAdvancedPrintSettingsContext`调用方法时，打印任务配置上下文将分配给 MainPage 类的变量。 这将允许自定义浮出控件在启动时访问打印设置。

传递给方法的事件参数可 `LoadAdvancedPrintSettingsContext` 公开用于访问和控制打印机的属性：

- **args.configu**属性提供了类型为 PrintTaskConfiguration 的对象。 此对象提供对打印任务扩展上下文的访问权限，并且还允许您添加一个事件处理程序来更新打印票证。
- **args.configu. printerExtensionContext**属性提供了类型为 printerExtensionContext 的对象。 此对象是指向打印架构、PrintTicket 和打印队列信息的 PrinterExtensionLibrary 接口的指针。 如果未公开任何接口，则此值将为 null。 有关详细信息，请参阅 [打印机扩展库概述](printer-extension-library-overview.md)。

此示例显示了 `LoadAdvancedPrintSettingsContext` 方法，因为它显示在 **Constants.cs** 文件中。

```CSharp
public PrintTaskConfiguration Config;
public Object Context;

public void LoadAdvancedPrintSettingsContext(PrintTaskSettingsActivatedEventArgs args)
{
    Config = args.Configuration;
    Context = Config.PrinterExtensionContext;
    LoadScenario(typeof(DeviceAppForPrinters.Preferences));
}
```

在自定义飞出页 **Preferences.xaml.cs**上，名为的类 `rootPage` 充当指向 MainPage 类的指针，以便可以从弹出窗口中访问打印任务扩展上下文和打印机设备上下文。

此示例显示了 `Preferences` **Preferences.xaml.cs** 文件的类中的指针。 下载 " [打印设置" 和 "打印通知](https://go.microsoft.com/fwlink/p/?LinkID=242862) " 示例以查看完整代码。

```CSharp
public sealed partial class Preferences : SDKTemplate.Common.LayoutAwarePage
{
    // A pointer back to the main page.  
    MainPage rootPage = MainPage.Current;

    // To listen for save requests.
    PrintTaskConfiguration configuration;

    // To create the printer device context.
    Object printerExtensionContext;
    PrintHelperClass printHelper;

    // The features in this sample were chosen because they're available on a wide range of printer drivers.
    private string[] features = { "PageOrientation", "PageOutputColor", "PageMediaSize", "PageMediaType" };
    private string[] selections = { null, null, null, null };

    // . . .
    // . . .
    // . . .
```

调用 **Preferences.xaml.cs** 的页构造函数时，将为打印任务扩展上下文创建对象， (名为 `PrintTaskConfiguraton`) 的对象 `configuration` 和 (`PrintHelperClass` 名为) 的对象的打印机设备上下文 `printHelper` 。

创建这些对象后，将在方法中使用打印机设备上下文 `DisplaySettings` 来加载 textblock 和 ComboBoxs。 请注意，与 JavaScript 不同的是，所选内容的更改不会在应用程序的其他线程上触发。 您必须维护用户选择的本地缓存，以供以后使用。

此示例显示了 Preferences.xaml.cs 文件中的自定义飞出页构造函数、 `DisplaySettings` 和其他帮助器方法。 **Preferences.xaml.cs**

```CSharp
public Preferences()
{
    this.InitializeComponent();

    configuration = rootPage.Config;
    printerExtensionContext = rootPage.Context;
    printHelper = new PrintHelperClass(printerExtensionContext);

    // Disable scenario navigation by hiding the scenario list UI elements
    ((UIElement)rootPage.FindName("Scenarios")).Visibility = Windows.UI.Xaml.Visibility.Collapsed;
    ((UIElement)rootPage.FindName("ScenarioListLabel")).Visibility = Windows.UI.Xaml.Visibility.Collapsed;
    ((UIElement)rootPage.FindName("DescriptionText")).Visibility = Windows.UI.Xaml.Visibility.Collapsed;

    DisplaySettings();
}


private void DisplaySettings(bool constraints=false)
{
    PrintOptions.Visibility = Windows.UI.Xaml.Visibility.Visible;
    WaitPanel.Visibility = Windows.UI.Xaml.Visibility.Collapsed;

    // Fill in the drop-down select controls for some common printing features.
    TextBlock[] featureLabels = { PageOrientationLabel, PageOutputColorLabel, PageMediaSizeLabel, PageMediaTypeLabel };
    ComboBox[] featureBoxes = { PageOrientationBox, PageOutputColorBox, PageMediaSizeBox, PageMediaTypeBox };

    for (int i = 0; i < features.Length; i++)
    {
        // Only display a feature if it exists
        featureLabels[i].Visibility = Windows.UI.Xaml.Visibility.Collapsed;
        featureBoxes[i].Visibility = Windows.UI.Xaml.Visibility.Collapsed;

        string feature = features[i];

        // Check whether the currently selected printer's capabilities include this feature.
        if (!printHelper.FeatureExists(feature))
        {
            continue;
        }

        // Fill in the labels so that they display the display name of each feature.
        featureLabels[i].Text = printHelper.GetFeatureDisplayName(feature);
        string[] index = printHelper.GetOptionInfo(feature, "Index");
        string[] displayName = printHelper.GetOptionInfo(feature, "DisplayName");
        string selectedOption = printHelper.GetSelectedOptionIndex(feature);

        // Unless specified, do not get constraints
        bool[] constrainedList = constraints ? printHelper.GetOptionConstraints(feature) : new bool[index.Length];

        // Populate the combo box with the options for the current feature.
        PopulateBox(featureBoxes[i], index, displayName, selectedOption, constrainedList);
        selections[i] = selectedOption;

        // Every time the selection for a feature changes, we update our local cached set of selections.
        featureBoxes[i].SelectionChanged += OnFeatureOptionsChanged;

        // Show existing features
        featureLabels[i].Visibility = Windows.UI.Xaml.Visibility.Visible;
        featureBoxes[i].Visibility = Windows.UI.Xaml.Visibility.Visible;
    }
}

void PopulateBox(ComboBox box, string[] index, string[] displayName, string selectedOption, bool[] constrainedList)
{
    // Clear the combobox of any options from previous UI refresh before repopulating it.
    box.SelectionChanged -= OnFeatureOptionsChanged;
    box.Items.Clear();
    // There should be only one displayName for each possible option.
    if (index.Length == displayName.Length)
    {
        for (int i = 0; i < index.Length; i++)
        {
            // Create a new DisplayItem so the user will see the friendly displayName instead of the index.
            ComboBoxItem newItem = new ComboBoxItem();
            newItem.Content = displayName[i];
            newItem.DataContext = index[i];
            newItem.Foreground = constrainedList[i] ? new SolidColorBrush(Colors.Red) : new SolidColorBrush(Colors.Black);
            box.Items.Add(newItem);

            // Display current selected option as selected in the combo box.
            if (selectedOption == index[i])
            {
                box.SelectedIndex = i;
                box.Foreground = newItem.Foreground;
            }
        }
    }
}

private void OnFeatureOptionsChanged(object sender, SelectionChangedEventArgs args)
{
    ComboBox comboBox = sender as ComboBox;

    for (int i = 0; i < features.Length; i++)
    {
        if (features[i] + "Box" == comboBox.Name)
        {
            selections[i] = (comboBox.SelectedItem as ComboBoxItem).DataContext as string;
        }
    }
}
```

## <a name="step-5-save-settings"></a>步骤5：保存设置

当用户完成设置高级打印设置时，Microsoft Store 设备应用需要在用户返回到 " **打印** " 窗口之前保存更改。 若要执行此操作，应用程序需要在用户点击 " **后退** " 按钮时从自定义弹出页面)  (进行侦听。 发生这种情况时，将 `SaveRequested` 触发打印任务扩展上下文 (`configuration` 对象) 的事件。

此示例显示了的事件侦听器 `SaveRequested` ，它是在 `OnNavigatedTo` **Preferences.xaml.cs** 文件中的自定义浮出控件的事件处理程序中添加的。 `SaveRequested`触发事件时， `OnSaveRequested` 将调用方法， (该方法也**Preferences.xaml.cs**文件中) 。

```CSharp
protected override void OnNavigatedTo(NavigationEventArgs e)
{
    if (null == configuration)
    {
        rootPage.NotifyUser("Configuration arguments cannot be null", NotifyType.ErrorMessage);
        return;
    }

    // Add an event listener for saverequested (the back button of the flyout is pressed).
    configuration.SaveRequested += OnSaveRequested;
}
```

在 `OnSaveRequested` 方法中，应用程序首先使用 `printHelper` 对象为打印机扩展上下文上的每个功能设置当前选定的选项。 然后，它对 `Save` `request` 作为参数传递给方法的对象调用方法 `OnSaveRequested` 。 `Save`PrintTaskConfigurationSaveRequest 类中的方法使用打印机扩展上下文来验证打印票证，并保存打印任务配置（& e）。

>[!IMPORTANT]
>如果打印票证以任何方式无效，则该 `Save` 方法将引发应用程序必须处理的异常。 如果应用程序不处理此异常，则会停止流，并强制用户停止弹出窗口并重新启动打印流。

此示例显示了 `OnSaveRequested` **Preferences.xaml.cs** 文件中的方法。 由于 `SaveRequested` 事件不是在 ui 线程上引发的，因此它需要使用 CoreDispatcher 将消息发布到 UI 线程，以便在验证和保存票证时显示相应的消息。

```CSharp
async private void OnSaveRequested(object sender, PrintTaskConfigurationSaveRequestedEventArgs args)
{
    if (null == printHelper || null == printerExtensionContext || null == args)
    {
        await Dispatcher.RunAsync(Windows.UI.Core.CoreDispatcherPriority.Normal, () =>
        {
            rootPage.NotifyUser("onSaveRequested: args, printHelper, and context cannot be null", NotifyType.ErrorMessage);
        });
        return;
    }

    // Get the request object, which has the save method that allows saving updated print settings.
    PrintTaskConfigurationSaveRequest request = args.Request;

    if (null == request)
    {
        await Dispatcher.RunAsync(Windows.UI.Core.CoreDispatcherPriority.Normal, () =>
        {
            rootPage.NotifyUser("onSaveRequested: request cannot be null", NotifyType.ErrorMessage);
        });
        return;
    }

    PrintTaskConfigurationSaveRequestedDeferral deferral = request.GetDeferral();

    // Two separate messages are dispatched to:
    // 1) put up a popup panel,
    // 2) set the each options to the print ticket and attempt to save it,
    // 3) tear down the popup panel if the print ticket could not be saved.
    await Dispatcher.RunAsync(Windows.UI.Core.CoreDispatcherPriority.Normal, () =>
    {
        PrintOptions.Visibility = Windows.UI.Xaml.Visibility.Collapsed;
        WaitPanel.Visibility = Windows.UI.Xaml.Visibility.Visible;
    });

    // Go through all the feature select elements, look up the selected
    // option name, and update the context
    // for each feature
    for (var i = 0; i < features.Length; i++)
    {
        // Set the feature's selected option in the context's print ticket.
        // The printerExtensionContext object is updated with each iteration of this loop
        printHelper.SetFeatureOption(features[i], selections[i]);
    }

    bool ticketSaved;
    try
    {
        // This save request will throw an exception if ticket validation fails.
        // When the exception is thrown, the app flyout will remain.
        // If you want the flyout to remain regardless of outcome, you can call
        // request.Cancel(). This should be used sparingly, however, as it could
        // disrupt the entire the print flow and will force the user to
        // light dismiss to restart the entire experience.
        request.Save(printerExtensionContext);

        if (configuration != null)
        {
            configuration.SaveRequested -= OnSaveRequested;
        }
        ticketSaved = true;
    }
    catch (Exception exp)
    {
        // Check if the HResult from the exception is from an invalid ticket, otherwise rethrow the exception
        if (exp.HResult.Equals(unchecked((int)0x8007000D))) // E_INVALID_DATA
        {
            ticketSaved = false;
        }
        else
        {
            throw;
        }
    }

    // If ticket isn't saved, refresh UI and notify user
    if (!ticketSaved)
    {
        await Dispatcher.RunAsync(Windows.UI.Core.CoreDispatcherPriority.Normal, () =>
        {
            rootPage.NotifyUser("Failed to save the print ticket", NotifyType.ErrorMessage);
            DisplaySettings(true);
        });
    }
    deferral.Complete();
}
```

### <a name="saving-options-that-require-user-input"></a>正在保存需要用户输入的选项

" [打印设置和打印通知](https://go.microsoft.com/fwlink/p/?LinkID=242862) " 示例演示如何设置定义的功能，这些功能涵盖大多数打印选项。 但是，某些选项需要自定义 UI 才能获取用户指定的值。 例如，如果应用使用 "高级打印" 设置来指定自定义页面大小，则需要执行以下步骤来保存用户指定的值：

1. 在应用程序激活过程中检索打印票证。 [步骤3：处理激活](#step-3-handle-activation)中前面介绍了 "打印设置" 应用程序激活。

2. 检查是否指定了 "页面大小" 选项。 在 c # 或 JS 应用程序中，print helper 类可以检查此选项。 在 c + + 应用程序中，对 IPrintSchemaOption 调用 QueryInterface 以检索 IPrintSchemaPageMediaSizeOption。

    此示例显示了打印帮助程序类中的一个方法，用于检查是否指定了 "页面大小" 选项。

    ```CSharp
    public bool ShouldShowCustomUI(string index)
    {
        if (null != index)
        {
            string feature = "PageMediaSize";
            int i = int.Parse(index);
            IPrintSchemaOption selectedOption = GetCachedFeatureOptions(feature)[i];
            if (selectedOption.Name.Equals("CustomMediaSize", StringComparison.CurrentCulture)
                || selectedOption.Name.Equals("PSCustomMediaSize", StringComparison.CurrentCulture))
            {
                return true;
            }
        }
        return false;
    }
    ```

3. 在 "自定义" 弹出窗口中，显示一个自定义 UI，该 UI 要求用户提供页面高度和宽度，并从 IPrintSchemaPageMediaSizeOption 中检索用户指定的高度和宽度。

    此示例显示了一个方法，该方法用于向用户询问页面的高度和宽度。

    ```CSharp
    private void ShowCustomPageMediaSizeUI(string index, bool keepValue)
    {
        //Hide custom media size UI unless needed
        if (IsCustomSizeSelected(index))
        {
           if (keepValue && (!customWidth.Equals("")) && (!customHeight.Equals("")))
           {
                        CustomWidthBox.Text = customWidth;
                        CustomHeightBox.Text = customHeight;
           }
           else
           {
              // Use a helper function from the WinRT helper component
              CustomWidthBox.Text = printHelper.GetCustomWidth(index);
              CustomHeightBox.Text = printHelper.GetCustomHeight(index);
           }
           CustomUIPanel.Visibility = Windows.UI.Xaml.Visibility.Visible;
           CustomWidthBox.KeyDown += OnCustomValueEntered;
           CustomHeightBox.KeyDown += OnCustomValueEntered;
        }
        else
        {
           CustomUIPanel.Visibility = Windows.UI.Xaml.Visibility.Collapsed;
           CustomWidthBox.KeyDown -= OnCustomValueEntered;
           CustomHeightBox.KeyDown -= OnCustomValueEntered;
        }
    }
    ```

4. `IPrintSchemaPageMediaSizeOption`用用户指定的值更新对象，并验证高度和宽度是否与用户指定的值匹配。

    此示例是一个帮助器方法，用于更新 `IPrintSchemaPageMediaSizeOption` 打印机帮助器类中的对象。 `OnSaveRequested`如果自定义弹出窗口中的处理程序确定请求了自定义页面大小选项，则该处理程序将调用此函数。

    ```CSharp
    public void SetCustomMediaSizeDimensions(string width, string height)
    {
      if ((null == width) && (null == height) && (null == Capabilities))
      {
                    return;
      }
      try
      {
                    CheckSizeValidity(width, height);
      }
      catch (FormatException e)
      {
                    throw new ArgumentException(e.Message);
      }
      catch (OverflowException e)
      {
                    throw new ArgumentException(e.Message);
      }

      // The context is retrieved during app activation.
      IPrintSchemaTicket ticket = context.Ticket;

      //
      // Input XML as Stream
      //
      XElement ticketRootXElement = null;
      using (Stream ticketReadStream = ticket.GetReadStream())
      {
         ticketRootXElement = XElement.Load(ticketReadStream);
      }

      XNamespace psfNs = PrintSchemaConstants.FrameworkNamespaceUri;
      XNamespace pskNs = PrintSchemaConstants.KeywordsNamespaceUri;
      string pskPrefix = ticketRootXElement.GetPrefixOfNamespace(pskNs);

      // Modify the MediaSizeHeight and MediaSizeWidth
      IEnumerable<XElement> parameterInitCollection =
        from c in ticketRootXElement.Elements(psfNs + "ParameterInit")

      select c;

      foreach (XElement parameterInit in parameterInitCollection)
      {
        if (0 == String.Compare((string)parameterInit.Attribute("name"), pskPrefix + ":PageMediaSizePSWidth"))
        {
          IEnumerable<XElement> valueCollection = from c in parameterInit.Elements(psfNs + "Value")
          select c;
          valueCollection.ElementAt(0).Value = width;
        }

         else if (0 == String.Compare((string)parameterInit.Attribute("name"), pskPrefix + ":PageMediaSizePSHeight"))
        {
          IEnumerable<XElement> valueCollection = from c in parameterInit.Elements(psfNs + "Value")
          select c;
          valueCollection.ElementAt(0).Value = height;
         }
      }

      //
      // Write XLinq changes back to DOM
      //
       using (Stream ticketWriteStream = ticket.GetWriteStream())
       {
         ticketRootXElement.Save(ticketWriteStream);
       }
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
5. 编辑并保存设备元数据。 若要将设备应用链接到设备，你必须将设备应用关联到设备
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

### <a name="issue-advanced-print-settings-shows-default-flyout-instead-of-custom-flyout"></a>问题：高级打印设置显示默认浮出控件，而不是自定义飞出

如果 "高级打印设置" 浮出控件显示默认浮出控件，而不是应用程序实现的自定义浮出控件 .。。

- **可能的原因：** 未启用测试签名。 请参阅本主题中的调试部分，了解有关如何打开它的信息。

- **可能的原因：** 应用未查询正确的包系列名称。 在代码中检查包系列名称。 在 Visual Studio 中打开 **appxmanifest.xml** ，并确保要查询的包系列名称与 " **打包** " 选项卡上的 "包系列名称" 字段中的相同。

- **可能的原因：** 设备元数据不与包系列名称关联。 使用 **设备元数据创作向导** 打开设备元数据，并检查包系列名称。 双击DeviceMetadataWizard.exe，从 *% ProgramFiles (x86) %* \\ Windows 工具包 \\ 8.1 \\ bin \\ x86 **DeviceMetadataWizard.exe**启动向导。

### <a name="issue-app-is-launched-in-flyout-then-is-immediately-dismissed"></a>问题：应用程序在浮出控件中启动，然后立即解除

如果高级打印设置的自定义浮出控件在启动后立即消失 .。。

- **可能的原因：** 在 Windows 8 中，有一个已知问题，即在弹出窗口中，UWP 应用将在调试器下解除。 一旦知道激活有效，就关闭调试。 如果需要调试保存打印票证，请在激活后附加调试器。

## <a name="related-topics"></a>相关主题

[开发 v4 打印驱动程序](https://go.microsoft.com/fwlink/p/?LinkId=314231)

[ (v4 打印驱动程序的打印机扩展接口) ](https://go.microsoft.com/fwlink/p/?LinkID=299887)

[双向通信](https://go.microsoft.com/fwlink/p/?LinkId=317192)

[UWP 应用入门](getting-started.md)

[ (分步指南创建 UWP 设备应用) ](step-1--create-a-uwp-device-app.md)

[ (分步指南创建 UWP 设备应用的设备元数据) ](step-2--create-device-metadata.md)
