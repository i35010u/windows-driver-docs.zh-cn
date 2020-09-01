---
title: Windows Hello 相机驱动程序启动指南
description: 本主题讨论如何为红外 (IR) 照相机启用人脸身份验证，并将其用于 (Oem) 和独立硬件供应商 (Ihv) 的原始设备制造商。
ms.assetid: 5CE619F4-E136-4F8F-8F90-F7F96DE4642E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ea3c7a9465f7ccf552aa7372637d24bcc22b3cf3
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89186059"
---
# <a name="camera-driver-bring-up-guide"></a>相机驱动程序启动指南

本主题讨论如何为红外 (IR) 照相机启用人脸身份验证，并将其用于 (Oem) 和独立硬件供应商 (Ihv) 需要在其设备中提供此功能的原始设备制造商。

## <a name="frameserver"></a>FrameServer

下图显示了人脸身份验证如何通过 FrameServer 与新的驱动程序堆栈一起工作：

![windows hello 和 frameserver](images/windows-hello-device-model.png)

## <a name="face-authentication-ddis"></a>面部身份验证 DDIs

Windows 10 版本1607中提供了两个新的面部身份验证 DDI 构造，可支持 Windows Hello：

- **KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ FACEAUTH \_ 模式**

  此属性 ID 用于在驱动程序中使用以下标志来打开和配置人脸身份验证：

  - **\_已禁用 KSCAMERA EXTENDEDPROP \_ FACEAUTH \_ 模式 \_**

  - **KSCAMERA \_ EXTENDEDPROP \_ FACEAUTH \_ 模式 \_ 备用 \_ 帧 \_ 照明**

  - **KSCAMERA \_ EXTENDEDPROP \_ FACEAUTH \_ 模式 \_ 背景 \_ 减**

  有关此控件以及如何使用位标志设置面部身份验证模式的详细信息，请参阅 [**KSPROPERTY \_ CAMERACONTROL \_ EXTENDED \_ FACEAUTH \_ 模式**](./ksproperty-cameracontrol-extended-faceauth-mode.md) 主题。

- **MF \_ 捕获 \_ 元数据 \_ 帧 \_ 照明**

    此 IR 相机的元数据属性指定帧使用活动 IR 照明。 有关详细信息，请参阅 [捕获统计信息元数据特性](mf-capture-metadata.md) 主题中的必需元数据属性表。

## <a name="usb-camera-support"></a>USB 照相机支持

若要为设备上的红外照相机启用人脸身份验证，必须提供正确配置的 DeviceMFT 组件和 USB Video 类 (UVC) 扩展单元。

### <a name="configure-the-devicemft-component"></a>配置 DeviceMFT 组件

为了构建支持设备上的人脸身份验证的 DeviceMFT 组件，可使用 [sampledevicemft](/samples/microsoft/windows-driver-samples/driver-device-transform-sample/) 示例。

若要修改驱动程序示例，请对示例源代码进行以下更改：

1. 在 DeviceMFT 组件中添加源类型信息

1. 标记 DeviceMFT 组件中的照明标志

1. 转换 DeviceMFT 组件中的 IKSControl，以与将在下一节中生成的 UVC 扩展单元通信：

### <a name="build-a-usb-video-class-uvc-extension-unit"></a> (UVC) 扩展单元生成 USB 视频类

若要为设备生成 UVC 扩展单元，请按照 [生成扩展单元示例控件](building-the-extension-unit-sample-control.md)中的说明进行操作。 本主题介绍了如何创建所需的项目文件，并提供了以下主题中的示例代码的链接：

[UVC 扩展单元](sample-interface-for-uvc-extension-units.md) (包含 *接口 .Idl* 的示例接口) 

[示例扩展单元 DLL](sample-extension-unit-plug-in-dll.md) (包含 *Xuproxy* 和 *Xuproxy*) 

[UVC 扩展单元](sample-registry-entry-for-uvc-extension-units.md) (包含 *Xusample* 的示例注册表项) 

[UVC 扩展单元 (包含 TestApp 的示例应用程序](sample-application-for-uvc-extension-units.md)) *TestApp.cpp*

[支持扩展单元的自动更新事件](supporting-autoupdate-events-with-extension-units.md)

[示例扩展单元描述符](sample-extension-unit-descriptor.md)

[提供 UVC INF 文件](providing-a-uvc-inf-file.md)

