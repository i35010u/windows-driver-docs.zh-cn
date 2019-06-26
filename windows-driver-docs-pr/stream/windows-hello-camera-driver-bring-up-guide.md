---
title: Windows Hello 照相机驱动程序显示指南
description: 本主题介绍如何启用红外 (IR) 照相机的人脸身份验证，并适用于原始设备制造商 (Oem) 和独立硬件供应商 (Ihv)。
ms.assetid: 5CE619F4-E136-4F8F-8F90-F7F96DE4642E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a5c36f71847f5565d0312721c72f053d8f126260
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385358"
---
# <a name="camera-driver-bring-up-guide"></a>相机驱动程序启动指南

本主题介绍如何启用红外 (IR) 照相机的人脸身份验证，并适用于原始设备制造商 (Oem) 和独立硬件供应商 (Ihv) 想要提供此功能在其设备中。

## <a name="frameserver"></a>FrameServer

下图显示了与 FrameServer 通过新的驱动程序堆栈的人脸身份验证工作原理：

![windows 你好和 frameserver](images/windows-hello-device-model.png)

## <a name="face-authentication-ddis"></a>人脸验证 DDIs

在 Windows 10，版本 1607 支持 Windows Hello 中提供了两个新的人脸验证 DDI 构造：

-   **KSPROPERTY\_CAMERACONTROL\_扩展\_FACEAUTH\_模式**

    此属性 ID 用于启用和配置中使用以下标记的驱动程序的人脸身份验证：

    -   **KSCAMERA\_EXTENDEDPROP\_FACEAUTH\_模式\_已禁用**

    -   **KSCAMERA\_EXTENDEDPROP\_FACEAUTH\_MODE\_ALTERNATIVE\_FRAME\_ILLUMINATION**

    -   **KSCAMERA\_EXTENDEDPROP\_FACEAUTH\_模式\_背景\_减法**

    有关此控件以及如何使用位标志设置的人脸身份验证模式的详细信息，请参阅[ **KSPROPERTY\_CAMERACONTROL\_扩展\_FACEAUTH\_模式** ](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-faceauth-mode)主题。

