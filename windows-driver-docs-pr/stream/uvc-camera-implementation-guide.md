---
title: Windows 10 UVC 相机实施指南
description: 概述了如何公开 USB 视频类符合照相机传送到收件箱驱动程序通过应用程序某些功能。
ms.date: 11/15/2018
ms.localizationpriority: medium
ms.openlocfilehash: 7e550bd9332abb197b4857b29e1ddd399ec4985d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547217"
---
# <a name="windows-10-uvc-camera-implementation-guide"></a>Windows 10 UVC 相机实施指南

Windows 10 设备符合 USB 视频类规范 （版本 1.0 到 1.5） 提供的收件箱 USB 视频类 (UVC) 驱动程序。 此驱动程序支持颜色和传感器类型照相机。 本文档概述了如何公开 UVC 符合照相机传送到收件箱驱动程序通过应用程序某些功能。

## <a name="terminology"></a>术语

| 关键字              | 描述                                                                  |
|----------------------|------------------------------------------------------------------------------|
| UVC                  | USB 视频类                                                              |
| UVC 驱动程序           | 附带了操作系统的 USBVideo.sys 驱动程序                                   |
| IR                   | 红外线                                                                     |
| 颜色照相机         | 照相机输出颜色流 （例如，RGB 或 YUV 照相机）      |
| 传感器照相机        | 照相机输出非颜色流 （例如，红外线 （ir） 或深度照相机） |
| BOS                  | 二进制对象存储设备                                                   |
| MS 操作系统 2.0 描述符 | Microsoft 平台特定 BOS 设备功能描述符                 |

## <a name="sensor-cameras"></a>传感器照相机

Windows 支持两种类别的照相机。 一个颜色照相机，另一个是一种非颜色传感器照相机。 RGB 或 YUV 照相机归类为颜色照相机和非颜色相机灰度等，红外线 （ir） 和深度照相机归类为传感器照相机。 UVC 驱动程序支持这两种类型的照相机。 我们建议照相机固件指定一个值，基于 UVC 驱动程序将在其上注册一个帐户下的照相机或支持这两种类别。

照相机支持颜色唯一的格式类型应注册下 KSCATEGORY\_视频\_照相机。 支持红外线 （ir） 的照相机或仅限深度的格式类型应注册下 KSCATEGORY\_传感器\_照相机。 照相机支持颜色和非颜色格式类型应注册下 KSCATEGORY\_视频\_照相机和 KSCATEGORY\_传感器\_照相机。 这种分类可帮助应用程序可以选择他们想要使用的照相机。

