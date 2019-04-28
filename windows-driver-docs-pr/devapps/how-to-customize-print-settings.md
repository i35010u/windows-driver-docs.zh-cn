---
title: 如何自定义打印设置 （UWP 设备应用）
description: 本主题介绍在高级打印设置浮出控件，并演示如何将C#版本的打印设置和打印示例使用自定义的浮出控件替换默认浮出控件的通知。
ms.assetid: 099BD9B2-1AA6-49A5-AB84-0AF6FA0EFB26
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 653724ee75540e1bcff7b23853696cd43d53edd1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330678"
---
# <a name="how-to-customize-print-settings-uwp-device-apps"></a>如何自定义打印设置 （UWP 设备应用）


在 Windows 8.1 UWP 设备应用程序允许自定义高级打印设置显示的 flyout 的打印机制造商。 本主题介绍在高级打印设置浮出控件，并演示如何将C#的版本[打印设置和打印通知](https://go.microsoft.com/fwlink/p/?LinkID=242862)示例使用自定义的浮出控件替换默认浮出控件。 若要在一般情况下了解有关 UWP 的设备应用程序的详细信息，请参阅[满足 UWP 设备应用](meet-uwp-device-apps.md)。

C#的版本[打印设置和打印通知](https://go.microsoft.com/fwlink/p/?LinkID=242862)的示例使用**Preferences.xaml**页以显示自定义浮出控件的 UI 高级打印设置。 打印帮助器类用于创建设备上下文 (IPrinterExtensionContext)，并执行设备查询。 **PrinterHelperClass.cs**文件位于**DeviceAppForPrintersLibrary**项目，然后使用 Api 中定义**PrinterExtensionLibrary**项目。 打印机扩展库提供了方便地访问 v4 打印驱动程序的打印机扩展插件接口。 有关详细信息，请参阅[打印机扩展库概述](printer-extension-library-overview.md)。

**请注意**  本主题中所示的代码示例基于C#的版本[打印设置和打印通知](https://go.microsoft.com/fwlink/p/?LinkID=242862)示例。 此示例也会出现在 JavaScript 和C++。 请注意，由于C++可以直接访问 COMC++示例的版本不包括代码库项目。 下载示例，请参阅最新版本的代码。

 

## <a name="span-idadvancedprintsettingsspanspan-idadvancedprintsettingsspanspan-idadvancedprintsettingsspanadvanced-print-settings"></a><span id="Advanced_print_settings"></span><span id="advanced_print_settings"></span><span id="ADVANCED_PRINT_SETTINGS"></span>高级打印设置


高级打印设置体验是打印机提供当用户想要选择不在打印窗口中提供的打印设置的功能。 它是可通过访问**更多设置**打印窗口中的链接。 它不是一种的全屏体验，但显示中弹出一个窗口，也就是用于显示用户单击或点击外部时关闭的轻量、 上下文的用户界面的控件。

这种体验可用于突出显示不同的功能如打印机将水印应用于文档页，提供安全的打印选项或图像增强功能选项。

当没有为打印机安装 UWP 设备应用时，Windows 提供的默认打印设置体验。 如果 Windows 检测到为您的打印机，安装的 UWP 设备应用程序和应用程序具有中选择的`windows.printTaskSettings`扩展，您的应用程序取代了 Windows 提供的默认体验。

若要调用的飞出式高级打印设置：

1.  打开支持打印的 UWP 应用
2.  通过在屏幕右侧轻扫 （或通过使用 Windows 徽标键 + C） 来访问超级按钮
3.  点击**设备**超级按钮
4.  点击**打印**
5.  点击打印机
6.  **打印**窗口随即打开
7.  单击**更多的设置**链接**打印**窗口
8.  高级打印的设置浮出控件打开
    -   *默认浮出控件*安装打印机无 UWP 设备应用会出现
    -   一个*自定义浮出控件*安装打印机的 UWP 设备应用程序会出现

![默认和自定义浮出控件的高级打印设置的示例。](images/373072-printer-settings-launch.png)

## <a name="span-idprerequisitesspanspan-idprerequisitesspanspan-idprerequisitesspanprerequisites"></a><span id="Prerequisites"></span><span id="prerequisites"></span><span id="PREREQUISITES"></span>先决条件


开始之前：