有关示例代码模块如何协同工作的详细信息，请参阅 [扩展单元插件体系结构](extension-unit-plug-in-architecture.md) 主题。

## <a name="inf-file-entries"></a>INF 文件条目

若要将 UVC 设备注册到 **KSCATEGORY \_ 传感器 \_ 相机**下，应指定传感器相机促销标志：

```INF
HKR,,SensorCameraMode,0x00010001,0x00000001
```

若要将此照相机从常规相机应用隐藏，因为它没有 RGB 流，请按如下所示使用 skip 枚举标志：

```INF
HKR,,SkipCameraEnumeration,0x00010001,0x00000001
```

这将从 **KSCATEGORY \_ 视频**中删除相机，这会阻止定期相机应用对其进行枚举。

**SkipCameraEnumeration**和**SensorCameraMode**条目都应放置在 INF 文件的**DDInstall**节中。

## <a name="hlk-tests-for-kscategory_sensor_camera-to-assist-driver-testing"></a>用于 KSCATEGORY 传感器相机的 HLK 测试 \_ \_ ，以协助驱动程序测试

硬件徽标工具包 (需要对 IR 和 RGB 照相机模块进行测试) 测试。 此测试验证用于 Windows Hello 人脸身份验证的 RGB 和 IR 相机的基本功能。 在 HLK 测试套件中已经指定了 RGB 相机要求。

这些是红外照相机模块需要通过的测试：

1. 枚举所有 KS 传感器类别相机：

    - 支持 IR 流的设备必须位于 "传感器相机" \_ 类别下。

    - 支持 RGB 流的设备会在视频 \_ 摄像机类别下进行。

    - 仅适用于支持 IR 和 RGB 流的单个照相机设备，应在两个 KSCAMERA 类别下注册该设备：传感器 \_ 相机和摄像机 \_ 。

1. 查找定义了 **MF \_ DEVICESTREAM \_ 属性 \_ FACEAUTH \_ 功能** 属性的流：

    - 如果没有为 stream 定义 **MF \_ DEVICESTREAM \_ 属性 \_ FACEAUTH \_ 功能** 属性，则跳过测试。

    - 如果多个流定义了 **MF \_ DEVICESTREAM \_ 属性 \_ FACEAUTH \_ 功能** 属性，则测试将失败，因为只有一个流应支持 Windows Hello。

    - 如果未对此流将 **MF \_ DEVICESTREAM \_ 属性 \_ FRAMESOURCE \_ 类型** 设置为 IR，则测试将失败，因为此流中不能有 RGB 媒体类型。

    - 选择此流，并验证该媒体类型是否为支持 Windows Hello 的 (MJPG/L8/NV12) 并且分辨率是否大于或等于 320 x 320 像素：

        1. 如果支持人脸身份验证配置文件，则验证此流中的配置文件媒体类型。

        1. 如果不支持人脸身份验证配置文件，请验证此流的默认媒体类型。

    - 检查对面部身份验证 DDI 中某个属性的支持：发亮/无发亮或环境减。

    - 将 KS 属性设置为支持的属性。

    - 启动流式处理

1. 检查运行时属性：

    - 验证用于对元数据进行人脸身份验证的 (预览测试) 。

    - 验证 "启动时间" 是否小于500毫秒 (预览测试是否具有元数据) 的人脸身份验证。
  
    - 使用以下参数以最小帧速率验证流式处理： 15 FPS 亮起，15 FPS 环境或 15 FPS 环境，分辨率大于或等于 320 x 320 像素，媒体类型为

        1. 如果 "亮起" 属性处于启用状态，则检查帧上的元数据 (以 15 FPS) 的亮起/非亮起对帧。

        1. 如果启用了环境减法属性，请在 15 FPS) 检查帧上是否没有元数据 (环境帧。

1. “停止流式传输”

1. 取消设置 KS 控件

1. RGB + IR 的并发性：根据相机配置文件中的定义进行测试

如果未通过上述的 HLK 测试，Microsoft 将不会向 OEM 发出签名的驱动程序，并且 Windows Hello 将不会运行。

## <a name="related-topics"></a>相关主题

[使用 MediaCapture 捕获照片和视频](/windows/uwp/audio-video-camera/capture-photos-and-video-with-mediacapture)  

[Windows. Media. 捕获命名空间](/uwp/api/Windows.Media.Capture)