UVC 照相机可以指定通过属性，其类别首**SensorCameraMode**和**SkipCameraEnumeration**，在其 BOS [MS 操作系统 2.0 描述符](https://docs.microsoft.com/windows-hardware/drivers/usbcon/microsoft-defined-usb-descriptors)中的详细说明以下各节。

该属性**SensorCameraMode**采用值 1 或 2。

值为 1，将注册该设备下 KSCATEGORY\_传感器\_照相机。 除了此指定为 1 的值**SkipCameraEnumeration**以使照相机可用于应用程序只寻找传感器照相机。 公开仅传感器照相机媒体类型的照相机应使用此值。

值为 2， **SensorCameraMode**，将注册的设备在 KSCATEGORY\_传感器\_照相机和 KSCATEGORY\_视频\_照相机。 这将使照相机适用于应用程序寻找传感器和颜色照相机。 公开这两个传感器照相机和颜色照相机媒体类型的照相机应使用此值。

我们建议指定使用 BOS 描述符的上面提到的注册表值。 请参阅[示例复合设备](#example-composite-device)节具有平台特定 MS OS 2.0 描述符的示例 BOS 描述符。

如果按上文所述，无法更新设备固件，可以使用自定义 INF 并指定您的照相机需要通过指定的值注册为传感器照相机**SensorCameraMode**和**SkipCameraEnumeration** ，如下所示：

自定义的 INF 文件 （基于收件箱 UVC 驱动程序） 必须包含以下 AddReg 条目：

**SensorCameraMode**:REG\_DWORD:1 （若要注册为传感器照相机）

**SkipCameraEnumeration**:REG\_DWORD:1 （使其仅可用于红外线 （ir） 应用程序）

自定义的 INF 部分的示例如下所示：

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

如果**SensorCameraMode**并**SkipCameraEnumeration**固件或 INF 中未指定属性，照相机将注册为一个彩色相机并将仅对颜色照相机注意可见应用程序。

## <a name="ir-stream"></a>红外线 （ir） 流

Windows 收件箱 USB 视频类 (UVC) 驱动程序支持捕获 YUV 格式中的场景，并通过 USB 作为未压缩的 YUV 或压缩 MJPEG 帧传输此像素数据的照相机。

应在流视频格式描述符中，指定以下格式类型的 Guid，WDK ksmedia.h 标头文件中定义：

| 在任务栏的搜索框中键入 | 描述 |
| --- | --- |
| KSDATAFORMAT\_子类型\_L8\_红外线 （IR) |  未压缩 8 位亮度平面。 此类型映射到[MFVideoFormat\_L8](https://docs.microsoft.com/windows/desktop/medfound/video-subtype-guids#luminance-and-depth-formats)。 |
| KSDATAFORMAT\_SUBTYPE\_L16\_IR | 未压缩的 16 位亮度平面。 此类型映射到[MFVideoFormat\_L16](https://docs.microsoft.com/windows/desktop/medfound/video-subtype-guids#luminance-and-depth-formats)。 |
| KSDATAFORMAT\_SUBTYPE\_MJPG\_IR | 压缩的 MJPEG 帧数。 Media Foundation 这转换为未压缩的 NV12 帧，并使用仅亮度平面。 |

如果帧描述符 guidFormat 字段中指定了这些格式类型的 Guid，Media Foundation 捕获管道会将流标记为红外线 （ir） 流。 使用 Media Foundation FrameReader API 编写应用程序将无法使用红外线 （ir） 流。 不缩放或转换的红外线 （ir） 帧支持通过红外线 （ir） 流的管道。

流公开红外线 （ir） 格式的类型必须公开 RGB 或深度格式类型。

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
> 红外线 （ir） 流将显示为 DShow 中的正则捕获流。

## <a name="depth-stream"></a>深度流

Windows 收件箱 USB 视频类驱动程序支持生成深度流的摄像头。 这些相机捕获场景的深度信息 （例如，航班时间），并通过 USB 为未压缩的 YUV 帧传输深度映射。 应在流视频格式描述符中，指定以下格式类型 GUID，WDK ksmedia.h 标头文件中定义：

| 在任务栏的搜索框中键入 | 描述 |
| --- | --- |
| KSDATAFORMAT\_SUBTYPE\_D16 |  16 位深度的值映射。 此类型等同于[MFVideoFormat\_D16](https://docs.microsoft.com/windows/desktop/medfound/video-subtype-guids#luminance-and-depth-formats)。 值是以毫米为单位。 |

当帧描述符 guidFormat 成员中指定 GUID 的格式类型时，Media Foundation 捕获管道会将流标记为深度流。 使用 FrameReader API 编写的应用程序将无法使用深度流。 不缩放或转换的深度帧受深度流的管道。

流提供深度格式类型必须公开 RGB 或红外线 （ir） 格式类型。

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
> 深度流显示为 DShow 中的正则捕获流。

## <a name="grouping-cameras"></a>对相机进行分组

Windows 支持基于其容器 ID，以帮助应用程序的工作相关的照相机的相机的分组。 例如，IR 照相机和颜色照相机存在于同一个物理设备上可以公开到 OS 为相关的照相机。 这将使等 Windows Hello 应用程序以使其方案相关的相机的使用。

无法在固件中的照相机的 BOS 描述符中指定照相机函数之间的关系。 UVC 驱动程序将此信息的使用和公开这些相关的照相机函数。 这将使操作系统照相机堆栈公开其作为一组相关的应用程序的照相机。

必须指定照相机固件*UVC FSSensorGroupID*，这是与大括号的字符串形式的 GUID。 具有相同照相机*UVC FSSensorGroupID*将组合在一起。

传感器组可以通过指定给定名称*UVC FSSensorGroupName*，Unicode 字符串，在固件中的。

请参阅示例复合设备下面的部分，用于演示的示例指定 BOS *UVC FSSensorGroupID*并*UVC FSSensorGroupName*。

如果您不能更新设备固件，上文所述，可以使用自定义 INF 和指定您的相机通过传感器组 ID 指定为传感器组的一部分并命名，如下所示。 自定义的 INF 文件 （基于收件箱 UVC 驱动程序） 必须包含以下 AddReg 条目：

**FSSensorGroupID**:REG_SZ:"{您的传感器 group ID GUID}"

**FSSensorGroupName**:REG_SZ:"您传感器组的友好名称"

自定义的 INF 部分的示例将如下所示：

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
> 在 DShow 捕获管道中不支持传感器组。

## <a name="method-2-or-method-3-still-capture-support"></a>方法 2 或 3 方法仍然捕获支持

UVC 规范提供一种机制来指定是否视频流式处理接口支持方法 1/2/3 仍类型捕获映像。 若要使 OS 充分利用设备的方法 2/3 静止图像捕获支持功能，通过 UVC 驱动程序，设备固件可能 BOS 描述符中指定的值。

要指定以启用方法 2/3 静止图像捕获的值是名为 DWORD *UVC EnableDependentStillPinCapture*。 指定使用 BOS 描述符其值。 [示例复合设备](#example-composite-device)下面说明了启用仍与示例 BOS 描述符的映像捕获。

如果无法更新设备固件，如上文所述，可以使用自定义 INF 指定您的照相机支持方法 2 或 3 方法仍然捕获方法。

自定义的 INF 文件 （基于自定义 UVC 驱动程序或收件箱 UVC 驱动程序） 必须包含以下 AddReg 条目：

**EnableDependentStillPinCapture**:REG_DWORD:0x0 （禁用） 为 0x1 （启用）

当此项设置为已启用 (0x1) 时，捕获管道将利用方法 2/3 （假设固件还公布方法 2/3 UVC 规范由指定的支持） 仍然映像捕获。

自定义的 INF 部分示例如下所示：

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

设备 MFT 是 Ihv 和 Oem 来扩展在 Windows 上的相机功能的建议的用户模式下插件机制。 在 Windows 10，版本 1703 之前, 照相机管道支持只有一个 DMFT 扩展插件。 从 Windows 10，版本 1703，Windows 照相机管道支持最多包含三个 DMFTs DMFTs 的可选链。 这提供了更大的灵活性，oem 和 Ihv 提供增值的后期处理相机流的形式。 例如，设备可以使用以及 IHV DMFT 和 OEM DMFT PDMFT。 下图说明了涉及 DMFTs 链的体系结构。

![DMFT 链](images/dmft-chain.png)

捕获到 DevProxy，从相机驱动程序的示例流，然后通过 DMFT 链。 链中的每个 DMFT 有机会处理示例。 如果 DMFT 不想要处理的示例，它可以充当直通只需传递到下一步 DMFT 示例。

对于控件，如 KsProperty，调用将会增加流 – 链中的最后一个 DMFT 将获得第一个调用，调用可以在这里得到处理，或获取传递给链中的上一个 DMFT。

错误将从传播 DMFT 到 DTM 然后对应用程序。 IHV/OEM DMFTs DMFT 无法实例化的任何一个将 DTM 的致命错误。

DMFTs 的要求：

- DMFT 输入插针计数必须与上一 DMFT 输出 pin 数匹配，否则 DTM 会在初始化期间失败。 但是，同一 DMFT 的输入和输出插针计数不需要匹配。

- DMFT 需要支持接口-IMFDeviceTransform、 IMFShutdown、 IMFRealTimeClientEx、 IKsControl 和 IMFMediaEventGenerator;IMFTransform 可能需要 MFT0 配置是否支持或链中的下一步 DMFT 需要 IMFTransform 支持。

- 在 64 位系统上，请不要使用帧，32 位和 64 位 DMFTs 必须要注册的服务器。 考虑到可能获取 USB 照相机插入到任意系统，用于"external"（或非收件箱） USB 摄像机，USB 摄像机供应商应提供 32 位和 64 位 DMFTs。

## <a name="configuring-the-dmft-chain"></a>配置 DMFT 链

照相机设备可以根据需要提供 DMFT COM 对象使用自定义的 INF 文件所使用的收件箱 USBVideo.INF 部分的 DLL 中。

在自定义。AddReg INF 文件的"接口"部分中，通过添加以下注册表项指定 DMFT Clsid:

**CameraDeviceMftCLSIDChain** (REG\_多\_SZ) %dmft0。CLSID %、 %dmft。CLSID %、 %dmft2。CLSID %

示例 INF 以下设置 （将为 %dmft0 中所示。CLSID %和 %dmft1.clsid%使用实际的 CLSID 字符串要用于你 DMFTs)、 有 2 个 Clsid 中 Windows 10，版本 1703，允许的最大值和第一个参数是靠近 DevProxy 和最后一个是链中的最后一个 DMFT。

平台 DMFT CLSID 为 {3D096DDE-8971-4AD5-98F9-C74F56492630}。

一些示例**CameraDeviceMftCLSIDChain**设置：

- *没有 IHV/OEM DMFT 或平台 DMFT*

  - CameraDeviceMftCLSIDChain =""（或无需指定此注册表项）

- *IHV/OEM DMFT*

  - CameraDeviceMftCLSIDChain = %dmft。CLSID %

- *平台 DMFT &lt; - &gt; IHV/OEM DMFT*

  - CameraDeviceMftCLSIDChain = "{3D096DDE-8971-4AD5-98F9-C74F56492630}",%Dmft.CLSID%

  - 下面是使用平台 DMFT 和链中的 （使用 GUID {D671BE6C-FDB8-424F-81D7-03F5B1CE2CC7}) DMFT USB 摄像头的结果注册表项的屏幕截图。

![注册表编辑器 DMFT 链](images/dmft-registry-editor.png)

- *IHV/OEM DMFT0 &lt;-&gt; IHV/OEM DMFT1*

  - CameraDeviceMftCLSIDChain = %Dmft0.CLSID%,%Dmft1.CLSID%,

> [!NOTE]
> **CameraDeviceMftCLSIDChain**可以具有最多 2 个的 Clsid。

如果**CameraDeviceMftCLSIDChain**是配置，旧 CameraDeviceMftCLSID 设置将被跳过通过 DTM。

如果**CameraDeviceMftCLSIDChain**未配置，并且配置旧 CameraDeviceMftCLSID，则链将如下所示 (如果其 USB 摄像头和支持的平台 DMFT 并且启用平台 DMFT) DevProxy &lt;–&gt;平台 DMFT &lt;–&gt; OEM/IHV DMFT 或 （如果相机不受平台 DMFT 或禁用平台 DMFT） DevProxy &lt; - &gt; OEM/IHV DMFT。

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

从 Windows 10，版本 1703，开始 Windows 提供的收件箱设备 MFT 用于 UVC 相机作为平台 DMFT (PDMFT) 已知上选择的基础。 此 DMFT 允许 Ihv 和 Oem 以利用 Windows 提供 post 处理算法。

| 支持的平台 DMFT 功能 | Windows 版本 |
|-------------------------------------|-----------------|
| 使基于人脸的区域的感兴趣 (ROI) 中支持的投资回报率的 USB 摄像机 3A 调整。 | Windows 10 版本 1703 |

> [!NOTE]
> 如果相机不支持基于投资回报率，然后 PDMFT 将不会加载即使设备选择中使用 PDMFT UVC 1.5。

UVC 照相机可以参加以通过指定通过 BOS 描述符 EnablePlatformDmft 使用平台 DMFT。

要指定以启用平台 DMFT 的值是按名称 DWORD *UVC EnablePlatformDmft*并指定使用 BOS 描述符其值。 [示例复合设备](#example-composite-device)以下部分说明了使用示例 BOS 描述符启用平台 DMFT。

如果无法更新设备固件上文所述，可以使用自定义的 INF 文件来为设备启用平台 DMFT。

自定义的 INF 文件 （基于自定义 UVC 驱动程序或收件箱 UVC 驱动程序） 必须包含以下 AddReg 条目：

**EnablePlatformDmft**:REG_DWORD:0x0 （禁用） 为 0x1 （启用）

当此项设置为已启用 (0x1) 时，则捕获管道将对设备使用收件箱平台 DMFT。 下面显示了此自定义的 INF 部分的示例：

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

在 Windows 10，版本 1703，如果设备选择中使用 PDMFT 然后 PDMFT 支持会启用所有功能 （基于设备功能）。 不支持粒度配置 PDMFT 功能。

## <a name="bos-and-ms-os-20-descriptor"></a>BOS 和 MS OS 2.0 描述符

UVC 符合照相机可以指定在其固件中的平台功能 BOS 描述符中的 Windows 特定的设备配置值。 有关，请参阅文档[MS OS 2.0 描述符](https://msdn.microsoft.com/library/windows/hardware/dn385747)若要了解如何指定一个有效的 BOS 描述符，它传达了对操作系统的设备配置。 当在固件中指定有效的 MS OS 2.0 描述符时，USB 堆栈将配置值复制到设备硬件注册表键下面显示：

```Registry
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Enum\USB\<Device ID>\<Instance ID>\Device Parameters
```

UVC 驱动程序从设备 HW 注册表项读取配置值并相应地在 OS 中配置该设备。 例如，如果固件指定设备要注册为使用配置值的传感器摄像机，UVC 驱动程序注册的类别下只是设备。

配置通过平台 BOS 描述符 UVC 设备是在 Windows 10，版本 1703 帮助 UVC 设备供应商来配置设备而无需在 Windows OS 上的 INF 文件中启用了一种机制。

配置通过自定义 INF UVC 设备仍受支持，将优先于 BOS 描述符基于机制。 指定通过 INF 的设备属性，而不需要添加前缀"UVC-"。 此前缀仅需用于通过 BOS 描述符指定的并且每个接口实例特定的设备属性。 如果你的设备需要如 DMFT 用户模式下的插件，然后您需要安装 DMFT 提供 INF。 不能使用固件配置它。

## <a name="currently-supported-configuration-values-through-bos-descriptor"></a>当前支持的配置值通过 BOS 描述符

| 配置名称 | 在任务栏的搜索框中键入 | 描述 |
| --- | --- | --- |
| SensorCameraMode                              | REG\_DWORD | 注册特定类别下的照相机。  |
| UVC-FSSensorGroupID<br>UVC-FSSensorGroupName  | REG\_SZ    | 使用相同的 UVC FSSensorGroupID 组照相机 |
| UVC-EnableDependentStillPinCapture            | REG\_DWORD | 若要启用仍捕获方法 2/3              |
| UVC-EnablePlatformDmft                        | REG\_DWORD | 若要启用平台 DMFT                         |

当 UVC 驱动程序发现具有前缀"UVC-"的注册表值时，它将填充设备的类别接口实例注册表项，使用不带前缀相同的值。 该驱动程序将执行此操作指定固件的任何变量，而不仅仅是上面所列。

```Registry
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\DeviceClasses\{e5323777-f976-4f5b-9b55-b94699c46e44}\<Device Symbolic Link>\Device Parameters
```

对于操作系统，使利用 BOS 平台的设备功能和 MS OS 2.0 描述符，设备描述符必须指定要 0x0210 bcdUSB 版本或更高版本。

## <a name="example-composite-device"></a>示例复合设备

本部分提供有关两个相机功能的示例复合设备 BOS 描述符和 MS OS 2.0 描述符。 一个函数是 UVC 颜色照相机和第二个函数是一种 UVC IR 照相机。

示例描述符如下所示：

1. 注册颜色照相机函数下 KSCATEGORY\_视频\_照相机

1. 注册 IR 照相机函数下 KSCATEGORY\_传感器\_照相机

1. 启用颜色照相机函数静止图像捕获

1. 将作为一个组相关联的颜色和 IR 照相机函数

在设备枚举时 USB 堆栈从设备检索 BOS 描述符。 后面的 BOS 描述符是平台特定的设备功能。

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

指定 BOS 平台功能描述符：

1. MS OS 2.0 描述符平台功能的 GUID

1. 供应商控件代码 bMS\_VendorCode （此处是设置为 1。 它可以使用供应商更适合于创建任何值） 来检索 MS OS 2.0 描述符。

1. 此 BOS 描述符是适用于 OS 版本为 Windows 10 及更高版本。

将看到 BOS 描述符后, 发出 USB 堆栈供应商特定的控件请求来检索 MS OS 2.0 描述符。

控制请求检索 MS OS 2.0 供应商特定的描述符的格式：

| bmRequestType | bRequest            | wValue | wIndex | wLength | 数据                                   |
|---------------|---------------------|--------|--------|---------|----------------------------------------|
| 1100 0000B    | **bMS\_VendorCode** | 0x00   | 0x07   | 长度  | 返回的 MS OS 2.0 描述符设置 blob |

_**bmRequestType**_

- 数据传输方向 – 主机到设备

- 类型-供应商

- 接收方的设备

_**bRequest**_

**BMS\_VendorCode**描述符集信息结构中返回的值。

_**wValue**_

设置为 0x00。

_**wIndex**_

为 MS 0x7\_OS\_20\_描述符\_索引。

_**wLength**_

MS OS 2.0 描述符集，如 BOS 描述符中返回的长度。 在此示例中 0x25C (604)。

设备应返回类似于 USBVideoMSOS20DescriptorSet 中指定的 MS OS 2.0 描述符。

USBVideoMSOS20DescriptorSet 描述颜色和红外线 （ir） 函数。 它指定以下 MS 操作系统 2.0 描述符值：

1. 将标头设置

1. 配置子集标头

1. 颜色照相机函数子集标头

1. 传感器组 ID 的注册表值功能描述符

1. 传感器组名称的注册表值功能描述符

1. 仍然启用捕获映像的注册表值功能描述符

1. 启用平台 DMFT 的注册表值功能描述符

1. IR 照相机函数子集标头

1. 传感器组 ID 的注册表值功能描述符

1. 传感器组名称的注册表值功能描述符

1. 有关注册为传感器照相机的照相机的注册表值功能描述符

固件必须将返回虚部设备在此部分开头所述的以下 MS OS 2.0 描述符的供应商请求的处理程序。

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
