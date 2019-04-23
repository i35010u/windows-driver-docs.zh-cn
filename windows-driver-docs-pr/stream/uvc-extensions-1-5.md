---
title: USB 视频类 1.5 规范的 Microsoft 扩展
description: 介绍新控件，以及执行标准的格式定义完善的框架元数据的功能使 USB 视频类 1.5 规范的 Microsoft 扩展。
ms.date: 04/03/2019
ms.localizationpriority: medium
ms.custom: rs5, 19H1
ms.openlocfilehash: 8a88e66f7f7d8fe90bd55bfdbc783b17c659a693
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59904021"
---
# <a name="microsoft-extensions-to-usb-video-class-15-specification"></a>USB 视频类 1.5 规范的 Microsoft 扩展

## <a name="1-overview"></a>1 概述

### <a name="11-summary"></a>1.1 摘要

Microsoft 扩展[USB 视频类规范](https://go.microsoft.com/fwlink/p/?linkid=2085170)启用新的控件，以及执行标准的格式定义完善的框架元数据的功能。

### <a name="12-architecture-decisions"></a>1.2 体系结构决策

USB 视频类 (UVC) 框架元数据支持将可供 ISOCH 和大容量终结点。 但是，对于大容量终结点元数据大小会限制为 240 字节 （因为的大容量终结点上的所有视频帧数据传输在单个视频帧数据包）。

UVC 元数据支持将仅可用于根据有效负载的帧。

将只能通过 Media Foundation (MF) 捕获管道 UVC 元数据支持。

UVC 元数据将参加。 需要元数据支持每个 IHV/OEM 必须启用此选项通过自定义的 INF 文件。

UVC 元数据将仅支持系统分配的内存。 将不支持 VRAM 或 DX 应用层协议。

## <a name="2-architectural-overview"></a>2 个体系结构概述

### <a name="21-description"></a>2.1 说明

#### <a name="221-capability-discovery-through-inf"></a>2.2.1 通过 INF 功能发现

##### <a name="2211-still-image-capture--method-2"></a>2.2.1.1 映像仍捕获 – 方法 2

某些现有 UVC 设备可能不支持方法 2 2.4.2.4 （仍映像捕获） 部分中所述的*UVC 1.5 类 specification.pdf* ，可以从以下网址下载[USB 视频类规范](https://go.microsoft.com/fwlink/p/?linkid=2085170)web 站点。

在 Windows 10，版本 1607年及更早版本，捕获管道未利用方法 2，即使设备播发为其每个 UVC 1.5 规格的支持。

在 Windows 10，版本 1703，利用此方法的设备的照相机的驱动程序，必须使用自定义的 INF 文件但自定义 INF 是所必需的给定的硬件，从而使方法 2 仍然映像捕获）。

注意：照相机的驱动程序可以基于 Windows USBVIDEO。SYS 也可以基于二进制的自定义驱动程序。

基于自定义 UVC 驱动程序或收件箱 UVC 驱动程序，自定义的 INF 文件应包含以下 AddReg 条目：

**EnableDependentStillPinCapture**:REG_DWORD:0x0 （禁用） 为 0x1 （启用）

当此项设置为已启用 (0x1) 时，捕获管道将利用方法 2 仍然映像捕获 （假设固件还播发指定 UVC 1.5 规范的支持方法 2）。

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
HKR,,EnableDependentStillPinCapture,0x00010001,0x00000001
```

#### <a name="222-extension-unit-controls"></a>2.2.2 扩展单元控件

Microsoft 的扩展**USB 视频类规范**有关启用新的控件是通过由 GUID MS_CAMERA_CONTROL_XU （称为 Microsoft XU） 标识的扩展单元。

```cpp
// {0F3F95DC-2632-4C4E-92C9-A04782F43BC8}
DEFINE_GUID(MS_CAMERA_CONTROL_XU,
    0xf3f95dc, 0x2632, 0x4c4e, 0x92, 0xc9, 0xa0, 0x47, 0x82, 0xf4, 0x3b, 0xc8);
```

由设备固件实现 Microsoft XU 容纳以下子节中定义的新控件。 以下请求定义适用于所有这些控件，除非重写的定义显式指定为该控件。 请参阅**UVC 1.5 类 specification.pdf** D3、 D4、 GET_INFO，等的定义。

GET_INFO 请求应报告没有自动更新和异步功能 （即 D3 和 D4 位应设置为 0） 的控件。

GET_LEN 请求应报告此控件的有效负载的最大长度 (**并将 wLength**)。

GET_RES 请求应报告的分辨率 （步长），以便**qwValue/dwValue**。 所有其他字段应设置为 0。

GET_MIN 请求应报告的最小支持的值**qwValue/dwValue**。 所有其他字段应设置为 0。

GET_MAX 请求应报告受支持的最大值**qwValue/dwValue**。 此外，所有受支持的标志应设置为 1 **bmControlFlags**。 所有其他字段应设置为 0。

GET_DEF 和 GET_CUR 请求应报告的默认值和当前设置的字段分别**qwValue/dwValue**并**bmControlFlags**。 所有其他字段应设置为 0。

设置所有字段后，如果主机发出 SET_CUR 请求。

下表将控件选择器为 Microsoft XU 映射到其各自的值和对应的位位置*bmControls*扩展单元描述符中的字段：

![扩展单元控件](images/uvc-1-15-01.png)

##### <a name="2221-cancelable-asynchronous-controls"></a>2.2.2.1 可取消的异步控件

通过利用自动更新功能在此处定义的可取消异步控件。

GET_INFO 请求应报告此类控件作为自动更新控件 (例如，D3 位应设置为 1)，但不能作为异步控件 (例如，位应设置为 0 的 D4)。

对于此类控件，可以发出 SET_CUR 请求以设置新值 (其中请求 SET_CUR(NORMAL) **bmOperationFlags:D0**位设置为 0) 或取消以前 SET_CUR(NORMAL) 请求 (SET_CUR(CANCEL) 其中请求**bmOperationFlags:D0**位设置为 1)。 立即收到的请求 （即使硬件不是配置或者聚合到请求的新设置），应由设备完成 SET_CUR 请求。 对于每个 SET_CUR(NORMAL) 请求，设备会生成时在应用新设置或 SET_CUR(CANCEL) 请求到达; 时引发此控件的相应控件更改中断到达此中断，直到 SET_CUR(NORMAL) 请求将被视为是正在进行中。 正在进行中 SET_CUR(NORMAL) 请求时，针对此特定控件的其他 SET_CUR(NORMAL) 请求应导致失败。 SET_CUR(CANCEL) 请求应始终成功。 如果没有任何要取消，然后设备只是没有任何影响。

控制更改中断负载应具有位**bmOperationFlags:D0**如果 SET_CUR(NORMAL) 指定将设置应用设置为 0 （即收敛发生），如果由于 SET_ 未应用设置设置为 1CUR(CANCEL) SET_CUR(NORMAL) 请求 （即收敛情况尚未发生） 后出现的请求。

##### <a name="2222-focus-control"></a>2.2.2.2 焦点控制

此控件允许主机软件指定照相机的焦点设置。 这是影响所有视频流式处理与视频控件接口关联的接口上的所有终结点的全局控件。

![焦点控制](images/uvc-1-15-02.png)

此控件应充当可取消的异步控件 （请参阅有关 GET_INFO 请求要求和功能行为的 SET_CUR 请求第 2.2.2.1 部分）。

GET_MAX 要求：此控件应公布支持 bits D0、 D1、 D2、 D8 和在 D18 **bmControlFlags**。

GET_DEF 要求：默认值为**bmControlFlags**应 D0 和 D18 设置为 1 并**dwValue**设置为 0。

对于 GET_CUR/SET_CUR 请求，以下限制适用于字段**bmControlFlags**:

- 在 D0、 D1 和 D8 位之间可以设置仅有一位;它们都不设置是有效太如果 D2 位设置。

- 在 D16、 D17、 D18、 D19 和 D20，可以设置仅有一位;要设置的其中任何一个太有效。

- D1 是与所有其他位当前定义 （D0、 D2、 D8、 D16、 D17、 D18、 D19 和 D20） 不兼容。

- D2 是与 D1 和 D8 不兼容。

如果未设置 D0 D2 与 D16、 D17、 D18、 D19 和 D20 不兼容。

##### <a name="2223-exposure-control"></a>2.2.2.3 曝光控制

此控件允许主机软件指定照相机的曝光度设置。 这是影响所有视频流式处理与视频控件接口关联的接口上的所有终结点的全局控件。

![公开控件](images/uvc-1-15-03.png)

GET_INFO 请求应报告此控件，为异步控件 (即 D4 位应设置为 1)，但不是作为一个自动更新控件 (即 D3 位应设置为 0)。

GET_MAX 要求：此控件应公布的位 D0、 D1 和 D2 中的支持**bmControlFlags**。

GET_DEF 要求：默认值为**bmControlFlags**应 D0 设置为 1 并**qwValue**设置为 0。

对于 GET_CUR/SET_CUR 请求，以下限制适用于字段**bmControlFlags**:

- 在 D0、 D1 和 D2 位之间应设置至少一位。

- D1 是与 D0 和 D2 不兼容。

##### <a name="2224-ev-compensation-control"></a>2.2.2.4 EV 补偿控件

此控件允许主机软件指定照相机的 EV 补偿设置。 这是影响所有视频流式处理与视频控件接口关联的接口上的所有终结点的全局控件。

![EV 补偿控件](images/uvc-1-15-04.png)

GET_INFO 请求应报告此控件，为异步控件 (即 D4 位应设置为 1)，但不是作为一个自动更新控件 (即 D3 位应设置为 0)。

GET_RES 请求应报告所有受支持的分辨率 （步长） 中设置相应的位**bmControlFlags**。 所有其他字段应设置为 0。

GET_MIN 和 GET_MAX 请求应报告的最小值和最大支持的值**dwValue**。 位 D4 （指示步长 1） 应是和中的设置仅位**bmControlFlags**。 所有其他字段应设置为 0。

GET_DEF，GET_CUR，SET_CUR 请求应遵守第 2.2.2.1 部分中的定义，但应具有一个和只能有一位 D0、 D1、 D2、 D3 和 D4 之间将位设置为字段**bmControlFlags**。 此外，GET_DEF 请求应有**dwValue**设置为 0。

##### <a name="2225-white-balance-control"></a>2.2.2.5 白平衡控件

此控件允许主机软件指定照相机的白平衡设置。 这是影响所有视频流式处理与视频控件接口关联的接口上的所有终结点的全局控件。

![白平衡控件](images/uvc-1-15-05.png)

GET_INFO 请求应报告此控件，为异步控件 (即 D4 位应设置为 1)，但不是作为一个自动更新控件 (即 D3 位应设置为 0)。

GET_RES，GET_MIN，GET_MAX 请求应遵守第 2.2.2.1 部分中的定义，但应有**dwValueFormat**设置为 1。

GET_MAX 要求：此控件应公布的位 D0、 D1 和 D2 中的支持**bmControlFlags**。

GET_DEF 要求：默认值为**bmControlFlags**应 D0 设置为 1 并**dwValueFormat 以及 dwValue**设置为 0。

对于 GET_CUR/SET_CUR 请求，以下限制适用于字段**bmControlFlags**:

- 在 D0、 D1 和 D2 位之间应设置至少一位。

- D1 是与 D0 和 D2 不兼容。

##### <a name="2226-iso-control"></a>2.2.2.6 ISO 控件

此控件允许主机软件摄像机上指定仍映像捕获的 ISO 电影速度设置。 此控件是仅适用于指定的视频/仍终结点 （这是与视频控件接口关联的所有视频流式处理接口上的所有视频/仍终结点的子集）。 如果使用了仍捕获方法 1，则应在视频的终结点上支持此控制。 如果使用方法 2 或仍捕获的方法 3，则应在仍处于终结点上支持此控制。

![ISO 控件](images/uvc-1-15-06.png)

GET_INFO 请求应报告此控件，为异步控件 (即 D4 位应设置为 1)，但不是作为一个自动更新控件 (即 D3 位应设置为 0)。

GET_RES、 GET_MIN、 GET_MAX、 GET_DEF，GET_CUR 请求应遵守第 2.2.2.1 部分中的定义。 此外，这些请求的输出应列出所有和仅终结点支持的任一 D0 （自动模式） 或 D52 （手动模式） 即如果能够 D0 或 D52 终结点，它获取列;否则，它不会不获取列。

##### <a name="2227-face-authentication-control"></a>2.2.2.7 人脸验证控件

此控件允许主机软件指定摄像机是否支持用于人脸身份验证的流式处理模式。 仅当照相机想要支持人脸身份验证，则应支持此控件。

此控件是仅适用于照相机，可以生成红外 (IR) 数据并且仅适用于指定的视频终结点 （这是与视频控件接口关联的所有视频流式处理接口上的所有视频终结点的子集）。

![人脸验证控件](images/uvc-1-15-07.png)

GET_RES 和 GET_MIN 请求应报告字段**bNumEntries**设置为 0，因此具有任何其他字段。

对于 GET_MAX 请求，有些设置为 1 上**bmControlFlags**字段指示，该终结点支持相应的模式。 GET_MAX 请求输出应列出所有和唯一终结点能够 D1 或 D2 （即如果终结点是能够 D1 或 D2，它获取列出; 否则为它不会不会获取列出)。 此外，应该不播发任何终结点，才能与 D1 和 D2。 如果终结点应以常规用途 （即在外部的人脸身份验证目的） 的方式工作，D0 应设置为 1。 对于该终结点 （除了 D1/D2)。

有关 GET_DEF / GET_CUR / SET_CUR 请求，有些设置为 1 表示，该终结点选择相应的模式。 在这些请求，一个和只能有一位 （在 D0、 D1 和 D2） 应设置为特定终结点。 如果终结点，则返回默认选择 （这是特定于实现的），GET_DEF 请求应能工作以常规用途的方式 （即在外部的人脸身份验证目的），则 D0 应在该终结点; 默认情况下设置为 1否则，要么 D1 或 D2 （但不是能同时） 应设置为 1 默认情况下。 GET_DEF / GET_CUR 请求输出应包含 GET_MAX 请求输出; 中列出的所有终结点的信息但是，SET_CUR 请求只能包含 GET_MAX 请求输出中列出的终结点的子集。

##### <a name="2228-camera-extrinsics-control"></a>2.2.2.8 照相机 Extrinsics 控件

此控件允许主机软件以获取照相机 extrinsics 数据与视频控件接口关联的视频流式处理接口上的终结点。 因此每个终结点中获取的数据将显示为属性 MFStreamExtension_CameraExtrinsics 上属性存储为相应的流 （使用 IMFDeviceTransform::GetOutputStreamAttributes 调用获取）。

![照相机 extrinsics 控件](images/uvc-1-15-08.png)

GET_RES、 GET_MIN、 GET_MAX，GET_CUR 请求应报告字段**bNumEntries**设置为 0，因此具有任何其他字段。

GET_DEF 请求应列出具有可用的 extrinsics 信息的所有终结点。

##### <a name="2229-camera-intrinsics-control"></a>2.2.2.9 内部函数的照相机控件

此控件使主机软件以获取与视频控件接口关联的视频流式处理接口上的终结点的照相机内部函数数据。 因此每个终结点中获取的数据将显示为属性 MFStreamExtension_PinholeCameraIntrinsics 上属性存储为相应的流 （使用 IMFDeviceTransform::GetOutputStreamAttributes 调用获取）。

![内部函数的照相机控件](images/uvc-1-15-09.png)

GET_RES、 GET_MIN、 GET_MAX，GET_CUR 请求应报告字段**bNumEntries**设置为 0，因此具有任何其他字段。

GET_DEF 请求应列出具有可用的内部函数信息的所有终结点。

##### <a name="22210-metadata-control"></a>2.2.2.10 元数据控件

此控件允许主机软件来查询和控制元数据生成的照相机。 这是影响所有视频流式处理与视频控件接口关联的接口上的所有终结点的全局控件。 此控件获取映射到[ **KSPROPERTY_CAMERACONTROL_EXTENDED_METADATA** ](ksproperty-cameracontrol-extended-metadata.md)照相机驱动程序。

![元数据控件](images/uvc-1-15-metadata-control.png)

如果固件支持 SET_CUR 请求，则执行以下操作：

- GET_MIN，GET_DEF 请求应报告字段 dwValue 设置为 0。
- GET_RES 请求应报告字段 dwValue GET_MAX 请求报告是相同的值。
- 收到 SET_CUR 请求时使用 dwValue 设置为 0，照相机应不会产生任何元数据。 DwValue 设置为相同的值，报告的 GET_MAX 请求与收到 SET_CUR 请求时，照相机可以生成元数据，且此类元数据的大小不能超过任何帧 dwValue。

如果固件不支持 SET_CUR 请求，执行以下操作：

- GET_MIN，GET_DEF 请求应报告字段 dwValue GET_MAX 请求报告是相同的值。
- GET_RES 请求应报告字段 dwValue 设置为 0。
- 照相机可以生成元数据，此类元数据的总大小不能超过任何帧的 dwValue-所报告的 GET_MAX 请求 – 时间 UsbVideoHeader 元数据负载的大小小于 1024 字节。  
- UsbVideoHeader 元数据有效负载是 sizeof(KSCAMERA_METADATA_ITEMHEADER) + sizeof(KSTREAM_UVC_METADATA) 或 24 个字节。
生成的元数据应符合 Microsoft 标准格式元数据部分 2.2.3 中所述。

##### <a name="22211-ir-torch-control"></a>2.2.2.11 IR Torch 控件

此控件提供了灵活的方式来报告到的它可以控制并提供能够对其进行控制的范围内的红外线 （ir) LED 硬件。  这是影响所有视频流式处理通过调整连接到摄像机 IR lamp 强大功能与视频控件接口关联的接口上的所有终结点的全局控件。 此控件获取映射到[ **KSPROPERTY_CAMERACONTROL_EXTENDED_IRTORCHMODE** ](ksproperty-cameracontrol-extended-irtorchmode.md)照相机驱动程序。

![IR Torch 控件](images/uvc-1-15-irtorch-control.png)

执行以下操作：

- GET_LEN 请求应报告值为 8。
- GET_INFO 请求应报告 3。  此值指示支持 GET_CUR 和 SET_CUR 的同步控件。
- GET_MIN 请求应报告字段 dwMode 设置为 0，dwValue 设置为一个值，该值最小电能。  功率级别为 0，则可能 OFF，但最小可操作的电源级别不需要是 0。
- GET_RES 请求应报告设置为 0 dwValue 组字段 dwMode 到的数字小于或等于 GET_MAX(dwValue) – GET_MIN(dwValue) 等该 GET_MAX(dwValue) – GET_MIN(dwValue) 是整除的值。  dwValue 可能不是零 (0)。
- GET_MAX 请求应报告字段 dwMode 与 D [0-2] 设置了位集能够识别此控件的功能。  dwMode 必须具有 D0 设置位，指示支持 OFF，则它必须具有至少一个其他位设置、 支持活动状态。  dwValue 必须设置为一个值，指示正常启动。
- GET_DEF 请求应报告字段 dwMode 设置为流式处理开始之前，系统应采用的默认模式。  dwMode 必须设置为 2 (ON) 或 4 （交替）。  dwValue 应设置为 FaceAuth 控件通常使用的电源级别。  dwValue 由制造商定义。
- GET_CUR 请求应报告字段 dwMode 设置为当前操作模式和 dwValue 设置为当前照明。
- 当收到 SET_CUR 请求时，IR Torch 将设置为使用请求的操作模式为 prorate 强度的照明。

必须发出 IR Torch [ **MF_CAPTURE_METADATA_FRAME_ILLUMINATION** ](standardized-extended-controls-.md)每个帧的属性。  它可以通过设备 MFT 或包括提供这**MetadataId_FrameIllumination**照相机中的元数据有效负载中的属性。  请参阅部分 2.2.3.4.4。  

此元数据的唯一用途是指示框架或不点亮。  这是不同的元数据所需[ **KSPROPERTY_CAMERACONTROL_EXTENDED_FACEAUTH_MODE** ](ksproperty-cameracontrol-extended-faceauth-mode.md) DDI 而**MSXU_FACE_AUTHENTICATION_CONTROL**部分中定义2.2.2.7。  

#### <a name="223-metadata"></a>2.2.3 元数据

对于标准格式的帧的元数据设计基于从 Windows 10 的 UVC 自定义元数据设计。 在 Windows 10 中，自定义元数据支持 UVC 的照相机的驱动程序使用自定义 INF (注意： 照相机驱动程序可以基于 Windows USBVIDEO。SYS，但自定义 INF 是必需的元数据通过给定的硬件）。 如果`MetadataBufferSizeInKB<PinIndex>`注册表项是否存在并且非零，然后输入该 pin 支持自定义元数据值指示用于元数据的缓冲区大小。 `<PinIndex>`字段指示视频 pin 索引 0 开始的索引。

在 Windows 10，版本 1703，照相机驱动程序，可以通过包括以下 AddReg 条目发出对 Microsoft 标准格式的元数据的支持：

`StandardFormatMetadata<PinIndex>`：REG_DWORD:0x0 (NotSupported) 为 0x1 （支持）

此注册表项将由 DevProxy 读取，并告知元数据的标准格式通过 KSSTREAM_METADATA_INFO 结构标志字段中设置标志 KSSTREAM_METADATA_INFO_FLAG_STANDARDFORMAT UVC 驱动程序。

##### <a name="2231-microsoft-standard-format-metadata"></a>2.2.3.1 Microsoft 标准格式的元数据

Microsoft 标准格式元数据是一个或多个实例的以下结构：

![标准格式的元数据](images/extension-standard-format-metadata.png)

```cpp
typedef struct tagKSCAMERA_METADATA_ITEMHEADER {
    ULONG MetadataId;
    ULONG Size; // Size of this header + metadata payload following
} KSCAMERA_METADATA_ITEMHEADER, *PKSCAMERA_METADATA_ITEMHEADER;
```

通过从包含明确定义的标识符，以及自定义的标识符的以下枚举定义的标识符来填充 MetadataId 字段 (标识符 > = MetadataId_Custom_Start)。

```cpp
typedef enum {
    MetadataId_Standard_Start = 1,
    MetadataId_PhotoConfirmation = MetadataId_Standard_Start,
    MetadataId_UsbVideoHeader,
    MetadataId_CaptureStats,
    MetadataId_CameraExtrinsics,
    MetadataId_CameraIntrinsics,
    MetadataId_FrameIllumination,
    MetadataId_Standard_End = MetadataId_FrameIllumination,
    MetadataId_Custom_Start = 0x80000000,
} KSCAMERA_MetadataId;
```

大小字段设置为 sizeof(KSCAMERA_METADATA_ITEMHEADER) + sizeof(Metadata Payload)。

##### <a name="2232-firmware-generated-standard-format-metadata-from-usb-video-frame-packets"></a>2.2.3.2 从 USB 视频帧数据包固件生成标准格式元数据

在基于帧视频通过 UVC 传输，视频帧是打包为一系列的数据包，但每个前面有 UVC 负载标头。 每个 UVC 负载标头是 USB 视频类驱动程序框架基于负载规范所定义：

**负载标头**

下面是基于帧格式的有效负载标头格式的说明。

![负载标头](images/uvc-1-15-10.png)

**HLE （标头长度） 字段**

标头长度字段以字节为单位指定的标头的长度。

**位字段标头字段**

*FID:框架标识符*

- 此位切换每个帧开始边界上，保持不变的帧的其余部分。

*EOF:帧的末尾*

- 此位指示视频帧的结束，并在最后一个视频样本属于一个帧中设置。 使用此位是一种优化以减少延迟时间以完成帧传输和是可选的。

*PTS:演示时间戳*

- 这位，当设置，则指示 PTS 字段是否存在。

*SCR:源时钟引用*

- 这位，当设置，则指示 SCR 字段是否存在。

*RES:保留。*

- 设置为 0。

*STI:静态图像*

- 这位，当设置，它标识为属于静止图像视频示例。

*ERR:位错误*

- 这位，当设置，则表示设备流式处理中的错误。

*EOH:标头的末尾*

- 这位，当设置，则指示 BFH 字段的末尾。

*PTS:演示时间戳，大小：4 个字节，值：数量*

- 存在时 BFH [0] 字段中设置了 PTS 位 PTS 字段。 请参阅部分 2.4.3.3"视频和仍映像有效负载标头"中*视频设备的 USB 设备类定义*规范。

*SCR:源时钟引用，大小：6 个字节，值：数量*

- 当 SCR 位设置 BFH [0] 字段中存在 SCR 字段。 请参阅部分 2.4.3.3*视频和仍映像有效负载标头*中*视频设备的 USB 设备类定义*规范。

现有 UVC 驱动程序中的 HLE 字段被固定到 2 个字节 (没有 PTS/SCR 存在) 或最多 12 个字节 (PTS/SCR 存在)。 但是，HLE 字段中，在的字节大小字段中，可能可以指定最多 255 个字节的标头数据。 如果这两个 PTS/SCR 存在，且大于 12 个字节 HLE isgreater，的下列负载标头的前 12 个字节作为标准元数据的特定于视频选取任何额外的数据帧时 INF 条目`StandardFormatMetadata<PinIndex>`设置。

标准格式生成的元数据 （固件） 帧被通过串联的视频帧数据包，表示该范围中找到的部分 blob。

![元数据帧数据包](images/extension-metadata-frame-packets.png)

##### <a name="2233-metadata-buffer-provided-to-user-mode-component"></a>2.2.3.3 元数据缓冲区提供给用户模式组件

提供给用户模式组件的元数据缓冲区将具有元数据项 （由 UVC 驱动程序生成） UVC 时间戳跟固件生成的元数据的项并按如下所示布局：

![元数据缓冲区](images/extension-metadata-buffer.png)

##### <a name="2234-metadata-format-for-standard-metadata-identifiers"></a>2.2.3.4 标准元数据标识符元数据格式

固件可以选择生成为标识符对应的元数据。 如果固件选择生成标识符对应的元数据，该标识符的元数据应在发出的固件的所有帧上显示。

###### <a name="22341-metadataidcapturestats"></a>2.2.3.4.1 MetadataId_CaptureStats

此标识符的元数据格式由以下结构定义：

```cpp
typedef struct tagKSCAMERA_METADATA_CAPTURESTATS {
    KSCAMERA_METADATA_ITEMHEADER Header;
    ULONG Flags;
    ULONG Reserved;
    ULONGLONG ExposureTime;
    ULONGLONG ExposureCompensationFlags;
    LONG ExposureCompensationValue;
    ULONG IsoSpeed;
    ULONG FocusState;
    ULONG LensPosition; // a.k.a Focus
    ULONG WhiteBalance;
    ULONG Flash;
    ULONG FlashPower;
    ULONG ZoomFactor;
    ULONGLONG SceneMode;
    ULONGLONG SensorFramerate;
} KSCAMERA_METADATA_CAPTURESTATS, *PKSCAMERA_METADATA_CAPTURESTATS;
```

**标志**字段指示该结构中的更高版本字段填写，并且具有有效的数据。 标志字段不应发生帧中的更改。 目前，定义以下标志：

```cpp
#define KSCAMERA_METADATA_CAPTURESTATS_FLAG_EXPOSURETIME            0x00000001
#define KSCAMERA_METADATA_CAPTURESTATS_FLAG_EXPOSURECOMPENSATION    0x00000002
#define KSCAMERA_METADATA_CAPTURESTATS_FLAG_ISOSPEED                0x00000004
#define KSCAMERA_METADATA_CAPTURESTATS_FLAG_FOCUSSTATE              0x00000008
#define KSCAMERA_METADATA_CAPTURESTATS_FLAG_LENSPOSITION            0x00000010
#define KSCAMERA_METADATA_CAPTURESTATS_FLAG_WHITEBALANCE            0x00000020
#define KSCAMERA_METADATA_CAPTURESTATS_FLAG_FLASH                   0x00000040
#define KSCAMERA_METADATA_CAPTURESTATS_FLAG_FLASHPOWER              0x00000080
#define KSCAMERA_METADATA_CAPTURESTATS_FLAG_ZOOMFACTOR              0x00000100
#define KSCAMERA_METADATA_CAPTURESTATS_FLAG_SCENEMODE               0x00000200
#define KSCAMERA_METADATA_CAPTURESTATS_FLAG_SENSORFRAMERATE         0x00000400
```

**保留**字段保留以供将来，应设置为 0。

**ExposureTime**字段包含的暴露时间，在 100ns，当捕获帧时应用于传感器。 这将显示为相应的 MF 示例 MF_CAPTURE_METADATA_EXPOSURE_TIME 属性。

**ExposureCompensationFlags**字段包含 EV 补偿步骤 （恰好一个 KSCAMERA_EXTENDEDPROP_EVCOMP_XXX 步操作应设置标志） 用于传达 EV 补偿值。 **ExposureCompensationValue**字段包含应用到传感器时捕获帧时的步骤的单位中的 EV 补偿值。 这些将显示为相应的 MF 示例 MF_CAPTURE_METADATA_EXPOSURE_COMPENSATION 属性。

**IsoSpeed**字段包含应用到传感器时捕获帧时的 ISO 速度值。 这是无单位。 这将显示为相应的 MF 示例 MF_CAPTURE_METADATA_ISO_SPEED 属性。

**FocusState**字段包含的当前焦点状态，这可能需要在枚举 KSCAMERA_EXTENDEDPROP_FOCUSSTATE 中定义的值之一。 这将显示为相应的 MF 示例 MF_CAPTURE_METADATA_FOCUSSTATE 属性。

**LensPosition**字段时捕获帧时，即无单位包含的逻辑可重用功能区位置。 这是可以从 KSPROPERTY_CAMERACONTROL_EXTENDED_FOCUS 查询 GET 调用中的相同值。 这将显示为相应的 MF 示例 MF_CAPTURE_METADATA_LENS_POSITION 属性。

**WhiteBalance**字段包含白平衡时捕获帧时，这是在 Kelvin 值应用到传感器。 这将显示为相应的 MF 示例 MF_CAPTURE_METADATA_WHITEBALANCE 属性。

**Flash**字段包含一个布尔值 1 表示关闭，捕获帧时，闪存和 0 含义 flash。 这将显示为相应的 MF 示例 MF_CAPTURE_METADATA_FLASH 属性。

**FlashPower**字段包含闪存的强大功能应用于捕获的帧，这是一个值的范围中的 [0，100]。 如果驱动程序不支持可调整 power flash，应省略此字段。 这将显示为相应的 MF 示例 MF_CAPTURE_METADATA_FLASH_POWER 属性。

**ZoomFactor**字段包含 Q16 格式应用于捕获的帧中的缩放值。 这将显示为相应的 MF 示例 MF_CAPTURE_METADATA_ZOOMFACTOR 属性。

**SceneMode**字段包含应用于捕获的帧，这是 64 位 KSCAMERA_EXTENDEDPROP_SCENEMODE_XXX 标志的场景模式。 这将显示为相应的 MF 示例 MF_CAPTURE_METADATA_SCENE_MODE 属性。

**SensorFramerate**字段包含测得的传感器读数率以赫兹时捕获帧时，其中包含在上部的 32 位的分子值和较低的 32 位中的分母值。 这将显示为相应的 MF 示例 MF_CAPTURE_METADATA_SENSORFRAMERATE 属性。

###### <a name="22342-metadataidcameraextrinsics"></a>2.2.3.4.2 MetadataId_CameraExtrinsics

此标识符的元数据格式包括标准 KSCAMERA_METADATA_ITEMHEADER 跟一个字节数组的有效负载。 应按有效负载[MFCameraExtrinsics](https://msdn.microsoft.com/library/windows/desktop/mt740392)结构后跟零个或多[MFCameraExtrinsic_CalibratedTransform](https://msdn.microsoft.com/library/windows/desktop/mt740393)结构。 有效负载必须是 8 字节对齐，所有未使用的字节数应会出现在有效负载的末尾，并设置为 0。

###### <a name="22343-metadataidcameraintrinsics"></a>2.2.3.4.3 MetadataId_CameraIntrinsics

此标识符的元数据格式包括标准 KSCAMERA_METADATA_ITEMHEADER 跟一个字节数组的有效负载。 应按有效负载[MFPinholeCameraIntrinsics](https://msdn.microsoft.com/library/windows/desktop/mt740396)结构。 有效负载必须是 8 字节对齐，所有未使用的字节数应会出现在有效负载的末尾，并设置为 0。

###### <a name="22344-metadataidframeillumination"></a>2.2.3.4.4 MetadataId_FrameIllumination

此标识符的元数据格式由以下结构定义：

```cpp
typedef struct tagKSCAMERA_METADATA_FRAMEILLUMINATION {
    KSCAMERA_METADATA_ITEMHEADER Header;
    ULONG Flags;
    ULONG Reserved;
} KSCAMERA_METADATA_FRAMEILLUMINATION, *PKSCAMERA_METADATA_FRAMEILLUMINATION;
```

**标志**字段指示有关捕获的帧的信息。 目前，定义以下标志：

```cpp
#define KSCAMERA_METADATA_FRAMEILLUMINATION_FLAG_ON 0x00000001
```

如果在捕获帧时当照明上时，该标志 KSCAMERA_METADATA_FRAMEILLUMINATION_FLAG_ON 应设置。 否则，不应设置此标志。

**保留**字段是保留供将来使用，应设置为 0。
