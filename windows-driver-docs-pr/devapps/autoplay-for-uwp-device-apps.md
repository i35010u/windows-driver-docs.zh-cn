---
title: UWP 设备应用的自动播放
description: 本主题介绍如何使用设备元数据创作向导来启用自动播放。 它还介绍了如何在应用中处理自动播放激活。
ms.assetid: A95382E6-DFF4-4F36-9C9B-4B26161160DE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 76030386ae552f6e789b69fc3385241a48abfd89
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565458"
---
# <a name="autoplay-for-uwp-device-apps"></a>UWP 设备应用的自动播放


设备制造商可以指定其 UWP 的设备应用程序为其设备的自动播放处理程序。 它们还可以让其自动播放处理程序为其设备用作其他 UWP 应用。 本主题介绍如何使用设备元数据创作向导来启用自动播放。 它还介绍了如何在应用中处理自动播放激活。 有关设备应用程序的详细信息，请参阅[满足 UWP 设备应用](meet-uwp-device-apps.md)。

**请注意**  无需用于所有类型的自动播放设备元数据。 不包含设备元数据，自动播放可作为一个选项提供您的应用程序时用户将设备连接到 PC。 这包括非卷设备的照相机或媒体播放器，如或卷的设备，如 USB 拇指驱动器、 SD 卡或 DVD。 自动播放还可以注册应用程序作为一个选项，当用户共享使用邻近 （点击） 的两个计算机之间的文件时。 但您的应用程序不能没有设备元数据的情况下自动安装。 有关使用自动播放时的设备元数据不是必需的详细信息，请参阅[使用自动播放自动启动](https://go.microsoft.com/fwlink/p/?LinkID=254861)。

 

## <a name="span-idautoplayoverviewspanspan-idautoplayoverviewspanspan-idautoplayoverviewspanautoplay-overview"></a><span id="AutoPlay_overview"></span><span id="autoplay_overview"></span><span id="AUTOPLAY_OVERVIEW"></span>自动播放概述


具体取决于您的应用程序的版本，可以启用自动播放，在以下方面：

-   仅在 UWP 设备应用可以处理你的设备的自动播放激活\[支持在 Windows 8 中，Windows 8.1\]。
-   其他的 UWP 应用可以处理你的设备的自动播放激活\[仅在 Windows 8.1 中支持\]。
-   UWP 设备应用和其他 UWP 应用可以处理你的设备的自动播放激活\[仅在 Windows 8.1 中支持\]。

此示例显示了应用程序名为自动播放对话框**Contoso 仪表板**的已注册的自动播放处理程序**Contoso 计步器**设备：

![设备的示例自动播放对话框](images/autoplayfordeviceapps.png)

当使用你的应用使用设备元数据，自动播放将支持以下设备类型：

| 设备类                 | 在 Windows 8 中受支持的自动播放                                                                    | 在 Windows 8.1 中受支持的自动播放                                                                    |
|------------------------------|----------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------|
| 数码照相机         | ![自动播放支持 windows 8 中此设备类](images/ap-tools.png)                   | ![自动播放支持 windows 8.1 中此设备类](images/ap-tools.png)                   |
| 数字视频摄像机      | ![自动播放支持 windows 8 中此设备类](images/ap-tools.png)                   | ![自动播放支持 windows 8.1 中此设备类](images/ap-tools.png)                   |
| 便携式媒体播放器        | ![自动播放支持 windows 8 中此设备类](images/ap-tools.png)                   | ![自动播放支持 windows 8.1 中此设备类](images/ap-tools.png)                   |
| 手机                   | ![自动播放支持 windows 8 中此设备类](images/ap-tools.png)                   | ![自动播放支持 windows 8.1 中此设备类](images/ap-tools.png)                   |
| 移动宽带             | ![自动播放不支持 windows 8 中此设备类](images/app-tools-doesnotapply.png) | ![自动播放不支持 windows 8.1 中此设备类](images/app-tools-doesnotapply.png) |
| Webcam                       | ![自动播放不支持 windows 8 中此设备类](images/app-tools-doesnotapply.png) | ![自动播放不支持 windows 8.1 中此设备类](images/app-tools-doesnotapply.png) |
| 人体学接口设备 (HID) | ![自动播放不支持 windows 8 中此设备类](images/app-tools-doesnotapply.png) | ![自动播放支持 windows 8.1 中此设备类](images/ap-tools.png)                   |
| 打印机、 扫描仪、 传真      | ![自动播放不支持 windows 8 中此设备类](images/app-tools-doesnotapply.png) | ![自动播放不支持 windows 8.1 中此设备类](images/app-tools-doesnotapply.png) |
| PC                           | ![自动播放不支持 windows 8 中此设备类](images/app-tools-doesnotapply.png) | ![自动播放不支持 windows 8.1 中此设备类](images/app-tools-doesnotapply.png) |
| 智能卡                   | ![自动播放不支持 windows 8 中此设备类](images/app-tools-doesnotapply.png) | ![自动播放支持 windows 8.1 中此设备类](images/ap-tools.png)                   |
| 常规的端口                 | ![自动播放不支持 windows 8 中此设备类](images/app-tools-doesnotapply.png) | ![自动播放支持 windows 8.1 中此设备类](images/ap-tools.png)                   |
| 蓝牙设备             | ![自动播放不支持 windows 8 中此设备类](images/app-tools-doesnotapply.png) | ![自动播放不支持 windows 8.1 中此设备类](images/app-tools-doesnotapply.png) |

 

## <a name="span-idbeforeyoubeginspanspan-idbeforeyoubeginspanspan-idbeforeyoubeginspanbefore-you-begin"></a><span id="Before_you_begin"></span><span id="before_you_begin"></span><span id="BEFORE_YOU_BEGIN"></span>开始之前的准备工作


-   **请确保具有设备元数据创建向导**。 你将需要它来启用自动播放。 在此版本中，此向导是包含在 Microsoft Visual Studio Professional 和 Microsoft Visual Studio Ultimate。 但如果你有 Microsoft Visual Studio Express 的 Windows，则需要下载[独立 SDK 的 Windows 8.1](https://go.microsoft.com/fwlink/p/?linkid=309209)获取向导。

-   **将您的应用程序与 Microsoft Store 相关联**。 你将需要你的应用程序包信息，若要启用自动播放。 有关详细信息，请参阅*将您的应用程序与 Microsoft Store 相关联*主题中[步骤 1:创建 UWP 设备应用](step-1--create-a-uwp-device-app.md)。

-   **创建设备元数据**。 如果你尚未开始，请参阅[步骤 2:创建设备元数据](step-2--create-device-metadata.md)中[构建循序渐进的 UWP 设备应用程序](build-a-uwp-device-app-step-by-step.md)指南。

## <a name="span-idenablingautoplayspanspan-idenablingautoplayspanspan-idenablingautoplayspanenabling-autoplay"></a><span id="Enabling_AutoPlay"></span><span id="enabling_autoplay"></span><span id="ENABLING_AUTOPLAY"></span>启用自动播放


**设备元数据创建向导**允许您声明 UWP 应用为你的设备的默认自动播放处理程序。 您还可以让其他 UWP 应用为你的设备的自动播放处理程序。 可以选择上述任何选项或这两种选项。

**若要启用自动播放与设备元数据创建向导**

1.  启动**设备元数据创建向导**从 *%programfiles （x86） %*\\Windows 工具包\\8.1\\bin\\x86，通过双击**DeviceMetadataWizard.exe**。
2.  单击**编辑设备元数据**。 这样就可以编辑现有的设备元数据包。
3.  在中**打开**对话框框中，找到与 UWP 设备应用程序相关联的设备元数据包。 (它具有**devicemetadata ms**文件扩展名。)
4.  （可选）。如果没有设备应用程序的包名称、 发布者名称和方便的应用程序 ID，请单击**应用信息**查看 UWP 设备应用的打包信息。
5.  单击**Windows 信息**指定自动播放详细信息。
6.  如果你想要指定应用为你的设备，选择的默认自动播放处理程序**使用 UWP 设备应用**。 您可以选择任何 UWP 应用或 UWP 设备应用，但该应用程序必须处理你的设备的自动播放激活并在应用包清单 （在下一个过程中指定） 中指定相应的体验 ID。
    -   **包名称**:在应用包清单中，这是标识元素的 Name 属性。
    -   **发布者名称**:在应用包清单中，这是标识元素的发布服务器属性。
    -   **应用程序 ID**:在应用包清单中，这是应用程序元素的 ID 属性。
    -   **谓词**:这是自动播放激活的标识符。 您的应用程序将使用它来确定是否激活来自你的设备。 可用于任何值对于谓词设置中，除**打开**，这保留的。
    -   **自动播放事件类型**:保留原样**设备**。 设备元数据，在该向导将自动指定与 UWP 设备应用程序关联的体验 ID。

7.  如果你想要让自动播放处理程序为你的设备，选择充当其他应用**启用的已注册应用的自动播放**。
8.  完成后，单击**下一步**。
9.  当您看见**完成**页上，记下**体验 ID**。 在应用程序中处理自动播放激活时，你将在下一步的过程中，需要它。
10. 验证你**将信息保存**然后单击**保存**来更新你的设备元数据包。

## <a name="span-idhandlingautoplayactivationspanspan-idhandlingautoplayactivationspanspan-idhandlingautoplayactivationspanhandling-autoplay-activation"></a><span id="Handling_AutoPlay_activation"></span><span id="handling_autoplay_activation"></span><span id="HANDLING_AUTOPLAY_ACTIVATION"></span>处理应用程序激活自动播放


若要处理在您的应用程序的自动播放激活，你需要注册`windows.autoPlayDevice`应用程序包中的扩展清单，然后处理该事件中的`OnActivated`事件，该应用程序对象。 请注意，您的应用程序可以将注册为多个设备的自动播放处理程序。

### <a name="span-idtoregisteryourappasanautoplayhandlerspanspan-idtoregisteryourappasanautoplayhandlerspanspan-idtoregisteryourappasanautoplayhandlerspanto-register-your-app-as-an-autoplay-handler"></a><span id="To_register_your_app_as_an_AutoPlay_handler"></span><span id="to_register_your_app_as_an_autoplay_handler"></span><span id="TO_REGISTER_YOUR_APP_AS_AN_AUTOPLAY_HANDLER"></span>若要将您的应用程序注册为一个自动播放处理程序

若要将您的应用程序注册为你的设备的自动播放处理程序，需要指定与 UWP 设备应用和自动播放相关联的体验 ID**谓词**并**ActionDisplayName** ，将用于激活您的应用程序。

1.  在 Microsoft Visual Studio 中打开应用的项目。
2.  在中**解决方案资源管理器**，右键单击**Package.appxmanifest**文件，然后选择**查看代码**。 这将显示在 XML （文本） 编辑器中的应用包清单。
3.  在中`Application`元素下面`VisualElements`元素中，粘贴以下`Extensions`元素插入包清单文件。
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

4.  此示例中的自动播放值替换为您的应用程序的实际值：
    -   `Verb`：这是自动播放激活的标识符。 您的应用程序将使用它来确定是否激活来自你的设备。 如果您的应用程序已指定为你的设备的默认自动播放处理程序，此值应匹配**谓词**设备元数据中指定的。 如果您的应用程序未指定为你的设备的默认自动播放处理程序，可用于任何值对于谓词设置中，除**打开**，这保留的。
    -   `ActionDisplayName`：自动播放会显示您的应用程序的字符串。
    -   `Experience ID`：体验将您的应用程序与你的设备相关联的 ID GUID。 这是你在前面过程中记下的值。

### <a name="span-idtohandleautoplayactivationspanspan-idtohandleautoplayactivationspanspan-idtohandleautoplayactivationspanto-handle-autoplay-activation"></a><span id="To_handle_AutoPlay_activation"></span><span id="to_handle_autoplay_activation"></span><span id="TO_HANDLE_AUTOPLAY_ACTIVATION"></span>若要处理自动播放激活

当你的设备触发自动播放激活时，激活类型将是`Windows.ApplicationModel.Activation.ActivationKind.device`。 使用`eventObj`对象通过传递`OnActivated`检查激活您的应用程序的方式。 如果它已从自动播放，则可以使用`eventObj`来确定哪些设备 ID 和自动播放谓词导致激活。

在此示例中，激活事件参数 (eventObj) 传送设备的 ID，以及激活的谓词。

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

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[满足 UWP 设备应用程序](meet-uwp-device-apps.md)

[分步构建 UWP 设备应用](build-a-uwp-device-app-step-by-step.md)

[借助自动播放功能自动启动](https://go.microsoft.com/fwlink/p/?LinkID=254861)

[启动、 恢复和多任务](https://go.microsoft.com/fwlink/p/?LinkID=309316)

 

 






