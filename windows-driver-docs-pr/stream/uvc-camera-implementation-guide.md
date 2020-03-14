---
title: Windows 10 UVC 相机实现指南
description: 概述如何通过收件箱驱动程序向应用程序公开 USB 视频类兼容相机的某些功能。
ms.date: 08/16/2019
ms.localizationpriority: medium
ms.openlocfilehash: 54b87f5f4ec0d42376246e22417851a8640a9b14
ms.sourcegitcommit: b316c97bafade8b76d5d3c30d48496915709a9df
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/13/2020
ms.locfileid: "79243050"
---
# <a name="windows-10-uvc-camera-implementation-guide"></a>Windows 10 UVC 相机实现指南

Windows 10 为符合 USB 视频类规范的设备提供了一个收件箱 USB 视频类（UVC）驱动程序（版本1.0 到1.5）。 此驱动程序支持颜色和传感器类型相机。 本文档概述了如何通过收件箱驱动程序向应用程序公开 UVC 兼容相机的某些功能。

## <a name="terminology"></a>术语

| 关键字              | 说明                                                                  |
|----------------------|------------------------------------------------------------------------------|
| UVC                  | USB 视频类                                                              |
| UVC 驱动程序           | 操作系统附带的 USBVideo 驱动程序                                   |
| IR                   | 红外线                                                                     |
| 彩色照相机         | 输出彩色流的照相机（例如 RGB 或 YUV 相机）      |
| 传感器相机        | 输出非颜色流的照相机（例如，IR 或深度相机） |
| BOS                  | 二进制设备对象存储                                                   |
| MS OS 2.0 描述符 | Microsoft 平台特定 BOS 设备功能描述符                 |

## <a name="sensor-cameras"></a>传感器相机

Windows 支持两种类型的相机。 一个是彩色相机，另一个是非彩色传感器相机。 RGB 或 YUV 相机被分类为彩色相机和非彩色相机，如灰色刻度、IR 和深度相机分类为传感器相机。 UVC 驱动程序支持这两种类型的相机。 建议照相机固件指定一个值，该值基于 UVC 驱动程序在一个或两个受支持的类别下注册照相机的值。

支持仅颜色格式类型的照相机应在 KSCATEGORY\_视频\_照相机下进行注册。 支持 IR 或仅深度格式类型的照相机应在 KSCATEGORY\_传感器\_照相机下进行注册。 支持颜色和非颜色格式类型的照相机应在 KSCATEGORY\_视频\_相机和 KSCATEGORY\_传感器\_相机中进行注册。 此分类可帮助应用程序选择他们想要使用的相机。

