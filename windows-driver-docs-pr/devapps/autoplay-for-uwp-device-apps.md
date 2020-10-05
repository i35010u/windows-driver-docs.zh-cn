---
title: UWP 设备应用的自动播放
description: 本主题介绍如何使用设备元数据创作向导来启用自动播放。 它还介绍了如何在应用中处理自动播放激活。
ms.assetid: A95382E6-DFF4-4F36-9C9B-4B26161160DE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6a2aef56176af5a699c4e2c381e43d1efaa78e59
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91734485"
---
# <a name="autoplay-for-uwp-device-apps"></a>UWP 设备应用的自动播放


设备制造商可以将其 UWP 设备应用指定为其设备的自动播放处理程序。 他们还可以让其他 UWP 应用充当其设备的自动播放处理程序。 本主题介绍如何使用设备元数据创作向导来启用自动播放。 它还介绍了如何在应用中处理自动播放激活。 有关设备应用的详细信息，请参阅 " [满足 UWP 设备应用](meet-uwp-device-apps.md)"。

**注意**   不需要为所有类型的自动播放使用设备元数据。 如果没有设备元数据，自动播放使你可以在用户将设备连接到 PC 时提供应用作为选项。 这包括非体积设备，如照相机或 media player，或卷设备（如 USB 拇指驱动器、SD 卡或 DVD）。 自动播放还允许你在用户使用邻近)  (点击时，将应用注册为一个选项。 但不能自动安装应用，无需设备元数据。 有关无需设备元数据时使用自动播放的详细信息，请参阅 [使用自动播放自动启动](/previous-versions/windows/apps/hh452731(v=win.10))。

 

## <a name="span-idautoplay_overviewspanspan-idautoplay_overviewspanspan-idautoplay_overviewspanautoplay-overview"></a><span id="AutoPlay_overview"></span><span id="autoplay_overview"></span><span id="AUTOPLAY_OVERVIEW"></span>自动播放概述


根据你的应用程序的版本，你可以通过以下方式启用自动播放：

-   只有 UWP 设备应用才能处理 \[ Windows 8 中受支持的设备的自动播放激活 Windows 8.1 \] 。
-   其他 UWP 应用只能处理 Windows 8.1 中支持的设备的自动播放激活 \[ \] 。
-   UWP 设备应用和其他 UWP 应用只能处理 Windows 8.1 中支持的设备的自动播放激活 \[ \] 。

此示例显示了已注册为**Contoso Pedometer**设备的自动播放处理程序的名为**contoso 仪表板**的应用程序的自动播放对话框：

![设备的示例自动播放对话框](images/autoplayfordeviceapps.png)

在应用中使用设备元数据时，自动播放支持以下设备类型：

| 设备分类                 | Windows 8 中支持的自动播放                                                                    | Windows 8.1 中支持的自动播放                                                                    |
|------------------------------|----------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------|
| 数字静止相机         | ![windows 8 中的此设备类支持自动播放](images/ap-tools.png)                   | ![windows 8.1 中支持自动播放此设备类](images/ap-tools.png)                   |
| 数字视频摄像机      | ![windows 8 中的此设备类支持自动播放](images/ap-tools.png)                   | ![windows 8.1 中支持自动播放此设备类](images/ap-tools.png)                   |
| 便携媒体播放器        | ![windows 8 中的此设备类支持自动播放](images/ap-tools.png)                   | ![windows 8.1 中支持自动播放此设备类](images/ap-tools.png)                   |
| 手机                   | ![windows 8 中的此设备类支持自动播放](images/ap-tools.png)                   | ![windows 8.1 中支持自动播放此设备类](images/ap-tools.png)                   |
| 移动宽带             | ![windows 8 中的此设备类不支持自动播放](images/app-tools-doesnotapply.png) | ![windows 8.1 中不支持自动播放此设备类](images/app-tools-doesnotapply.png) |
| 摄像头                       | ![windows 8 中的此设备类不支持自动播放](images/app-tools-doesnotapply.png) | ![windows 8.1 中不支持自动播放此设备类](images/app-tools-doesnotapply.png) |
| 人体学接口设备 (HID) | ![windows 8 中的此设备类不支持自动播放](images/app-tools-doesnotapply.png) | ![windows 8.1 中支持自动播放此设备类](images/ap-tools.png)                   |
| 打印机，扫描仪，传真      | ![windows 8 中的此设备类不支持自动播放](images/app-tools-doesnotapply.png) | ![windows 8.1 中不支持自动播放此设备类](images/app-tools-doesnotapply.png) |
| PC                           | ![windows 8 中的此设备类不支持自动播放](images/app-tools-doesnotapply.png) | ![windows 8.1 中不支持自动播放此设备类](images/app-tools-doesnotapply.png) |
| 智能卡                   | ![windows 8 中的此设备类不支持自动播放](images/app-tools-doesnotapply.png) | ![windows 8.1 中支持自动播放此设备类](images/ap-tools.png)                   |
| 常规端口                 | ![windows 8 中的此设备类不支持自动播放](images/app-tools-doesnotapply.png) | ![windows 8.1 中支持自动播放此设备类](images/ap-tools.png)                   |
| 蓝牙设备             | ![windows 8 中的此设备类不支持自动播放](images/app-tools-doesnotapply.png) | ![windows 8.1 中不支持自动播放此设备类](images/app-tools-doesnotapply.png) |

 

## <a name="span-idbefore_you_beginspanspan-idbefore_you_beginspanspan-idbefore_you_beginspanbefore-you-begin"></a><span id="Before_you_begin"></span><span id="before_you_begin"></span><span id="BEFORE_YOU_BEGIN"></span>开始之前


-   **请确保已安装设备元数据创作向导**。 你需要它来启用自动播放。 在此版本中，此向导包含在 Microsoft Visual Studio Professional 和 Microsoft Visual Studio Ultimate 中。 但是，如果您已 Microsoft Visual Studio Express Windows，则需要下载用于 [Windows 8.1 的独立 SDK](https://go.microsoft.com/fwlink/p/?linkid=309209) 以获取向导。

-   **将应用与 Microsoft Store 相关联**。 你将需要应用的包信息来启用自动播放。 有关详细信息，请参阅[步骤1：创建 UWP 设备应用](step-1--create-a-uwp-device-app.md)中的 "*将应用与 Microsoft Store 相关联"* 部分。

-   **创建设备元数据**。 如果尚未开始使用，请参阅[构建 UWP 设备应用循序渐进](build-a-uwp-device-app-step-by-step.md)指南中的[步骤2：创建设备元数据](step-2--create-device-metadata.md)。

## <a name="span-idenabling_autoplayspanspan-idenabling_autoplayspanspan-idenabling_autoplayspanenabling-autoplay"></a><span id="Enabling_AutoPlay"></span><span id="enabling_autoplay"></span><span id="ENABLING_AUTOPLAY"></span>启用自动播放


**设备元数据创作向导**允许你将 UWP 应用声明为设备的默认自动播放处理程序。 还可以让其他 UWP 应用充当设备的自动播放处理程序。 您可以选择这些选项中的任一选项，也可以选择这两种选项。

**使用设备元数据创作向导启用自动播放**

1.  双击DeviceMetadataWizard.exe，从 *% ProgramFiles (x86) %* Windows 工具包 8.1 bin X86 启动**设备元数据创作向导** \\ \\ \\ \\ 。 ** **
2.  单击 " **编辑设备元数据**"。 这将允许你编辑现有的设备元数据包。
3.  在 " **打开** " 对话框中，找到与 UWP 设备应用关联的设备元数据包。  (其文件扩展名为 **devicemetadata** 。 ) 
4.   (可选 ) 。如果没有设备应用的包名称、发布者名称和应用 ID，请单击 " **应用信息** " 以查看 UWP 设备应用的打包信息。
5.  单击 " **Windows 信息** " 以指定自动播放详细信息。
6.  如果要将应用指定为设备的默认自动播放处理程序，请选择 " **使用 UWP 设备应用**"。 你可以选择任何 UWP 应用或 UWP 设备应用，但该应用必须处理设备的自动播放激活，并在应用包清单中指定相应的体验 ID (如下一过程) 中所指定。
    -   **包名称**：在应用包清单中，这是 Identity 元素的 name 属性。
    -   **发布者名称**：在应用包清单中，这是 Identity 元素的发布服务器特性。
    -   **应用 ID**：在应用包清单中，这是应用程序元素的 ID 属性。
    -   **Verb**：这是自动播放激活的标识符。 你的应用程序将使用它来确定激活是否来自你的设备。 可以将任何值用于谓词设置，但 **open**除外。
    -   **自动播放事件类型**：将其保留为 **设备**。 在设备元数据中，向导将自动指定与 UWP 设备应用关联的体验 ID。

7.  如果想让其他应用充当设备的自动播放处理程序，请选择 " **为已注册的应用程序启用自动播放**"。
8.  完成后，单击 **“下一步”**。
9.  当你看到 " **完成** " 页面时，请记下 " **体验 ID**"。 当你在应用程序中处理自动播放激活时，你将在下一个过程中需要它。
10. 验证 **保存信息** ，并单击 " **保存** " 以更新设备元数据包。

## <a name="span-idhandling_autoplay_activationspanspan-idhandling_autoplay_activationspanspan-idhandling_autoplay_activationspanhandling-autoplay-activation"></a><span id="Handling_AutoPlay_activation"></span><span id="handling_autoplay_activation"></span><span id="HANDLING_AUTOPLAY_ACTIVATION"></span>处理自动播放激活


若要在应用中处理自动播放激活，需在应用 `windows.autoPlayDevice` 程序包清单中注册扩展，然后在应用程序对象的事件中处理该事件 `OnActivated` 。 请注意，你的应用可以注册为多个设备的自动播放处理程序。

### <a name="span-idto_register_your_app_as_an_autoplay_handlerspanspan-idto_register_your_app_as_an_autoplay_handlerspanspan-idto_register_your_app_as_an_autoplay_handlerspanto-register-your-app-as-an-autoplay-handler"></a><span id="To_register_your_app_as_an_AutoPlay_handler"></span><span id="to_register_your_app_as_an_autoplay_handler"></span><span id="TO_REGISTER_YOUR_APP_AS_AN_AUTOPLAY_HANDLER"></span>将应用注册为自动播放处理程序

若要将应用注册为设备的自动播放处理程序，需要指定与 UWP 设备应用关联的体验 ID 以及将用于激活应用的自动播放 **谓词** 和 **ActionDisplayName** 。

1.  在 Microsoft Visual Studio 中打开应用程序的项目。
2.  在 **解决方案资源管理器**中，右键单击 **appxmanifest.xml** 文件并选择 " **查看代码**"。 这会在 XML (文本) 编辑器中显示应用包清单。
3.  在元素中 `Application` 的元素下面 `VisualElements` ，将以下元素粘贴 `Extensions` 到包清单文件中。
    ```XML
          <Extensions>
            <Extension Category="windows.autoPlayDevice">
              <AutoPlayDevice>
                <LaunchAction
                    Verb="showDevice1"
                    ActionDisplayName="Launch App for Device 1"
                    DeviceEvent="ExperienceID:{00000000-ABCD-EF00-0000-000000000000}"/>
              </AutoPlayDevice>
            </Extension>
          </Extensions>
    ```

4.  将此示例中的自动播放值替换为应用的实际值：
    -   `Verb`：这是自动播放激活的标识符。 你的应用程序将使用它来确定激活是否来自你的设备。 如果你的应用已指定为设备的默认自动播放处理程序，则此值应与你在设备元数据中指定的 **谓词** 匹配。 如果你的应用未指定为你的设备的默认自动播放处理程序，则可以使用谓词设置的任何值，而 " **open**" 除外。
    -   `ActionDisplayName`：自动播放为应用显示的字符串。
    -   `Experience ID`：用于将应用与设备关联的体验 ID GUID。 这是你在前面的过程中记下的值。

### <a name="span-idto_handle_autoplay_activationspanspan-idto_handle_autoplay_activationspanspan-idto_handle_autoplay_activationspanto-handle-autoplay-activation"></a><span id="To_handle_AutoPlay_activation"></span><span id="to_handle_autoplay_activation"></span><span id="TO_HANDLE_AUTOPLAY_ACTIVATION"></span>处理自动播放激活

当设备触发自动播放激活时，激活类型将为 `Windows.ApplicationModel.Activation.ActivationKind.device` 。 使用 `eventObj` 传递的对象 `OnActivated` 检查应用的激活方式。 如果它来自自动播放，则可以使用 `eventObj` 确定哪些设备 ID 和自动播放谓词导致激活。

在此示例中，激活事件参数 (eventObj) 携带设备的 ID 以及用于激活的动作。

```JavaScript
<!DOCTYPE html>
<html>
<head>
  <script type="text/javascript">
    function OnActivated(eventObj) {
        if (eventObj.kind == Windows.ApplicationModel.Activation.ActivationKind.launch) {
            // Activated by the user.
        }
        else if (eventObj.kind == Windows.ApplicationModel.Activation.ActivationKind.device) {
            // Activated by a device, for AutoPlay.
            // Device path = eventObj.deviceInformationId;
            // verb (“showDevice1”) = eventObj.verb;
        }
    }

    Windows.UI.WebUI.WebUIApplication.addEventListener("activated", OnActivated, false);
  </script>
</head>

<body>
...
...
...
</body>
</html>
```

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[初识 UWP 设备应用](meet-uwp-device-apps.md)

[分步构建 UWP 设备应用](build-a-uwp-device-app-step-by-step.md)

[借助自动播放功能自动启动](/previous-versions/windows/apps/hh452731(v=win.10))

[Launching, resuming, and multitasking](/previous-versions/windows/apps/hh770837(v=win.10))

 