1.  请确保使用 v4 打印驱动程序安装您的打印机。 有关详细信息，请参阅[开发 v4 打印驱动程序](https://go.microsoft.com/fwlink/p/?LinkId=314231)。
2.  获取对开发计算机设置。 请参阅[入门](getting-started.md)有关下载工具和创建开发人员帐户信息。
3.  将你的应用与应用商店相关联。 请参阅[创建 UWP 设备应用](step-1--create-a-uwp-device-app.md)有关的信息。
4.  创建设备元数据为您将其与您的应用程序关联的打印机。 请参阅[创建设备元数据](step-2--create-device-metadata.md)有关的详细信息。
5.  构建您的应用程序的主页上的 UI。 可以从开始，它们将显示的全屏启动所有 UWP 设备应用程序。 使用入门体验突出显示你的产品或匹配特定品牌的方式和你的设备的功能中的服务。 没有任何特殊限制可以使用 UI 控件的类型。 若要开始使用的设计的全屏体验，请参阅[Microsoft Store 设计原则](https://go.microsoft.com/fwlink/p/?LinkID=299845)。
6.  如果您正在编写您编写的应用程序与C#或 JavaScript 中，添加**PrinterExtensionLibrary**并**DeviceAppForPrintersLibrary**到您 UWP 设备应用程序解决方案的项目。 您可以找到这些项目中的每个[打印设置和打印通知](https://go.microsoft.com/fwlink/p/?LinkID=242862)示例。
    **请注意**  由于C++可以直接访问 COMC++应用程序不需要单独的库以使用基于 COM 的打印机设备上下文。

     

## <a name="span-idstep1registertheextensionspanspan-idstep1registertheextensionspanspan-idstep1registertheextensionspanstep-1-register-the-extension"></a><span id="Step_1__Register_the_extension"></span><span id="step_1__register_the_extension"></span><span id="STEP_1__REGISTER_THE_EXTENSION"></span>步骤 1：注册扩展


为了使 Windows 能够识别应用程序可以提供高级打印设置的自定义浮出控件，它必须注册打印任务设置扩展。 此扩展中声明`Extension`元素中，使用`Category`属性设置为值为`windows.printTaskSettings`。 在C#和C++示例中，`Executable`属性设置为`$targetnametoken$.exe`并且`EntryPoint`属性设置为`DeviceAppForPrinters.App`。

可以在添加打印任务设置扩展**声明**清单设计器在 Microsoft Visual Studio 中的选项卡。 您还可以编辑的应用程序包清单 XML 手动，使用 XML （文本） 编辑器。 右键单击**Package.appxmanifest**中的文件**解决方案资源管理器**的编辑选项。

此示例演示中的打印任务设置扩展`Extension`元素，因为它在应用包清单文件中，将出现**Package.appxmanifest**。

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

## <a name="span-idstep2buildtheuispanspan-idstep2buildtheuispanspan-idstep2buildtheuispanstep-2-build-the-ui"></a><span id="Step_2__Build_the_UI"></span><span id="step_2__build_the_ui"></span><span id="STEP_2__BUILD_THE_UI"></span>步骤 2：生成 UI


生成你的应用之前, 应适用于您的设计人员和营销团队设计用户体验。 用户体验应项目贵公司的品牌方面，并帮助您构建与你的用户的连接。

### <a name="span-iddesignguidelinesspanspan-iddesignguidelinesspanspan-iddesignguidelinesspandesign-guidelines"></a><span id="Design_guidelines"></span><span id="design_guidelines"></span><span id="DESIGN_GUIDELINES"></span>设计指南

务必要查看[UWP 应用浮出控件准则](https://go.microsoft.com/fwlink/p/?LinkId=317078)设计自定义的浮出控件之前。 指导帮助确保在浮出控件提供直观的体验与其他 UWP 应用一致的。

为您的应用程序的主页，请注意 Windows 8.1，可以在一台监视器上的各种大小显示多个应用。 请参阅以下指南以了解有关如何应用可以重排正常之间屏幕尺寸、 窗口大小和方向详细信息。

-   [窗口大小和扩展到屏幕的准则](https://go.microsoft.com/fwlink/p/?LinkId=311830)
-   [重设大小、 高和窄布局的 windows 的准则](https://go.microsoft.com/fwlink/p/?LinkId=311831)

### <a name="span-idflyoutdimensionsspanspan-idflyoutdimensionsspanspan-idflyoutdimensionsspanflyout-dimensions"></a><span id="Flyout_dimensions"></span><span id="flyout_dimensions"></span><span id="FLYOUT_DIMENSIONS"></span>浮出控件维度

浮出控件显示高级打印设置是 646 像素宽和高至少 768 像素 （实际高度取决于用户屏幕的分辨率）。 由 Windows 提供浮出控件的标题区中后退按钮。 "应用程序标题"文本是从应用程序清单的应用程序标题。 标题区为 80 像素高，离开期间耗时 688 像素为单位的自定义浮出控件的可视区域。

![高级的打印机设置的浮出控件尺寸。](images/439446-printer-options-layout.png)

**请注意**  如果自定义的浮出控件是多个期间耗时 688 像素高，用户可能会滑动或向下滚动以查看的浮出控件是高于还是低于可视区域的部分。

 

### <a name="span-iddefiningtheapptitlecolorandiconspanspan-iddefiningtheapptitlecolorandiconspanspan-iddefiningtheapptitlecolorandiconspandefining-the-app-title-color-and-icon"></a><span id="Defining_the_app_title_color_and_icon"></span><span id="defining_the_app_title_color_and_icon"></span><span id="DEFINING_THE_APP_TITLE_COLOR_AND_ICON"></span>定义应用程序标题颜色和图标

标题、 背景色、 文本颜色和自定义浮出控件上的小徽标来自`VisualElements`应用包清单文件中的元素。

此示例演示的标题和图标，如中所定义`VisualElements`元素中的，在应用包清单文件 (**Package.appxmanifest**)。

```XML
      <VisualElements DisplayName="Device App For Printers C# sample" Logo="Assets\squareTile-sdk.png" SmallLogo="Assets\smallTile-sdk.png" Description="DeviceAppForPrinters C# sample" ForegroundText="light" BackgroundColor="#00b2f0" ToastCapable="true">
        <DefaultTile ShowName="allLogos" ShortName="App4PrinterCS" WideLogo="Assets\tile-sdk.png" />
        <SplashScreen Image="Assets\splash-sdk.png" BackgroundColor="#00b2f0" />
      </VisualElements>
```

### <a name="span-idbestpracticesspanspan-idbestpracticesspanspan-idbestpracticesspanbest-practices"></a><span id="Best_practices"></span><span id="best_practices"></span><span id="BEST_PRACTICES"></span>最佳做法

-   **保留相同的外观和感觉。** 对齐开始体验 （您的应用程序的 Main 页），该设计与你自定义浮出控件包括字体、 颜色和控件元素。 应用应该感到很熟悉而不考虑它们调用从它的人。

-   **简化的交互。** 避免耗时或复杂交互。 在大多数情况下，操作，例如设置打印机、 查看状态、 排序墨迹和故障排除是最佳开始体验内执行。

-   **保持在最低限度的导航。** 避免让您自定义的浮出控件中的多个页面之间来回导航的用户。 相反，使用垂直滚动或内联控件，如渐进式公开控件、 下拉列表和内联错误消息。

-   **不使用 light 解除浮出控件。** 打印体验已使用一个指示灯解除浮出控件。 包括另一个光消除中您的自定义元素浮出控件可以将你的用户相混淆。

-   **禁用链接会导致用户离开不打印体验。** 当用户打印内容时，则应采取措施以确保它们保持在打印的上下文中。 例如，如果您的应用程序会导致您的应用程序 （如有关主页上或购买墨迹页） 的其他区域的链接，则应禁用它们使用户不会意外地将留在高级打印设置体验。

## <a name="span-idstep3spanspan-idstep3spanstep-3-handle-activation"></a><span id="step3"></span><span id="STEP3"></span>步骤 3:处理激活


如果您的应用程序已声明打印任务设置扩展，它必须实现`OnActivated`方法以处理应用程序激活事件。 应用程序激活时，您的应用程序可以选择哪一页将为该应用启动时启动。 对于具有声明打印任务设置扩展的应用程序，Windows 将打印任务扩展上下文传递 Activated 事件参数中：Windows.ApplicationModel.Activation.IActivatedEventArgs.

UWP 设备应用程序可以确定的激活适用于高级打印设置 (的人只是点击**更多选项**在打印设置对话框) 时将事件参数的`kind`属性是否等于Windows.ApplicationModel.Activation.ActivationKind.printTaskSettings。

**请注意**  在某些情况下，如果在用户启动后后立即, 关闭应用程序可能会引发异常的处理程序的激活。 若要避免此问题，请确保您激活的处理程序高效地完成，而不会执行占用大量资源的处理。

 

此示例演示中的激活事件处理程序`OnActivated`方法，因为它将出现在**Constants.cs**文件。 然后，事件参数会转换为 Windows.ApplicationModel.Activation.PrintTaskSettingsActivatedEventArgs。 尽管该示例包含在此代码**Constants.cs**文件，它是实际的也在中定义的应用程序类的一部分**App.xaml.cs**文件。

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

## <a name="span-idstep4displaysettingsspanspan-idstep4displaysettingsspanspan-idstep4displaysettingsspanstep-4-display-settings"></a><span id="Step_4__Display_settings"></span><span id="step_4__display_settings"></span><span id="STEP_4__DISPLAY_SETTINGS"></span>步骤 4：“显示设置”


当`LoadAdvancedPrintSettingsContext`方法调用时，打印任务配置上下文分配给 MainPage 类的变量。 这将允许在启动时访问的打印设置的自定义的浮出控件。

传递到的事件参数`LoadAdvancedPrintSettingsContext`方法，用于访问和控制打印机公开属性：

-   **Args.configuration**属性提供类型 Windows.Devices.Printers.Extensions.PrintTaskConfiguration 的对象。 此对象提供了访问打印任务扩展上下文，并还允许您添加事件处理程序更新的打印票证。
-   **Args.configuration.printerExtensionContext**属性提供类型 Windows.Devices.Printers.Extensions.PrinterExtensionContext 的对象。 此对象是指向打印架构，PrintTicket，PrinterExtensionLibrary 接口的指针，打印队列的信息。 如果没有接口的公开方式，它将为 null。 有关详细信息，请参阅[打印机扩展库概述](printer-extension-library-overview.md)。

此示例演示`LoadAdvancedPrintSettingsContext`方法，因为它将出现在**Constants.cs**文件。

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

在自定义浮出控件页**Preferences.xaml.cs**，一个名为类`rootPage`充当指向 MainPage 类的指针，以便可以从浮出控件访问打印任务扩展上下文和打印机设备上下文。

此示例显示指针中的一部分`Preferences`类中，从**Preferences.xaml.cs**文件。 下载[打印设置和打印通知](https://go.microsoft.com/fwlink/p/?LinkID=242862)示例，请参阅完整代码。

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

时的页构造函数**Preferences.xaml.cs**是调用，对象创建为打印任务的扩展上下文 (`PrintTaskConfiguraton`名为对象`configuration`) 和打印机设备上下文 (`PrintHelperClass`名为对象`printHelper`).

创建这些对象后，在使用打印机设备上下文`DisplaySettings`方法以加载 Textblock 和 ComboBoxs。 请注意，与 JavaScript 不同，所选内容中的更改不会与其他应用程序在同一线程上触发。 您必须维护用户选择要用于更高版本的本地缓存。

此示例显示了自定义浮出控件页构造函数中， `DisplaySettings`，和中的其他帮助器方法**Preferences.xaml.cs**文件。

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

## <a name="span-idstep5savesettingsspanspan-idstep5savesettingsspanspan-idstep5savesettingsspanstep-5-save-settings"></a><span id="Step_5__Save_settings"></span><span id="step_5__save_settings"></span><span id="STEP_5__SAVE_SETTINGS"></span>步骤 5：保存设置


当用户完成设置高级打印设置时，Microsoft Store 设备应用程序需要以保存所做的更改，用户将恢复为之前**打印**窗口。 为此，应用程序需要在用户点击时侦听**回**（从自定义浮出控件页） 按钮。 在这种情况，`SaveRequested`打印任务扩展上下文的事件 (`configuration`对象) 触发。

此示例中显示的事件侦听器`SaveRequested`，添加到中`OnNavigatedTo`的自定义浮出控件的事件处理程序，请在**Preferences.xaml.cs**文件。 当`SaveRequested`触发事件时，`OnSaveRequested`将调用方法 (该方法也是在**Preferences.xaml.cs**文件)。

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

在中`OnSaveRequested`方法，该应用程序首次使用`printHelper`打印机扩展上下文上设置的每个功能的当前所选的选项的对象。 然后，调用`Save`方法`request`对象作为参数传入`OnSaveRequested`方法。 `Save`方法，从 Windows.Devices.Printers.Extensions.PrintTaskConfigurationSaveRequest 类中，使用打印机扩展上下文验证的打印票证和保存打印任务配置。

**重要**  如果的打印票证无效以任何方式`Save`方法将引发应用程序必须处理的异常。 如果应用程序不处理异常，该流已停止，强制对光线用户解除浮出控件，并且重新启动打印流。

 

此示例演示`OnSaveRequested`中的方法**Preferences.xaml.cs**文件。 因为`SaveRequested`不会在 UI 线程上引发事件，它需要使用 Windows.UI.Core.CoreDispatcher 将消息发布到 UI 线程要验证和保存票证时显示相应的消息。

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

### <a name="span-idsavingoptionsthatrequireuserinputspanspan-idsavingoptionsthatrequireuserinputspanspan-idsavingoptionsthatrequireuserinputspansaving-options-that-require-user-input"></a><span id="Saving_options_that_require_user_input"></span><span id="saving_options_that_require_user_input"></span><span id="SAVING_OPTIONS_THAT_REQUIRE_USER_INPUT"></span>正在保存需要用户输入的选项

[打印设置和打印通知](https://go.microsoft.com/fwlink/p/?LinkID=242862)示例演示如何设置已定义的功能，涵盖大多数打印选项。 但是，有些选项需要自定义的用户界面，以获取用户指定的值。 例如，如果应用使用高级打印设置来指定自定义页面大小，它将执行以下步骤将保存的用户指定的值：

1.  在应用激活过程中检索的打印票证。 前面部分中所述的打印设置的应用程序激活[步骤 3:处理激活](#step3)。

2.  检查是否已指定页大小选项。 在C#或 JS 应用程序打印的帮助器类可以检查此选项。 在C++应用程序中，在 IPrintSchemaOption 检索 IPrintSchemaPageMediaSizeOption 上调用 QueryInterface。

    如果指定页大小选项，则将检查打印帮助程序类中，此示例演示一种方法。

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

3.  自定义的浮出控件中显示一个自定义 UI，要求用户提供的页面高度和宽度，并从 IPrintSchemaPageMediaSizeOption 检索用户指定高度和宽度。

    此示例演示一种方法要求用户提供有关页面高度和宽度的自定义弹出窗口。

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

4.  更新`IPrintSchemaPageMediaSizeOption`对象使用用户指定的值，并验证的高度和宽度匹配的用户指定的值。

    此示例是一个帮助器方法用于更新`IPrintSchemaPageMediaSizeOption`打印机帮助程序类中的对象。 `OnSaveRequested`自定义浮出控件中的处理程序将调用此函数，如果确定请求了一个自定义页面大小选项。

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

## <a name="span-idtestingspanspan-idtestingspanspan-idtestingspantesting"></a><span id="Testing"></span><span id="testing"></span><span id="TESTING"></span>测试


你可以测试 UWP 设备应用之前，它必须链接到您的打印机使用的设备元数据。

-   需要打印机的位置，若要向其中添加设备应用信息的设备元数据包的副本。 如果没有设备元数据，您可以使用生成它**设备元数据创建向导**主题中所述[创建 UWP 设备应用的设备元数据](https://go.microsoft.com/fwlink/p/?LinkId=313644)。

    **请注意**  若要使用**设备元数据创建向导**，则必须安装 Microsoft Visual Studio Professional，Microsoft Visual Studio Ultimate，或[独立 SDK 的 Windows 8.1](https://go.microsoft.com/fwlink/p/?linkid=309209)之前完成本主题中的步骤。 安装 Microsoft Visual Studio Express 的 Windows 安装不包括在向导的 sdk 版本。

     

以下步骤生成您的应用程序并安装设备元数据。

1.  启用测试签名。
    1.  启动**设备元数据创建向导**从 *%programfiles （x86） %*\\Windows 工具包\\8.1\\bin\\x86，通过双击**DeviceMetadataWizard.exe**
    2.  从**工具**菜单中，选择**启用测试签名**。

2.  重新启动计算机
3.  通过打开解决方案 (.sln) 文件生成解决方案。 按 F7，或转至**生成-&gt;生成解决方案**从顶部菜单中加载示例之后。

4.  断开连接并卸载打印机。 此步骤是必需的以便 Windows 将在下一次检测到设备读取更新的设备元数据。
5.  编辑并保存设备元数据。 若要链接到你的设备的设备应用，必须将设备应用程序与你的设备**注意**  如果尚未创建设备元数据，请参阅[创建设备元数据为 UWP 设备应用](https://go.microsoft.com/fwlink/p/?LinkId=313644).

     

    1.  如果**设备元数据创建向导**未打开，启动从 *%programfiles （x86） %*\\Windows 工具包\\8.1\\bin\\x86，也可由双击**DeviceMetadataWizard.exe**。
    2.  单击**编辑设备元数据**。 这样就可以编辑现有的设备元数据包。
    3.  在中**打开**对话框框中，找到与 UWP 设备应用程序相关联的设备元数据包。 (它具有**devicemetadata ms**文件扩展名。)
    4.  上**指定 UWP 设备应用信息**页上，输入中的 Microsoft Store 应用信息**UWP 设备应用**框。 单击**导入 UWP 应用程序清单文件**自动输入**包名称**，**发布服务器的名称**，以及**UWP 应用程序 ID**。
    5.  如果您的应用程序注册的打印机通知，填写**通知处理程序**框。 在中**事件 ID**，输入打印事件处理程序的名称。 在中**事件资产**，输入该代码所在的位置的文件的名称。

    6.  完成后，单击**下一步**直至到达**完成**页。
    7.  上**查看设备元数据包**页面上，确保所有设置都正确，然后选择**复制到本地计算机上的元数据存储设备元数据包**复选框。 然后单击**保存**。

6.  重新连接您的打印机，以便在设备连接时，该 Windows 读取更新的设备元数据。

## <a name="span-idtroubleshootingspanspan-idtroubleshootingspanspan-idtroubleshootingspantroubleshooting"></a><span id="Troubleshooting"></span><span id="troubleshooting"></span><span id="TROUBLESHOOTING"></span>故障排除


### <a name="span-idissueadvancedprintsettingsshowsdefaultflyoutinsteadofcustomflyoutspanspan-idissueadvancedprintsettingsshowsdefaultflyoutinsteadofcustomflyoutspanspan-idissueadvancedprintsettingsshowsdefaultflyoutinsteadofcustomflyoutspanissue-advanced-print-settings-shows-default-flyout-instead-of-custom-flyout"></a><span id="Issue__Advanced_print_settings_shows_default_flyout_instead_of_custom_flyout"></span><span id="issue__advanced_print_settings_shows_default_flyout_instead_of_custom_flyout"></span><span id="ISSUE__ADVANCED_PRINT_SETTINGS_SHOWS_DEFAULT_FLYOUT_INSTEAD_OF_CUSTOM_FLYOUT"></span>问题：高级打印设置显示默认浮出控件而不是自定义浮出控件

如果高级打印设置浮出控件将显示默认浮出控件而不是以比您的应用程序实现自定义浮出控件...

-   **可能的原因：** 未打开测试签名。 请参阅本主题了解如何将其打开的调试部分。

-   **可能的原因：** 应用程序不查询的正确包系列名称。 检查你的代码中的包系列名称。 打开**package.appxmanifest**在 Visual Studio 并确保包系列名称要查询的匹配中的一个**打包**选项卡上，包系列名称字段中的。

-   **可能的原因：** 设备元数据所关联的包系列名称。 使用**设备元数据创建向导**要打开设备元数据并检查包系列名称。 从启动该向导 *%programfiles （x86） %*\\Windows 工具包\\8.1\\bin\\x86，通过双击**DeviceMetadataWizard.exe**。

### <a name="span-idissueappislaunchedinflyoutthenisimmediatelydismissedspanspan-idissueappislaunchedinflyoutthenisimmediatelydismissedspanspan-idissueappislaunchedinflyoutthenisimmediatelydismissedspanissue-app-is-launched-in-flyout-then-is-immediately-dismissed"></a><span id="Issue__App_is_launched_in_flyout_then_is_immediately_dismissed"></span><span id="issue__app_is_launched_in_flyout_then_is_immediately_dismissed"></span><span id="ISSUE__APP_IS_LAUNCHED_IN_FLYOUT_THEN_IS_IMMEDIATELY_DISMISSED"></span>问题：应用在浮出控件中启动，然后立即关闭

对于高级打印设置在自定义浮出控件消失后立即启动...

-   **可能的原因：** 在 Windows 8 中，是一个已知的问题，在浮出控件，UWP 应用将关闭在调试器下。 关闭调试一旦知道激活有效运行。 如果需要调试正在保存的打印票证，请在激活后附加调试器。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[开发 v4 打印驱动程序](https://go.microsoft.com/fwlink/p/?LinkId=314231)

[打印机扩展插件接口 （v4 打印驱动程序）](https://go.microsoft.com/fwlink/p/?LinkID=299887)

[双向通信](https://go.microsoft.com/fwlink/p/?LinkId=317192)

[UWP 应用入门](getting-started.md)

[创建 UWP 设备应用程序 （分步指南）](step-1--create-a-uwp-device-app.md)

[创建设备元数据对 UWP 设备应用 （分步指南）](step-2--create-device-metadata.md)

 

 