UVC 照相机可以通过属性**SensorCameraMode**和**SkipCameraEnumeration**指定其类别首选项，其 BOS [MS OS 2.0 描述符](https://docs.microsoft.com/windows-hardware/drivers/usbcon/microsoft-defined-usb-descriptors)在以下各节中详细说明。

属性**SensorCameraMode**的值为1或2。

如果值为1，则将在 KSCATEGORY\_传感器\_照相机下注册设备。 除了将**SkipCameraEnumeration**的值指定为1外，还可以使相机仅适用于查看传感器相机的应用程序。 仅限显示传感器相机媒体类型的相机应使用此值。

如果**SensorCameraMode**的值为2，将在 KSCATEGORY\_\_传感器下 &AMP;\_视频\_照相机注册设备。 这会使相机适用于查找传感器和彩色照相机的应用程序。 同时公开传感器相机和彩色相机介质类型的相机应使用此值。

建议使用 BOS 描述符指定上面提到的注册表值。 请参阅下面的[示例复合设备](#example-composite-device)部分，获取带有特定于平台的 MS OS 2.0 描述符的示例 BOS 描述符。

如以上所述，如果无法更新设备固件，则可以使用自定义 INF，并通过指定**SensorCameraMode**和**SkipCameraEnumeration**的值，指定照相机需要注册为传感器相机，如下所示：

自定义 INF 文件（基于收件箱 UVC 驱动程序）必须包含以下 AddReg 条目：

**SensorCameraMode**： REG\_DWORD：1（注册为传感器相机）

**SkipCameraEnumeration**： REG\_DWORD：1（仅适用于 IR 应用程序）

自定义 INF 部分的示例如下所示：

```INF
[USBVideo.NT.HW]
AddReg=USBVideo.HW.AddReg

[USBVideo.HW.AddReg]
HKR,, SensorCameraMode, 0x00010001,1      ; places the value under device HW
                                          ; Registry key

HKR,, SkipCameraEnumeration, 0x00010001,1 ; This makes the camera available
                                          ; only for application looking for
                                          ; IR cameras
```

如果固件或 INF 中未指定**SensorCameraMode**和**SkipCameraEnumeration**属性，照相机将被注册为彩色相机，并且仅对已识别相机的应用程序可见。

## <a name="ir-stream"></a>IR 流

Windows 收件箱 USB 视频类（UVC）驱动程序支持以 YUV 格式捕获场景的相机，并通过 USB 以未压缩的 YUV 或压缩的 MJPEG 帧形式传输像素数据。

以下格式类型 Guid 应在流视频格式描述符中指定，如 WDK ksmedia 头文件中定义的那样：

| 类型 | 说明 |
| --- | --- |
| KSDATAFORMAT\_子类型\_L8\_IR |  未压缩的8位亮度平面。 此类型映射到[MFVideoFormat\_L8](https://docs.microsoft.com/windows/desktop/medfound/video-subtype-guids#luminance-and-depth-formats)。 |
| KSDATAFORMAT\_L16\_子类型\_IR | 未压缩的16位亮度平面。 此类型映射到[MFVideoFormat\_L16](https://docs.microsoft.com/windows/desktop/medfound/video-subtype-guids#luminance-and-depth-formats)。 |
| KSDATAFORMAT\_MJPG\_子类型\_IR | 压缩的 MJPEG 帧。 媒体基础将其转换为 NV12 未压缩的帧并仅使用亮度平面。 |

当在帧描述符的 guidFormat 字段中指定这些格式类型 Guid 时，媒体基础捕获管道会将流标记为 IR 流。 使用媒体基础 FrameReader API 编写的应用程序将能够使用 IR 流。 对于 IR 流，管道不支持 IR 帧的缩放或转换。

公开 IR 格式类型的流不能公开 RGB 或深度格式类型。

```cpp
// Example Format Descriptor for UVC 1.1 frame based format

typedef struct _VIDEO_FORMAT_FRAME
{
    UCHAR bLength;
    UCHAR bDescriptorType;
    UCHAR bDescriptorSubtype;
    UCHAR bFormatIndex;
    UCHAR bNumFrameDescriptors;
    GUID  guidFormat;  // this field should contain the IR subtype GUID
    UCHAR bBitsPerPixel;
    UCHAR bDefaultFrameIndex;
    UCHAR bAspectRatioX;
    UCHAR bAspectRatioY;
    UCHAR bmInterlaceFlags;
    UCHAR bCopyProtect;
    UCHAR bVariableSize;
} VIDEO_FORMAT_FRAME, *PVIDEO_FORMAT_FRAME;
```

> [!NOTE]
> IR 流将显示为 DShow 中的常规捕获流。

## <a name="depth-stream"></a>深度流

Windows 收件箱 USB 视频类驱动程序支持生成深度流的相机。 这些相机捕获场景的详细信息（例如航班时间），并通过 USB 以未压缩的 YUV 帧形式传输深度地图。 应在流视频格式描述符中指定以下格式类型 GUID，如 WDK ksmedia 头文件中定义的那样：

| 类型 | 说明 |
| --- | --- |
| KSDATAFORMAT\_D16\_子类型 |  16位深度映射值。 此类型与[MFVideoFormat\_D16](https://docs.microsoft.com/windows/desktop/medfound/video-subtype-guids#luminance-and-depth-formats)相同。 值为毫米。 |

当在帧描述符的 guidFormat 成员中指定格式类型 GUID 时，媒体基础捕获管道会将流标记为深度流。 使用 FrameReader API 编写的应用程序将能够使用深度流。 对于深度流，管道不支持深度帧的缩放或转换。

流公开深度格式类型不得公开 RGB 或 IR 格式类型。

```cpp
// Example Format Descriptor for UVC 1.1 frame based format
typedef struct _VIDEO_FORMAT_FRAME
{
    UCHAR bLength;
    UCHAR bDescriptorType;
    UCHAR bDescriptorSubtype;
    UCHAR bFormatIndex;
    UCHAR bNumFrameDescriptors;
    GUID guidFormat; // this field should contain the IR subtype GUID
    UCHAR bBitsPerPixel;
    UCHAR bDefaultFrameIndex;
    UCHAR bAspectRatioX;
    UCHAR bAspectRatioY;
    UCHAR bmInterlaceFlags;
    UCHAR bCopyProtect;
    UCHAR bVariableSize;
} VIDEO_FORMAT_FRAME, *PVIDEO_FORMAT_FRAME;
```

> [!NOTE]
> 深度流在 DShow 中显示为常规捕获流。

## <a name="grouping-cameras"></a>分组相机

Windows 支持根据其容器 ID 对照相机分组，以帮助应用程序使用相关相机。 例如，在同一物理设备上出现 IR 相机和彩色照相机时，可以将其作为相关相机公开给操作系统。 这会使应用程序（如 Windows Hello）在应用场景中使用相关相机。

相机功能之间的关系可以在固件中照相机的 BOS 描述符中指定。 UVC 驱动程序将利用此信息，并将这些相机功能公开为相关。 这会使 OS 相机堆栈将它们作为一组相关的摄像机公开给应用程序。

照相机固件必须指定*UVC-FSSensorGroupID*，它是带有大括号的字符串格式的 GUID。 具有相同*UVC-FSSensorGroupID*的相机将组合在一起。

可以通过在固件中指定*UVC-FSSensorGroupName*（一个 Unicode 字符串）来指定传感器组的名称。

请参阅下面的示例复合设备部分，了解用于指定*UVC-FSSensorGroupID*和*UVC-FSSensorGroupName*的演示示例 BOS。

如以上所述，如果你无法更新设备固件，则可以使用自定义 INF，并通过指定传感器组 ID 和名称来指定你的相机属于传感器组，如下所示。 自定义 INF 文件（基于收件箱 UVC 驱动程序）必须包含以下 AddReg 条目：

**FSSensorGroupID**： REG_SZ： "{你的传感器组 ID GUID}"

**FSSensorGroupName**： REG_SZ： "你的传感器组友好名称"

自定义 INF 部分的示例如下所示：

```INF
[USBVideo.NT.Interfaces]
AddInterface=%KSCATEGORY_CAPTURE%,GLOBAL,USBVideo.Interface
AddInterface=%KSCATEGORY_RENDER%,GLOBAL,USBVideo.Interface
AddInterface=%KSCATEGORY_VIDEO%,GLOBAL,USBVideo.Interface
AddInterface=%KSCATEGORY_RENDER_EXT%,GLOBAL,USBVideo.Interface
AddInterface=%KSCATEGORY_VIDEO_CAMERA%,GLOBAL,USBVideo.Interface

[USBVideo.Interface]
AddReg=USBVideo.Interface.AddReg

[USBVideo.Interface.AddReg]
HKR,,CLSID,,%ProxyVCap.CLSID%
HKR,,FriendlyName,,%USBVideo.DeviceDesc%
HKR,,RTCFlags,0x00010001,0x00000010
HKR,, FSSensorGroupID,0x00000000,%FSSensorGroupID%
HKR,, FSSensorGroupName,0x00000000,%FSSensorGroupName%
```

> [!NOTE]
> DShow 捕获管道不支持传感器组。

## <a name="method-2-or-method-3-still-capture-support"></a>方法2或方法3仍捕获支持

UVC 规范提供一种机制，用于指定视频流接口是否支持方法1/2/3 类型静止图像捕获。 为了使 OS 利用设备的方法2/3 静止图像捕获支持，通过 UVC 驱动程序，设备固件可以在 BOS 描述符中指定一个值。

为启用方法2/3 仍为映像捕获指定的值为名为*UVC-EnableDependentStillPinCapture*的 DWORD。 使用 BOS 说明符指定其值。 下面的[示例复合设备](#example-composite-device)演示如何使用示例 BOS 描述符启用静态图像捕获。

如以上所述，如果无法更新设备固件，则可以使用自定义 INF 来指定相机支持方法2或方法3仍捕获方法。

自定义 INF 文件（基于自定义 UVC 驱动程序或收件箱 UVC 驱动程序）必须包含以下 AddReg 项：

**EnableDependentStillPinCapture**： REG_DWORD：0X0 （Disabled）到0X1 （已启用）

如果此项设置为 "已启用（0x1）"，捕获管道将利用方法2/3 进行静止映像捕获（假设该固件还公布对 UVC spec 指定的方法2/3 的支持）。

自定义 INF 部分的示例如下所示：

```INF
[USBVideo.NT.Interfaces]
AddInterface=%KSCATEGORY_CAPTURE%,GLOBAL,USBVideo.Interface
AddInterface=%KSCATEGORY_RENDER%,GLOBAL,USBVideo.Interface
AddInterface=%KSCATEGORY_VIDEO%,GLOBAL,USBVideo.Interface
AddInterface=%KSCATEGORY_RENDER_EXT%,GLOBAL,USBVideo.Interface
AddInterface=%KSCATEGORY_VIDEO_CAMERA%,GLOBAL,USBVideo.Interface

[USBVideo.Interface]
AddReg=USBVideo.Interface.AddReg

[USBVideo.Interface.AddReg]
HKR,,CLSID,,%ProxyVCap.CLSID%
HKR,,FriendlyName,,%USBVideo.DeviceDesc%
HKR,,RTCFlags,0x00010001,0x00000010
HKR,,EnableDependentStillPinCapture,0x00010001,0x00000001
```

## <a name="device-mft-chaining"></a>设备 MFT 链接

设备 MFT 是推荐用于 Ihv 和 Oem 的用户模式插件机制，用于在 Windows 上扩展相机功能。 在 Windows 10 版本1703之前，照相机管道仅支持一个 DMFT 扩展插件。 从 Windows 10 版本1703开始，Windows 相机管道支持可选的 DMFTs 链，最多包含三个 DMFTs。 这为 Oem 和 Ihv 提供了更大的灵活性，以便以 post 处理相机流的形式提供增值。 例如，设备可以将 PDMFT 与 IHV DMFT 和 OEM DMFT 一起使用。 下图说明了涉及一系列 DMFTs 的体系结构。

![DMFT 链](images/dmft-chain.png)

捕获示例从相机驱动程序流式传输到 DevProxy，然后浏览 DMFT 链。 链中的每个 DMFT 都有机会处理该示例。 如果 DMFT 不想处理该示例，则可以直接将该示例传递到下一个 DMFT。

对于 KsProperty 之类的控件，调用将会进入流–链中的最后一个 DMFT 将首先获取调用，可以在那里处理调用，或将其传递给链中的上一个 DMFT。

错误将从 DMFT 传播到应用程序。 对于 IHV/OEM DMFTs，DMFT 中的任何一个实例都无法实例化，这将是 DTM 的严重错误。

对 DMFTs 的要求：

- DMFT 的输入插针计数必须与之前 DMFT 的输出插针计数匹配，否则，DTM 会在初始化时失败。 但是，相同 DMFT 的输入和输出插针计数不需要匹配。

- DMFT 需要支持接口-IMFDeviceTransform、IMFShutdown、IMFRealTimeClientEx、IKsControl 和 IMFMediaEventGenerator;如果配置了 MFT0，或者链中的下一个 DMFT 需要 IMFTransform 支持，则可能需要支持 IMFTransform。

- 在不使用框架服务器的64位系统上，必须注册32位和64位的 DMFTs。 如果 USB 摄像机可能会插入任意系统，对于 "外部" （或非收件箱） USB 摄像机，USB 照相机供应商应同时提供32位和64位的 DMFTs。

## <a name="configuring-the-dmft-chain"></a>配置 DMFT 链

照相机设备可以选择使用使用收件箱 USBVideo 部分的自定义 INF 文件来提供 DLL 中的 DMFT COM 对象。

在 "自定义"。INF 文件的 "Interface AddReg" 部分，通过添加以下注册表项来指定 DMFT Clsid：

**CameraDeviceMftCLSIDChain** （REG\_多\_SZ）% Dmft0。CLSID%，% Dmft。CLSID%，% Dmft2。CLSID

如下面的示例 INF 设置中所示（替换% Dmft0。CLSID% 和% Dmft1% with 用于 DMFTs 的实际 CLSID 字符串），Windows 10 中最多允许有2个 Clsid，版本1703，第一个 Clsid 最接近 DevProxy，最后一项是链中的最后一个 DMFT。

平台 DMFT CLSID 为 {3D096DDE-8971-4AD5-98F9-C74F56492630}。

示例**CameraDeviceMftCLSIDChain**设置：

- *无 IHV/OEM DMFT 或平台 DMFT*

  - CameraDeviceMftCLSIDChain = "" （或者无需指定此注册表项）

- *IHV/OEM DMFT*

  - CameraDeviceMftCLSIDChain =% Dmft。CLSID

- *平台 DMFT &lt;-&gt; IHV/OEM DMFT*

  - CameraDeviceMftCLSIDChain = "{3D096DDE-8971-4AD5-98F9-C74F56492630}"，% Dmft。CLSID

  - 下面是一个屏幕截图，其中包含平台 DMFT 的 USB 摄像机的结果注册表项，以及链中的 DMFT （GUID 为 {D671BE6C-FDB8-424F-81D7-03F5B1CE2CC7}）。

![注册表编辑器 DMFT 链](images/dmft-registry-editor.png)

- *IHV/OEM DMFT0 &lt;-&gt; IHV/OEM DMFT1*

  - CameraDeviceMftCLSIDChain =% Dmft0。CLSID%，% Dmft1。CLSID%，

> [!NOTE]
> **CameraDeviceMftCLSIDChain**最多可以有两个 clsid。

如果配置了**CameraDeviceMftCLSIDChain** ，则 DTM 将跳过旧的 CameraDeviceMftCLSID 设置。

如果未配置**CameraDeviceMftCLSIDChain** ，并且配置了旧版 CameraDeviceMftCLSID，则该链将如下所示（如果启用了平台 DMFT 和平台 DMFT 的 USB 摄像机，并已启用平台） DevProxy &lt;–&gt; 平台 DMFT &lt;–&gt; OEM/IHV DMFT 或（如果禁用了平台 DMFT 或平台 DMFT，则 DevProxy &lt;-OEM/IHV DMFT。&gt;

示例 INF 文件设置：

```INF
[USBVideo.Interface.AddReg]
HKR,,CLSID,,%ProxyVCap.CLSID%
HKR,,FriendlyName,,%USBVideo.DeviceDesc%
HKR,,RTCFlags,0x00010001,0x00000010
HKR,,EnablePlatformDmft,0x00010001,0x00000001
HKR,,DisablePlatformDmftFeatures,0x00010001,0x00000001
HKR,,CameraDeviceMftCLSIDChain, 0x00010000,%Dmft0.CLSID%,%Dmft1.CLSID%
```

## <a name="platform-device-mft"></a>平台设备 MFT

从 Windows 10 1703 版开始，Windows 提供了一个收件箱设备 MFT，适用于 UVC 照相机（称为平台 DMFT （PDMFT））。 此 DMFT 允许 Ihv 和 Oem 利用 Windows 提供的后处理算法。

| 平台 DMFT 支持的功能 | Windows 版本 |
|-------------------------------------|-----------------|
| 启用基于人脸的感兴趣区域（ROI），以便在支持 ROI 的 USB 摄像机中进行3A 调整。 | Windows 10 版本 1703 |

> [!NOTE]
> 如果相机不支持基于 UVC 1.5 的 ROI，则即使设备选择使用 PDMFT，PDMFT 也不会加载。

UVC 照相机可以通过指定 EnablePlatformDmft 到 BOS 描述符来选择使用平台 DMFT。

要指定启用平台 DMFT 的值是使用*UVC-EnablePlatformDmft*的 DWORD，并使用 BOS 说明符指定其值。 下面的[示例复合设备](#example-composite-device)部分演示如何启用平台 DMFT，并提供示例 BOS 描述符。

如以上所述，如果无法更新设备固件，则可以使用自定义 INF 文件为设备启用平台 DMFT。

自定义 INF 文件（基于自定义 UVC 驱动程序或收件箱 UVC 驱动程序）必须包含以下 AddReg 项：

**EnablePlatformDmft**： REG_DWORD：0X0 （Disabled）到0X1 （已启用）

如果此项设置为 "已启用（0x1）"，捕获管道将使用收件箱平台 DMFT 作为设备。 下面显示了此自定义 INF 部分的示例：

```INF
[USBVideo.NT.Interfaces]
AddInterface=%KSCATEGORY_CAPTURE%,GLOBAL,USBVideo.Interface
AddInterface=%KSCATEGORY_RENDER%,GLOBAL,USBVideo.Interface
AddInterface=%KSCATEGORY_VIDEO%,GLOBAL,USBVideo.Interface
AddInterface=%KSCATEGORY_RENDER_EXT%,GLOBAL,USBVideo.Interface
AddInterface=%KSCATEGORY_VIDEO_CAMERA%,GLOBAL,USBVideo.Interface

[USBVideo.Interface]
AddReg=USBVideo.Interface.AddReg

[USBVideo.Interface.AddReg]
HKR,,CLSID,,%ProxyVCap.CLSID%
HKR,,FriendlyName,,%USBVideo.DeviceDesc%
HKR,,RTCFlags,0x00010001,0x00000010
HKR,,EnablePlatformDmft,0x00010001,0x00000001
```

在 Windows 10 版本1703中，如果设备使用 PDMFT，则会启用 PDMFT 支持的所有功能（基于设备功能）。 不支持精细配置 PDMFT 功能。

## <a name="face-auth-profile-via-ms-os-descriptors"></a>通过 MS OS 描述符的人脸身份验证配置文件

Windows 10 RS5 现对具有 Windows Hello 支持的任何照相机强制执行人脸身份验证配置文件 V2 要求。 对于使用自定义相机驱动程序堆栈的基于 MIPI 的系统，可以通过 INF （或扩展 INF）或者通过用户模式插件（设备 MFT）发布此支持。

但对于 USB 视频设备，使用基于 UVC 的相机的约束是，对于 Windows 10 19H1，不允许使用自定义相机驱动程序。 所有基于 UVC 的相机必须使用收件箱 USB 视频类驱动程序，并且必须以设备 MFT 的形式实现任何供应商扩展。

对于许多 OEM/Odm，照相机模块的首选方法是实现模块固件中的大部分功能，即通过 Microsoft OS 描述符。

通过 MSO 描述符（也称为 BOS 描述符）发布人脸身份验证配置文件支持以下照相机：

- 仅 RGB 使用单独的 IR 相机在传感器组中使用的相机。
- 要在具有单独的 RGB 相机的传感器组中使用的 IR 仅限相机。
- 带有单独 IR 和 RGB pin 的 RGB + IR 相机。

> **注意：** 如果照相机固件无法满足上述三个要求之一，则 ODM/OEM 必须使用扩展 INF 声明照相机配置文件 V2。

### <a name="example-microsoft-os-descriptor-layout"></a>Microsoft OS 描述符布局示例

下面的示例包含以下规范：

- Microsoft OS 扩展描述符规范1。0
- Microsoft 操作系统2.0 描述符规范

### <a name="microsoft-os-extended-descriptor-10-specification"></a>Microsoft OS 扩展描述符1.0 规范

扩展属性 OS 描述符包含两个组件

- 固定长度标头部分
- 标头部分后面的一个或多个可变长度自定义属性部分

#### <a name="microsoft-os-10-descriptor-header-section"></a>Microsoft 操作系统1.0 描述符标头部分

标头部分描述单个自定义属性（人脸身份验证配置文件）。

| 偏移 | 字段      | 大小(字节) | 值  | 说明                     |
| ------ | ---------- | ------------ | ------ | ------------------------------- |
| 0      | dwLength   | 4            | \<\>   |                                 |
| 4      | bcdVersion | 2            | 0x0100 | 版本 1.0                     |
| 6      | WIndex     | 2            | 0x0005 | 扩展属性 OS 描述符 |
| 8      | wCount     | 2            | 0x0001 | 一个自定义属性             |

#### <a name="microsoft-os-10-descriptor-custom-property-section"></a>Microsoft OS 1.0 描述符自定义属性部分

| 偏移 | 字段                | 大小(字节) | 值                 | 说明                                |
| ------ | -------------------- | ------------ | --------------------- | ------------------------------------------ |
| 0      | dwSize               | 4            | 0x00000036 （54）       | 此属性的总大小（以字节为单位）。   |
| 4      | dwPropertyDataType   | 4            | 0x00000004            | REG\_DWORD\_极少\_ENDIAN                 |
| 8      | wPropertyNameLength  | 2            | 0x00000024 （36）       | 属性名称的大小（以字节为单位）。      |
| 10     | bPropertyName        | 36           | UVC-CPV2FaceAuth      | Unicode 中的 "UVC-CPV2FaceAuth" 字符串。      |
| 46     | dwPropertyDataLength | 4            | 0x00000004            | 对于属性数据（sizeof （DWORD）），4个字节。 |
| 50     | bPropertyData        | 4            | 请参阅下面的数据架构 | 请参阅下面的数据架构。                     |

##### <a name="payload-schema"></a>负载架构

UVC-CPV2FaceAuth 数据负载为32位无符号整数。 高阶16位表示由 RGB pin 公开的媒体类型列表的索引（从0开始）。 低序位16位表示由 IR pin 公开的媒体类型列表的索引（从0开始）。

例如，按从 RGB pin 声明的顺序公开以下媒体类型的类型3照相机：

- YUY2、640x480@30fps
- MJPG、1280x720@30fps
- MJPG、800x600@30fps
- MJPG、1920x1080@30fps

对于 IR：

- L8，480x480@30fps
- L8，480x480@15fps
- L8，480x480@10fps

负载值为0x00010000 将导致发布以下面部身份验证配置文件：

Pin0：（RES = = 1280，720;FRT = = 30，1;SUT = = MJPG）//第二种媒体类型（0x0001）  
Pin1：（RES = = 480480;FRT = = 30，1;SUT = = L8）//第一种媒体类型（0x0000）

> **注意**：编写本文时，Windows HELLO 对 RGB 流和 IR 流的 340x340@15fps 的 480x480@7.5fps 要求最低。 启用面部身份验证配置文件时，需要将 IHV/Oem 选为满足此要求的媒体类型。

##### <a name="type-1-camera-sample"></a>键入1相机示例

对于类型1相机，由于没有 IR pin （假定类型1相机将与传感器组中计算机上的类型2照相机配对），只会发布 RGB 媒体类型索引。 对于 IR 媒体类型索引，有效负载的低序位16位值必须设置为0xFFFF。

例如，如果类型1相机公开以下媒体类型列表：

- YUY2、640x480@30fps
- MJPG、1280x720@30fps
- MJPG、800x600@30fps
- MJPG、1920x1080@30fps

若要使用 MJPG、1280x720@30fps 媒体类型发布 CPV2FaceAuth，必须将负载设置为0x0001FFFF。

##### <a name="type-2-camera-sample"></a>类型2相机示例

对于类型2相机，高序位16位必须设置为0xFFFF，低序位16位指示要使用的 IR 媒体类型。

例如，对于具有以下介质类型的类型2相机：

- L8，480x480@30fps
- L8，480x480@15fps
- L8，480x480@10fps

如果第一种媒体类型用于面部身份验证，则该值必须是：0xFFFF0000。

### <a name="microsoft-os-extended-descriptor-20-specification"></a>Microsoft OS 扩展描述符2.0 规范

MSO 扩展描述符2.0 可用于定义注册表值，以添加人脸身份验证配置文件支持。 这是使用[MICROSOFT OS 2.0 注册表属性描述符](#microsoft-os-20-registry-property-descriptor)实现的。

对于 UVC CPV2FaceAuth 注册表项，以下示例显示了一个示例 MSO 2.0 描述符集：

```cpp
UCHAR Example2_MSOS20DescriptorSet_UVCFaceAuthForFutureWindows[0x3C] =
{
    //
    // Microsoft OS 2.0 Descriptor Set Header
    //
    0x0A, 0x00,               // wLength - 10 bytes
    0x00, 0x00,               // MSOS20_SET_HEADER_DESCRIPTOR
    0x00, 0x00, 0x0?, 0x06,   // dwWindowsVersion – 0x060?0000 for future Windows version
    0x3C, 0x00,               // wTotalLength – 60 bytes

    //
    // Microsoft OS 2.0 Registry Value Feature Descriptor
    //
    0x32, 0x00,               // wLength - 50 bytes
    0x04, 0x00,               // wDescriptorType – 4 for Registry Property
    0x04, 0x00,               // wPropertyDataType - 4 for REG_DWORD_LITTLE_ENDIAN
    0x30, 0x00,               // wPropertyNameLength – 36 bytes
    0x55, 0x00, 0x56, 0x00,   // Property Name - "UVC-CPV2FaceAuth"
    0x43, 0x00, 0x2D, 0x00,
    0x43, 0x00, 0x50, 0x00,
    0x56, 0x00, 0x32, 0x00,
    0x46, 0x00, 0x61, 0x00,
    0x63, 0x00, 0x65, 0x00,
    0x41, 0x00, 0x75, 0x00,
    0x74, 0x00, 0x68, 0x00,
    0x00, 0x00, 0x00, 0x00,
    0x04, 0x00,               // wPropertyDataLength – 4 bytes
    0x00, 0x00, 0x01, 0x00    // PropertyData – 0x00010000 (see Payload Schema)
}
```

添加 UVC-CPV2FaceAuth 注册表项时，设备无需按照本文档中所述发布 EnableDshowRedirection 注册表项： https://docs.microsoft.com/windows-hardware/drivers/stream/dshow-bridge-implementation-guidance-for-usb-video-class-devices。

但是，如果设备供应商必须支持较旧版本的 Windows 和/或需要在框架服务器中启用 MJPEG 解压缩，则必须添加 EnableDshowRedirection 注册表项。

### <a name="sensor-group-generation"></a>传感器组生成

当 Oem 使用类型1和类型2照相机来提供适用于 Windows Hello 支持的 RGB 和 IR 流时，Oem 必须将两个照相机声明为合成传感器组的一部分。

为此，可在每个照相机的设备接口属性下，通过在扩展 INF 中声明 FSSensorGroupId 和 FSSensorGroupName 标记。

但是，如果未提供扩展 INF，Odm 可能使用相同的 MSO 描述符发布 FSSensorGroupId 和 FSSensorGroupName 值。 收件箱 Windows 10 USB 视频类驱动程序将自动获取其负载名称为 "UVC" 的任何 MSO 描述符，并将标记迁移到设备接口属性存储中（删除 "UVC-" 前缀）。

这样一来，类型1和类型2照相机会发布以下内容，以使 OS 能够将相机合成为多设备传感器组，以便与 Windows Hello 一起使用：

> UVC-FSSensorGroupId  
> UVC-FSSensorGroupName

每个标记的有效负载必须是 Unicode 字符串。 UVC-FSSensorGroupId 负载必须是以下格式的 GUID 字符串：

> {XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX} 个。

在类型1和类型2相机之间，GUID 的值必须相同，并且必须将两个照相机添加到相同的物理机箱。 对于内置相机，物理机箱就是计算机本身。 对于外部照相机，必须将类型1和类型2相机模块内置于连接到计算机的同一物理设备中。

## <a name="custom-device-interface-categories-for-sensor-groups"></a>传感器组的自定义设备接口类别

从19H1 开始，Windows 提供了一个 IHV/OEM 指定的扩展机制，以允许将合成的传感器组发布到任何自定义或预定义的类别。 生成的传感器组由在自定义 INF 中提供传感器组 ID 密钥的 IHV/Oem 定义：

> FSSensorGroupId： {Custom GUID}  
> FSSensorGroupName：用于传感器组\> \<友好名称

除了 INF 中的两个 AddReg 条目，还为自定义类别定义了一个新的 AddReg 条目：

> FSSensorGroupCategoryList： {GUID};{GUID}; ...;GUID.EMPTY

使用分号（;) 来定义多个类别分隔的 GUID 列表。

声明匹配 FSSensorGroupId 的每个设备必须声明相同的 FSSensorGroupCategoryList。 如果列表不匹配，则将忽略所有列表，默认情况下，传感器组将发布到 KSCATEGORY\_传感器\_组，就像未定义任何自定义类别一样。

## <a name="camera-rotation"></a>相机旋转

查看[照相机设备方向](camera-device-orientation.md)

## <a name="uvc-control-cache"></a>UVC 控件缓存

请参阅[UVC 控件缓存](camera-device-uvc-control-cache.md)

## <a name="bos-and-ms-os-20-descriptor"></a>BOS 和 MS OS 2.0 描述符

UVC 兼容相机可以使用[MICROSOFT OS 2.0 描述符](https://docs.microsoft.com/previous-versions/dn385747(v=msdn.10))在其固件中指定平台功能 BOS 描述符中的 Windows 特定设备配置值。 请参阅有关 MS OS 2.0 描述符的文档，以了解如何指定有效的 BOS 描述符，以将设备配置传递到 OS。

### <a name="microsoft-os-20-descriptor-set-header"></a>Microsoft 操作系统2.0 描述符集标头

| 偏移 | 字段            | 大小(字节) | 说明                                                                  |
| ------ | ---------------- | ------------ | ---------------------------------------------------------------------------- |
| 0      | wLength          | 2            | 此标头的长度（以字节为单位）必须为10。                                  |
| 2      | wDescriptorType  | 2            | MSOS20\_设置\_标头\_描述符                                              |
| 4      | dwWindowsVersion | 4            | Windows 版本。                                                             |
| 8      | wTotalLength     | 2            | 整个 MS OS 2.0 描述符集的大小，包括此标头大小。 |

### <a name="microsoft-os-20-registry-property-descriptor"></a>Microsoft OS 2.0 注册表属性描述符

| 偏移 | 字段               | 大小(字节) | 说明                        |
| ------ | ------------------- | ------------ | ---------------------------------- |
| 0      | wLength             | 2            | 此描述符的长度（以字节为单位） |
| 2      | wDescriptorType     | 2            | MS\_OS\_20\_功能\_REG\_属性 |
| 4      | wPropertyDataType   | 2            | 0x04 （REG\_DWORD\_极少\_ENDIAN）  |
| 6      | wPropertyNameLength | 2            | 属性名称的长度。   |
| 8      | PropertyName        | 变量     | 注册表属性的名称。 |
| 8 + M    | wPropertyDataLength | 2            | 属性数据的长度。   |
| 10 + M   | PropertyData        | 变量     | 属性数据                      |

在固件中指定有效的 MS OS 2.0 描述符后，USB stack 会将配置值复制到下面显示的设备 HW 注册表项中：

```Registry
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Enum\USB\<Device ID>\<Instance ID>\Device Parameters
```

UVC 驱动程序从设备 HW 注册表项读取配置值，并相应地在操作系统上配置设备。 例如，如果固件使用配置值指定要注册为传感器相机的设备，则 UVC 驱动程序将仅在该类别下注册设备。

通过平台 BOS 描述符配置 UVC 设备是在 Windows 10 版本1703中启用的一种机制，可帮助 UVC 设备供应商配置设备，而无需在 Windows 操作系统上使用 INF 文件。

仍支持通过自定义 INF 配置 UVC 设备，并优先于基于 BOS 描述符的机制。 通过 INF 指定设备属性时，无需添加前缀 "UVC-"。 仅在通过 BOS 描述符指定的设备属性和每个接口实例特定的设备属性中需要此前缀。 如果设备需要用户模式插件（如 DMFT），则需要提供一个 INF 用于安装 DMFT。 不能使用固件来配置它。

## <a name="currently-supported-configuration-values-through-bos-descriptor"></a>当前通过 BOS 描述符支持的配置值

| 配置名称 | 类型 | 说明 |
| --- | --- | --- |
| SensorCameraMode                              | REG\_DWORD | 将照相机注册到特定类别下。  |
| UVC-FSSensorGroupID<br>UVC-FSSensorGroupName  | REG\_SZ    | 具有相同 UVC 的组照相机-FSSensorGroupID |
| UVC-EnableDependentStillPinCapture            | REG\_DWORD | 启用仍捕获方法2/3              |
| UVC-EnablePlatformDmft                        | REG\_DWORD | 启用平台 DMFT                         |

当 UVC 驱动程序看到带有前缀 "UVC-" 的注册表值时，它将用相同的值（没有前缀）填充设备的类别接口实例注册表项。 驱动程序将针对固件指定的任何变量（而不只是上面列出的变量）执行此操作。

```Registry
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\DeviceClasses\{e5323777-f976-4f5b-9b55-b94699c46e44}\<Device Symbolic Link>\Device Parameters
```

要使 OS 使用 BOS 平台设备功能和 MS OS 2.0 描述符，设备描述符必须指定要0x0210 或更高版本的 bcdUSB 版本。

## <a name="example-composite-device"></a>复合设备示例

本部分提供了一个包含两个照相机功能的示例复合设备的 BOS 描述符和 MS OS 2.0 描述符。 一个函数是 UVC 的彩色相机，第二个函数是 UVC IR 相机。

示例描述符如下所示：

1. 在 KSCATEGORY 下注册彩色相机功能\_视频\_摄像机
1. 将 IR 相机功能注册到 KSCATEGORY\_传感器\_相机
1. 启用彩色相机函数仍图像捕获
1. 将颜色和 IR 相机功能与组相关联

在设备枚举时，USB stack 将从设备中检索 BOS 描述符。 以下 BOS 描述符是特定于平台的设备功能。

```cpp
#include <usbspec.h>

const BYTE USBVideoBOSDescriptor[0x21] =
{
    /* BOS Descriptor */
    0x05,                       // Descriptor size
    USB_BOS_DESCRIPTOR_TYPE,    // Device descriptor type BOS
    0x21, 0x00,                 // Length 0x21 (33) this and all sub descriptors
    0x01,                       // Number of device capability descriptors

    /* Platform Device Capability Descriptor */
    0x1C,                                   // 28 bytes bLength
    USB_DEVICE_CAPABILITY_DESCRIPTOR_TYPE,  // Platform Descriptor type
    USB_DEVICE_CAPABILITY_PLATFORM,         // bDevCapabilityType PLATFORM
    0,                                      // bReserved
    0xDF, 0x60, 0xDD, 0xD8,                 // PlatformCapabilityUUID
    0x89, 0x45,                             // MS OS2.0 Descriptor
    0xC7, 0x4C,                             // D8DD60DF-4589-4CC7-9CD2-659D9E648A9F
    0x9C, 0xD2, 0x65, 0x9D, 0x9E, 0x64, 0x8A, 0x9F,
                                            // CapabilityData
    0x00, 0x00, 0x00, 0x0A,                 // dwWindowsVersion for Windows 10 and later
    0xC8, 0x02,                             // wLength 0x2C8 (712)
    0x01,                                   // bMS_VendorCode - any value. e.g. 0x01
    0x00                                    // bAltEnumCmd 0
};
```

BOS 平台功能描述符指定：

1. MS OS 2.0 描述符平台功能 GUID
1. 供应商控制代码 bMS\_VendorCode （此处设置为1。 它可以采用供应商首选的任何值）来检索 MS OS 2.0 描述符。
1. 此 BOS 描述符适用于 Windows 10 及更高版本的操作系统版本。

查看 BOS 描述符后，USB stack 将发出特定于供应商的控制请求来检索 MS OS 2.0 描述符。

用于检索 MS OS 2.0 供应商特定描述符的控制请求的格式：

| bmRequestType | BRequest            | wValue | WIndex | wLength | 数据                                   |
|---------------|---------------------|--------|--------|---------|----------------------------------------|
| 1100 0000B    | **bMS\_VendorCode** | 0x00   | 0x07   | 长度  | 返回的 MS OS 2.0 描述符集 blob |

_**bmRequestType**_

- 数据传输方向–设备到主机
- 类型-供应商
- 收件人-设备

_**bRequest**_

描述符集信息结构中返回的**bMS\_VendorCode**值。

_**wValue**_

设置为0x00。

_**wIndex**_

用于 MS\_OS\_20\_描述符\_索引的0x7。

_**wLength**_

MS OS 2.0 描述符集的长度，在 BOS 描述符中返回。 0x25C （604）。

设备应返回 MS OS 2.0 描述符，如 USBVideoMSOS20DescriptorSet 中所指定的。

USBVideoMSOS20DescriptorSet 描述了颜色和 IR 函数。 它指定以下 MS OS 2.0 描述符值：

1. 设置标头
1. 配置子集标头
1. 彩色相机函数子集标题
1. 传感器组 ID 的注册表值功能描述符
1. 传感器组名称的注册表值功能描述符
1. 用于启用静态映像捕获的注册表值功能描述符
1. 用于启用平台 DMFT 的注册表值功能描述符
1. IR 相机函数子集标题
1. 传感器组 ID 的注册表值功能描述符
1. 传感器组名称的注册表值功能描述符
1. 用于将照相机注册为传感器相机的注册表值功能描述符

该固件将具有供应商请求的处理程序，该处理程序将为本部分开头所述的虚部设备返回以下 MS OS 2.0 描述符。

```cpp
UCHAR USBVideoMSOS20DescriptorSet[0x2C8] =
{
    /* Microsoft OS 2.0 Descriptor Set Header */
    0x0A, 0x00,             // wLength of MSOS20_SET_HEADER_DESCRIPTOR
    0x00, 0x00,             // wDescriptorType == MSOS20_SET_HEADER_DESCRIPTOR
    0x00, 0x00, 0x00, 0x0A, // dwWindowsVersion – 0x10000000 for Windows 10
    0xC8, 0x02,             // wTotalLength - Total length 0x2C8 (712)

    /* Microsoft OS 2.0 Configuration Subset Header */
    0x08, 0x00,             // wLength of MSOS20_SUBSET_HEADER_CONFIGURATION
    0x01, 0x00,             // wDescriptorType == MSOS20_SUBSET_HEADER_CONFIGURATION
    0x00,                   // bConfigurationValue set to the first configuration
    0x00,                   // bReserved set to 0.
    0xBE, 0x02,             // wTotalLength - Total length 0x2BE (702)

    /****************Color Camera Function******************/

    /* Microsoft OS 2.0 Function Subset Header */
    0x08, 0x00,             // wLength of MSOS20_SUBSET_HEADER_FUNCTION
    0x02, 0x00,             // wDescriptorType == MSOS20_SUBSET_HEADER_FUNCTION
    0x00,                   // bFirstInterface field of the first IAD
    0x00,                   // bReserved set to 0.
    0x6E, 0x01,             // wSubsetLength - Length 0x16E (366)

    /****************Register the Color Camera in a sensor group******************/

    /* Microsoft OS 2.0 Registry Value Feature Descriptor */
    0x80, 0x00,             // wLength 0x80 (128) in bytes of this descriptor
    0x04, 0x00,             // wDescriptorType – MSOS20_FEATURE_REG_PROPERTY
    0x01, 0x00,             // wPropertyDataType - REG_SZ
    0x28, 0x00,             // wPropertyNameLength – 0x28 (40) bytes
    'U', 0x00, 'V', 0x00,   // Property Name - "UVC-FSSensorGroupID"
    'C', 0x00, '-', 0x00,
    'F', 0x00, 'S', 0x00,
    'S', 0x00, 'e', 0x00,
    'n', 0x00, 's', 0x00,
    'o', 0x00, 'r', 0x00,
    'G', 0x00, 'r', 0x00,
    'o', 0x00, 'u', 0x00,
    'p', 0x00, 'I', 0x00,
    'D', 0x00, 0x00, 0x00,
    0x4E, 0x00,             // wPropertyDataLength – 0x4E (78) bytes
                            // FSSensorGroupID GUID in string format:
                            // "{20C94C5C-F402-4F1F-B324-0C1CF0257870}"
    '{', 0x00, '2', 0x00,   // This is just an example GUID.
    '0', 0x00, 'C', 0x00,   // You need to generate and use your
    '9', 0x00, '4', 0x00,   // own GUID for the sensor group ID
    'C', 0x00, '5', 0x00,
    'C', 0x00, '-', 0x00,
    'F', 0x00, '4', 0x00,
    '0', 0x00, '2', 0x00,
    '-', 0x00, '4', 0x00,
    'F', 0x00, '1', 0x00,
    'F', 0x00, '-', 0x00,
    'B', 0x00, '3', 0x00,
    '2', 0x00, '4', 0x00,
    '-', 0x00, '0', 0x00,
    'C', 0x00, '1', 0x00,
    'C', 0x00, 'F', 0x00,
    '0', 0x00, '2', 0x00,
    '5', 0x00, '7', 0x00,
    '8', 0x00, '7', 0x00,
    '0', 0x00, '}', 0x00,
    0x00, 0x00,

    /* Microsoft OS 2.0 Registry Value Feature Descriptor */
    0x56, 0x00,             // wLength 0x56 (86) in bytes of this descriptor
    0x04, 0x00,             // wDescriptorType – MSOS20_FEATURE_REG_PROPERTY
    0x01, 0x00,             // wPropertyDataType - REG_SZ
    0x2C, 0x00,             // wPropertyNameLength – 0x2C (44) bytes
    'U', 0x00, 'V', 0x00,   // Property Name - "UVC-FSSensorGroupName"
    'C', 0x00, '-', 0x00,
    'F', 0x00, 'S', 0x00,
    'S', 0x00, 'e', 0x00,
    'n', 0x00, 's', 0x00,
    'o', 0x00, 'r', 0x00,
    'G', 0x00, 'r', 0x00,
    'o', 0x00, 'u', 0x00,
    'p', 0x00, 'N', 0x00,
    'a', 0x00, 'm', 0x00,
    'e', 0x00, 0x00, 0x00,
    0x20, 0x00,             // wPropertyDataLength – 0x20 (32) bytes
                            // FSSensorGroupName "YourCameraGroup"
    'Y', 0x00, 'o', 0x00,
    'u', 0x00, 'r', 0x00,
    'C', 0x00, 'a', 0x00,
    'm', 0x00, 'e', 0x00,
    'r', 0x00, 'a', 0x00,
    'G', 0x00, 'r', 0x00,
    'o', 0x00, 'u', 0x00,
    'p', 0x00, 0x00, 0x00,

    /****************Enable Still Image Capture for Color Camera************/

    /* Microsoft OS 2.0 Registry Value Feature Descriptor */
    0x54, 0x00,             // wLength 0x54 (84) in bytes of this descriptor
    0x04, 0x00,             // wDescriptorType – MSOS20_FEATURE_REG_PROPERTY
    0x04, 0x00,             // wPropertyDataType - REG_DWORD
    0x46, 0x00,             // wPropertyNameLength – 0x46 (70) bytes
    'U', 0x00, 'V', 0x00,   // Property Name - "UVC-EnableDependentStillPinCapture"
    'C', 0x00, '-', 0x00,
    'E', 0x00, 'n', 0x00,
    'a', 0x00, 'b', 0x00,
    'l', 0x00, 'e', 0x00,
    'D', 0x00, 'e', 0x00,
    'p', 0x00, 'e', 0x00,
    'n', 0x00, 'd', 0x00,
    'e', 0x00, 'n', 0x00,
    't', 0x00, 'S', 0x00,
    't', 0x00, 'i', 0x00,
    'l', 0x00, 'l', 0x00,
    'P', 0x00, 'i', 0x00,
    'n', 0x00, 'C', 0x00,
    'a', 0x00, 'p', 0x00,
    't', 0x00, 'u', 0x00,
    'r', 0x00, 'e', 0x00,
    0x00, 0x00,
    0x04, 0x00,              // wPropertyDataLength – 4 bytes
    0x01, 0x00, 0x00, 0x00,   // Enable still pin capture using Method 2 or Method 3

    /****************Enable Platform DMFT for ROI-capable USB Camera************/

    /* Microsoft OS 2.0 Registry Value Feature Descriptor */
    0x3C, 0x00,             // wLength 0x3C (60) in bytes of this descriptor
    0x04, 0x00,             // wDescriptorType – MSOS20_FEATURE_REG_PROPERTY
    0x04, 0x00,             // wPropertyDataType - REG_DWORD
    0x2E, 0x00,             // wPropertyNameLength – 0x2E (46) bytes
    'U', 0x00, 'V', 0x00,   // Property Name - "UVC-EnablePlatformDmft"
    'C', 0x00, '-', 0x00,
    'E', 0x00, 'n', 0x00,
    'a', 0x00, 'b', 0x00,
    'l', 0x00, 'e', 0x00,
    'P', 0x00, 'l', 0x00,
    'a', 0x00, 't', 0x00,
    'f', 0x00, 'o', 0x00,
    'r', 0x00, 'm', 0x00,
    'D', 0x00, 'm', 0x00,
    'f', 0x00, 't', 0x00,
    0x00, 0x00,
    0x04, 0x00,              // wPropertyDataLength – 4 bytes
    0x01, 0x00, 0x00, 0x00,  // Enable Platform DMFT

    /****************IR Camera Function*********************************************/

    /* Microsoft OS 2.0 Function Subset Header */
    0x08, 0x00,             // wLength of MSOS20_SUBSET_HEADER_FUNCTION
    0x02, 0x00,             // wDescriptorType == MSOS20_SUBSET_HEADER_FUNCTION
    0x01,                   // bFirstInterface set of the second function
    0x00,                   // bReserved set to 0.
    0x48, 0x01,             // wSubsetLength - Length 0x148 (328)

    /********Register the IR Camera to the same sensor group as the Color Camera*****/

    /* Microsoft OS 2.0 Registry Value Feature Descriptor */
    0x80, 0x00,             // wLength 0x80 (128) in bytes of this descriptor
    0x04, 0x00,             // wDescriptorType – MSOS20_FEATURE_REG_PROPERTY
    0x01, 0x00,             // wPropertyDataType - REG_SZ
    0x28, 0x00,             // wPropertyNameLength – 0x28 (40) bytes
    'U', 0x00, 'V', 0x00,   // Property Name - "UVC-FSSensorGroupID"
    'C', 0x00, '-', 0x00,
    'F', 0x00, 'S', 0x00,
    'S', 0x00, 'e', 0x00,
    'n', 0x00, 's', 0x00,
    'o', 0x00, 'r', 0x00,
    'G', 0x00, 'r', 0x00,
    'o', 0x00, 'u', 0x00,
    'p', 0x00, 'I', 0x00,
    'D', 0x00, 0x00, 0x00,
    0x4E, 0x00,             // wPropertyDataLength – 78 bytes
                            // FSSensorGroupID GUID in string format:
                            // "{20C94C5C-F402-4F1F-B324-0C1CF0257870}"
    '{', 0x00, '2', 0x00,
    '0', 0x00, 'C', 0x00,
    '9', 0x00, '4', 0x00,
    'C', 0x00, '5', 0x00,
    'C', 0x00, '-', 0x00,
    'F', 0x00, '4', 0x00,
    '0', 0x00, '2', 0x00,
    '-', 0x00, '4', 0x00,
    'F', 0x00, '1', 0x00,
    'F', 0x00, '-', 0x00,
    'B', 0x00, '3', 0x00,
    '2', 0x00, '4', 0x00,
    '-', 0x00, '0', 0x00,
    'C', 0x00, '1', 0x00,
    'C', 0x00, 'F', 0x00,
    '0', 0x00, '2', 0x00,
    '5', 0x00, '7', 0x00,
    '8', 0x00, '7', 0x00,
    '0', 0x00, '}', 0x00,
    0x00, 0x00,

    /* Microsoft OS 2.0 Registry Value Feature Descriptor */
    0x56, 0x00,             // wLength 0x56 (86) in bytes of this descriptor
    0x04, 0x00,             // wDescriptorType – MSOS20_FEATURE_REG_PROPERTY
    0x01, 0x00,             // wPropertyDataType - REG_SZ
    0x2C, 0x00,             // wPropertyNameLength – 0x2C (44) bytes
    'U', 0x00, 'V', 0x00,   // Property Name - "UVC-FSSensorGroupName"
    'C', 0x00, '-', 0x00,
    'F', 0x00, 'S', 0x00,
    'S', 0x00, 'e', 0x00,
    'n', 0x00, 's', 0x00,
    'o', 0x00, 'r', 0x00,
    'G', 0x00, 'r', 0x00,
    'o', 0x00, 'u', 0x00,
    'p', 0x00, 'N', 0x00,
    'a', 0x00, 'm', 0x00,
    'e', 0x00, 0x00, 0x00,
    0x20, 0x00,             // wPropertyDataLength – 32 bytes
                            // FSSensorGroupName "YourCameraGroup"
    'Y', 0x00, 'o', 0x00,
    'u', 0x00, 'r', 0x00,
    'C', 0x00, 'a', 0x00,
    'm', 0x00, 'e', 0x00,
    'r', 0x00, 'a', 0x00,
    'G', 0x00, 'r', 0x00,
    'o', 0x00, 'u', 0x00,
    'p', 0x00, 0x00, 0x00,

    /****************Make IR camera visible to applications*********************/

    /* Microsoft OS 2.0 Registry Value Feature Descriptor */
    0x30, 0x00,             // wLength 0x30 (48) in bytes of this descriptor
    0x04, 0x00,             // wDescriptorType – MSOS20_FEATURE_REG_PROPERTY
    0x04, 0x00,             // wPropertyDataType - REG_DWORD
    0x22, 0x00,             // wPropertyNameLength – 0x22 (34) bytes
    'S', 0x00, 'e', 0x00,
    'n', 0x00, 's', 0x00,
    'o', 0x00, 'r', 0x00,
    'C', 0x00, 'a', 0x00,
    'm', 0x00, 'e', 0x00,
    'r', 0x00, 'a', 0x00,
    'M', 0x00, 'o', 0x00,
    'd', 0x00, 'e', 0x00,
    0x00, 0x00,
    0x04, 0x00,              // wPropertyDataLength – 4 bytes
    0x01, 0x00, 0x00, 0x00, // This exposes the camera to OS as an IR only camera
                            // i.e. KSCATEGORY_SENSOR_CAMERA

    /* Microsoft OS 2.0 Registry Value Feature Descriptor */
    0x3A, 0x00,             // wLength 0x3A (58) in bytes of this descriptor
    0x04, 0x00,             // wDescriptorType – MSOS20_FEATURE_REG_PROPERTY
    0x04, 0x00,             // wPropertyDataType - REG_DWORD
    0x2C, 0x00,             // wPropertyNameLength – 0x2C (44) bytes
    'S', 0x00, 'k', 0x00,
    'i', 0x00, 'p', 0x00,
    'C', 0x00, 'a', 0x00,
    'm', 0x00, 'e', 0x00,
    'r', 0x00, 'a', 0x00,
    'E', 0x00, 'n', 0x00,
    'u', 0x00, 'm', 0x00,
    'e', 0x00, 'r', 0x00,
    'a', 0x00, 't', 0x00,
    'i', 0x00, 'o', 0x00,
    'n', 0x00, 0x00, 0x00,
    0x04, 0x00,             // wPropertyDataLength – 4 bytes
    0x01, 0x00, 0x00, 0x00  // This exposes the camera to applications looking for IR only cameras
};  
```