-   **MF\_捕获\_元数据\_帧\_照明**

    IR 照相机此元数据属性指定使用帧 active IR 照明。 有关详细信息，请参阅**必需的元数据特性**表中[照片捕获反馈](standardized-extended-controls-.md#photo-capture-feedback-applied-device-settings)一部分[扩展相机控件](standardized-extended-controls-.md)主题。

## <a name="usb-camera-support"></a>USB 摄像头支持

若要启用你的设备上的红外相机的人脸身份验证，必须提供正确配置的 DeviceMFT 组件和 USB 视频类 (UVC) 扩展单元。

### <a name="configure-the-devicemft-component"></a>配置 DeviceMFT 组件

作为起始点的构建 DeviceMFT 组件来支持在设备上的人脸身份验证可以使用[sampledevicemft](https://github.com/Microsoft/Windows-driver-samples/tree/master/avstream/sampledevicemft)示例位于[Windows 驱动程序示例](https://github.com/Microsoft/Windows-driver-samples)上的存储库GitHub。

若要修改驱动程序示例，请下载并提取[Windows 驱动程序示例 master.zip](https://github.com/Microsoft/Windows-driver-samples/archive/master.zip)，或者，使用 git 克隆到开发计算机的 Windows 驱动程序示例存储库或。 导航到**sampledevicemft**示例位于**avstream**文件夹，然后进行下列更改的示例源代码：

1.  添加 DeviceMFT 组件中的源类型信息

2.  标记 DeviceMFT 组件中的照明标志

3.  将转换 IKSControl DeviceMFT 组件中，将生成下一节中的 UVC 扩展单元与进行通信：

### <a name="build-a-usb-video-class-uvc-extension-unit"></a>生成一个 USB 视频类 (UVC) 扩展单元

若要生成一个 UVC 扩展单元，以便你的设备，请按照中的说明[生成扩展单元示例控件](building-the-extension-unit-sample-control.md)。 本主题包含创建所需的项目文件的信息，并提供指向以下主题中的示例代码：

[示例 UVC 扩展单位的接口](sample-interface-for-uvc-extension-units.md)(包含*Interface.idl*)

[示例扩展单元插件 DLL](sample-extension-unit-plug-in-dll.md) (包含*Xuproxy.h*并*Xuproxy.cpp*)

[UVC 扩展单位的示例注册表条目](sample-registry-entry-for-uvc-extension-units.md)(包含*Xusample.rgs*)

[UVC 扩展单位的示例应用程序](sample-application-for-uvc-extension-units.md)(包含*TestApp.cpp*)

[支持扩展单位的自动更新事件](supporting-autoupdate-events-with-extension-units.md)

[示例扩展单元描述符](sample-extension-unit-descriptor.md)

[提供 UVC INF 文件](providing-a-uvc-inf-file.md)

请参阅[扩展单元插件体系结构](extension-unit-plug-in-architecture.md)示例代码模块如何协同工作的详细信息的主题。

## <a name="inf-file-entries"></a>INF 文件条目


若要注册 UVC 设备受**KSCATEGORY\_传感器\_照相机**，应指定传感器照相机升级标志：

```INF
HKR,,SensorCameraMode,0x00010001,0x00000001
```

若要隐藏此摄像机从正则相机应用程序，因为它具有不 RGB 流，请使用跳过枚举标志，如下所示：

```INF
HKR,,SkipCameraEnumeration,0x00010001,0x00000001
```

此操作将删除从照相机**KSCATEGORY\_视频**，这将阻止该服务从被枚举通过旧的枚举由正则相机应用。

这两个**SkipCameraEnumeration**并**SensorCameraMode**应将条目放在**DDInstall.HW** INF 文件部分。

## <a name="hlk-tests-for-kscategorysensorcamera-to-assist-driver-testing"></a>HLK 测试 KSCATEGORY\_传感器\_照相机以帮助驱动程序测试


硬件徽标工具包 (HLK) 测试是必需的红外线 （ir） 和 RGB 照相机模块。 此测试验证 RGB 和 IR 照相机用于 Windows Hello 面部身份验证的基本功能。 RGB 照相机要求已 HLK 测试套件中进行指定。

这些都是将需要传递的用于启用红外线 （ir） 照相机模块的测试：

1.  枚举所有 KS 传感器类别照相机：

    -   支持红外线 （ir） 流的设备必须位于传感器\_照相机类别。

    -   支持 RGB 流的设备在视频下转\_照相机类别。

    -   仅对于单个照相机设备支持红外线 （ir） 和 RGB 流，应注册这两个 KSCAMERA 类别下的设备：传感器\_照相机和视频\_照相机。

2.  查找流具有**MF\_DEVICESTREAM\_特性\_FACEAUTH\_功能**定义属性：

    -   如果没有流具有**MF\_DEVICESTREAM\_特性\_FACEAUTH\_功能**属性定义，然后跳过测试。

    -   如果有多个流**MF\_DEVICESTREAM\_特性\_FACEAUTH\_功能**属性定义的失败测试，因为只有一个流应该是 Windows hello 企业支持。

    -   如果**MF\_DEVICESTREAM\_特性\_框架资源\_类型**是不为此流将设置为红外线 （ir），使测试失败，因为此流上，无法 RGB 媒体类型。

    -   选择此流，并验证的媒体类型是支持 Windows Hello (MJPG/L8/NV12) 和解决方法是大于或等于 320 x 320 像素：

        1.  如果支持人脸身份验证配置文件，然后验证此流的配置文件的媒体类型。

        2.  如果不支持人脸身份验证配置文件，验证此流的默认媒体类型。

    -   检查对人脸验证 DDI 中的属性之一的支持：照亮/未经 illuminated 或环境减法。

    -   KS 属性设置为一个受支持。

    -   启动流式处理

3.  检查运行时属性：

    -   验证时间戳精度 （进行人脸验证所使用的元数据的预览测试）。

    -   验证该启动小于 500 毫秒 （进行人脸验证所使用的元数据的预览测试）。

    -   验证流式处理以使用以下参数的最小的帧速率：15 FPS 照明和 15 FPS 环境或 15 FPS 环境减去分辨率大于或等于 320 x 320 像素，媒体上，键入 L8/NV12 的正数 stride 示例：

        1.  如果启用了照明的属性，检查的帧 （照亮/非照亮对帧在 15 帧/秒） 的元数据。

        2.  如果启用了环境减法属性，检查的帧 （环境帧在 15 帧/秒） 的任何元数据。

4.  “停止流式传输”

5.  取消设置 KS 控件

6.  并发性 RGB + 红外线 （ir）： 如果照相机配置文件中定义测试

如果不传递上面列出的 HLK 测试，Microsoft 不会为 OEM，颁发签名的驱动程序和 Windows Hello 将不起作用。

## <a name="related-topics"></a>相关主题

[捕获照片和视频 MediaCapture](https://docs.microsoft.com/windows/uwp/audio-video-camera/capture-photos-and-video-with-mediacapture)  

[Windows.Media.Capture namespace](https://docs.microsoft.com/uwp/api/Windows.Media.Capture)  
