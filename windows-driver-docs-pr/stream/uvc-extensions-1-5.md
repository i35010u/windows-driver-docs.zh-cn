---
title: USB 视频类 1.5 规范的 Microsoft 扩展
description: 介绍适用于 USB 视频类1.5 规范的 Microsoft 扩展，这些扩展可实现新的控制，并能够以标准格式执行定义完善的帧元数据。
ms.date: 06/19/2020
ms.localizationpriority: medium
ms.custom: rs5, 19H1
ms.openlocfilehash: 4bc384ed2b4276e1b732b7a50dbe3ab8f08bdd7b
ms.sourcegitcommit: 17c1bbc5ea0bef3bbc87794b030a073f905dc942
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/25/2020
ms.locfileid: "88802441"
---
# <a name="microsoft-extensions-to-usb-video-class-15-specification"></a>USB 视频类 1.5 规范的 Microsoft 扩展

## <a name="1-overview"></a>1概述

### <a name="11-summary"></a>1.1 摘要

Microsoft 对 [USB 视频类规范](https://www.usb.org/document-library/video-class-v15-document-set) 的扩展可实现新的控制，并能够以标准格式使用定义完善的帧元数据。

### <a name="12-architecture-decisions"></a>1.2 体系结构决策

USB 视频类 (UVC) 帧元数据支持将可用于 ISOCH 和批量终结点。 但对于大容量终结点，元数据大小将限制为240字节 (因为这种情况下，所有视频帧数据都将在大容量终结点) 上以单个视频帧数据包传输。

UVC 元数据支持将仅适用于基于帧的负载。

UVC 元数据支持将只能通过媒体基础 (MF) 捕获管道提供。

UVC 元数据将选择加入。 需要元数据支持的每个 IHV/OEM 必须通过自定义 INF 文件启用此服务。

UVC 元数据仅支持系统分配的内存。 将不支持 VRAM 或 DX 表面。

## <a name="2-architectural-overview"></a>2体系结构概述

### <a name="21-description"></a>2.1 说明

#### <a name="221-capability-discovery-through-inf"></a>通过 INF 2.2.1 功能发现

##### <a name="2211-still-image-capture--method-2"></a>2.2.1.1 静止图像捕获–方法2

某些现有的 UVC 设备可能不支持*UVC 1.5 类 specification.pdf*的 2.4.2.4 (仍图像捕获) 部分中所述的方法2。 [USB Video Class specification](https://www.usb.org/document-library/video-class-v15-document-set)

在 Windows 10 版本1607及更早版本中，捕获管道未利用方法2，即使设备为每个 UVC 1.5 规范公布了该方法。

在 Windows 10 版本1703中，利用此方法的设备必须使用适用于照相机驱动程序的自定义 INF 文件，但对于给定硬件，需要使用自定义 INF 来启用方法2静态映像捕获) 。

注意：照相机驱动程序可以基于 Windows USBVIDEO.SYS，也可以基于自定义驱动程序二进制文件。

基于自定义 UVC 驱动程序或收件箱 UVC 驱动程序的自定义 INF 文件应包括以下 AddReg 条目：

**EnableDependentStillPinCapture**： REG_DWORD： 0X0 (禁用了) 到0x1 的 () 

如果此项设置为 "已启用 (0x1) ，则捕获管道会将方法2用于静态映像捕获 (假定固件还公布了 UVC 1.5 spec) 指定的方法2的支持。

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

#### <a name="222-extension-unit-controls"></a>2.2.2 扩展单元控件

用于启用新控件的 Microsoft **视频类规范** 的 "扩展" 是通过 GUID MS_CAMERA_CONTROL_XU (称为 XU) 的扩展单元来完成的。

```cpp
// {0F3F95DC-2632-4C4E-92C9-A04782F43BC8}
DEFINE_GUID(MS_CAMERA_CONTROL_XU,
    0xf3f95dc, 0x2632, 0x4c4e, 0x92, 0xc9, 0xa0, 0x47, 0x82, 0xf4, 0x3b, 0xc8);
```

设备固件实现的 XU 将承载以下子部分中定义的新控件。 以下请求定义适用于所有这些控件，除非为该控件显式指定了重写定义。 有关 D3、D4、GET_INFO 等的定义，请参阅 **UVC 1.5 类 specification.pdf** 。

GET_INFO 请求应报告不含自动更新和异步功能的控件 (例如，D3 和 D4 位应设置为 0) 。

GET_LEN 请求应报告此控件 (**wLength**) 的有效负载的最大长度。

GET_RES 请求应报告 **qwValue/dwValue**的步骤大小) 的分辨率 (。 所有其他字段应设置为0。

GET_MIN request 应报告 **qwValue/dwValue**支持的最小值。 所有其他字段应设置为0。

GET_MAX 请求应报告 **qwValue/dwValue**的最大支持值。 此外， **bmControlFlags**中的所有支持标志都应设置为1。 所有其他字段应设置为0。

GET_DEF 和 GET_CUR 请求应分别为 **qwValue/dwValue** 和 **bmControlFlags**字段报告默认设置和当前设置。 所有其他字段应设置为0。

设置所有字段后，主机会发出 SET_CUR 请求。

下表将 Microsoft XU 的控件选择器映射到其各自的值，并将 *bmControls* 字段的位位置映射到扩展单元描述符中：

![扩展单元控件](images/uvc-1-15-01.png)

##### <a name="2221-cancelable-asynchronous-controls"></a>第2.2.2.1 可取消异步控件

可取消的异步控件通过利用自动更新功能在此处定义。

GET_INFO 请求应将此类控件报告为自动更新控件 (例如，D3 位应设置为 1) 但不是异步控件 (例如，D4 位应设置为 0) 。

对于此类控制，可以发出 SET_CUR 请求以设置新值 (SET_CUR (正常) 请求，其中 **bmOperationFlags： D0** 位设置为 0) 或取消以前的 SET_CUR (普通) 请求 (SET_CUR (取消) 请求，其中 **bmOperationFlags： D0** 位设置为 1) 。 收到请求后，应立即由设备完成 SET_CUR 请求 (即使未将硬件配置或聚合到) 请求的新设置。 对于每个 SET_CUR (普通) 请求，在应用新设置时或当 SET_CUR (取消) 请求到达时，设备将为引发的控件生成相应的控件更改中断;在此中断到达之前，会将 SET_CUR (普通) 请求视为正在进行。 如果 SET_CUR (普通) 请求正在进行中，则此特定控件的其他 SET_CUR (常规) 请求应导致失败。 SET_CUR (取消) 请求应始终成功。 如果没有要取消的内容，则设备将不执行任何操作。

如果应用了 SET_CUR (普通) 指定的设置，则控制更改中断负载应将位 **bmOperationFlags** 设置为 0 (即发生了聚合) 并将设置为1（如果未应用这些设置的原因是 SET_CUR (常规) 请求 SET_CUR ()  (

##### <a name="2222-focus-control"></a>2.2.2.2 焦点控件

此控件允许主机软件指定照相机的焦点设置。 这是一个全局控件，该控件影响与视频控件接口相关联的所有视频流接口上的所有终结点。

![焦点控件](images/uvc-1-15-02.png)

此控件应作为可取消的异步控件 (参阅 GET_INFO 请求要求的节第2.2.2.1 和 SET_CUR 请求) 的功能行为。

GET_MAX 要求：此控件应播发对 **bmControlFlags**中的 bits D0、D1、D2、D8 和 D18 的支持。

GET_DEF 要求： **BmControlFlags** 的默认值应为 D0，D18 设置为1， **dwValue** 设置为0。

对于 GET_CUR/SET_CUR 请求，以下限制适用于字段 **bmControlFlags**：

- 在 D0、D1 和 D8 位之间，只能设置一个位;如果设置了 D2 位，则未设置的任何一个都是有效的。

- 在 D16、D17、D18、D19 和 D20 之间，只能设置一个位;它们均未设置为有效。

- D1 与当前定义的所有其他位不兼容 (D0、D2、D8、D16、D17、D18、D19 和 D20) 。

- D2 与 D1 和 D8 不兼容。

如果未设置 D0，则 D2 与 D16、D17、D18、D19 和 D20 不兼容。

##### <a name="2223-exposure-control"></a>2.2.2.3 公开控制

此控件允许主机软件指定相机的曝光设置。 这是一个全局控件，该控件影响与视频控件接口相关联的所有视频流接口上的所有终结点。

![公开控制](images/uvc-1-15-03.png)

GET_INFO 请求应将此控件报告为异步控件 (例如，D4 位应设置为 1) 但不应设置为自动更新控件 (例如，D3 位应设置为 0) 。

GET_MAX 要求：此控件应播发对 **bmControlFlags**中的 bits D0、D1 和 D2 的支持。

GET_DEF 要求： **BmControlFlags** 的默认值应设置为1， **qwValue** 设置为0。

对于 GET_CUR/SET_CUR 请求，以下限制适用于字段 **bmControlFlags**：

- 在 D0、D1 和 D2 位之间，应该至少设置一个位。

- D1 与 D0 和 D2 不兼容。

##### <a name="2224-ev-compensation-control"></a>2.2.2.4 EV 补偿控制

此控件允许主机软件指定相机的 EV 补偿设置。 这是一个全局控件，该控件影响与视频控件接口相关联的所有视频流接口上的所有终结点。

![EV 补偿控制](images/uvc-1-15-04.png)

GET_INFO 请求应将此控件报告为异步控件 (例如，D4 位应设置为 1) 但不应设置为自动更新控件 (例如，D3 位应设置为 0) 。

GET_RES 请求应通过在 **bmControlFlags**中设置相应的位来 (步骤大小) 报告所有支持的分辨率。 所有其他字段应设置为0。

GET_MIN 和 GET_MAX 请求应报告 **dwValue**支持的最小值和最大值。 位 D4 (表明步骤大小 1) 应为 **bmControlFlags**中设置的一个和唯一一个位。 所有其他字段应设置为0。

GET_DEF、GET_CUR、SET_CUR 请求应遵循第2.2.2.1 部分中的定义，但应在 D0、D1、D2、D3 和 D4 位之间为 field **bmControlFlags**设置一个且仅设置一个位。 此外，GET_DEF request 应将 **dwValue** 设置为0。

##### <a name="2225-white-balance-control"></a>2.2.2.5 白平衡控制

此控件允许主机软件指定相机的白平衡设置。 这是一个全局控件，该控件影响与视频控件接口相关联的所有视频流接口上的所有终结点。

![白平衡控制](images/uvc-1-15-05.png)

GET_INFO 请求应将此控件报告为异步控件 (例如，D4 位应设置为 1) 但不应设置为自动更新控件 (例如，D3 位应设置为 0) 。

GET_RES、GET_MIN GET_MAX 请求应遵循第2.2.2.1 部分中的定义，但应将 **dwValueFormat** 设置为1。

GET_MAX 要求：此控件应播发对 **bmControlFlags**中的 bits D0、D1 和 D2 的支持。

GET_DEF 要求： **BmControlFlags** 的默认值应设置为 "1" 和 "dwValueFormat"，并将 " **dwValue** " 设置为 "0"。

对于 GET_CUR/SET_CUR 请求，以下限制适用于字段 **bmControlFlags**：

- 在 D0、D1 和 D2 位之间，应该至少设置一个位。

- D1 与 D0 和 D2 不兼容。

##### <a name="2226-iso-control"></a>第2.2.2.6 部分 ISO 控制

此控件允许主机软件指定相机上静止图像捕获的 ISO 胶片速度设置。 此控件仅适用于指定的视频/静态终结点 (，这是与视频控制接口) 相关联的所有视频/仍终结点的子集。 如果使用方法1进行仍捕获，则视频终结点应支持此控件。 如果使用方法2或方法3进行仍捕获，则此控件应在静止终结点上受支持。

![ISO 控制](images/uvc-1-15-06.png)

GET_INFO 请求应将此控件报告为异步控件 (例如，D4 位应设置为 1) 但不应设置为自动更新控件 (例如，D3 位应设置为 0) 。

GET_RES、GET_MIN、GET_MAX、GET_DEF、GET_CUR 请求应遵循第2.2.2.1 部分中的定义。 此外，这些请求的输出应列出所有和仅支持 D0 (Auto 模式) 或 D52 (手动模式的终结点) 也就是说，如果终结点可以是 D0 或 D52，则会列出它;否则，它不会列出。

##### <a name="2227-face-authentication-control"></a>2.2.2.7 面部身份验证控制

此控件允许主机软件指定相机是否支持用于面部身份验证的流模式。 只有照相机希望支持人脸身份验证时，才应支持此控制。

此控件仅适用于可生成红外 (IR) 数据的照相机，并且仅适用于指定的视频终结点 (这是与视频控件接口) 关联的所有视频流接口上所有视频终结点的子集。

![人脸身份验证控件](images/uvc-1-15-07.png)

GET_RES 和 GET_MIN 请求应将报表字段 **bNumEntries** 设置为0，因此没有其他字段。

对于 GET_MAX 请求， **bmControlFlags** 字段上的位设置为1，表示该终结点支持相应的模式。 GET_MAX 请求输出应列出所有和仅支持 D1 或 D2 (的终结点，即，如果终结点可以是 D1 或 D2，则会列出;否则，它不) 列出。 此外，不应播发任何终结点以支持 D1 和 D2。 如果某个终结点应采用常规用途 (即，在人脸 authentication) 目的之外工作，则除了 D1/D2) 外，该终结点的 D0 应该设置为 1 (。

对于 GET_DEF/GET_CUR/SET_CUR 请求，将位设置为1，表示为该终结点选择了相应的模式。 在这些请求中，只应为特定的终结点设置一个且仅有一个位 (在 D0 之间，D1 & D2) 。 对于返回) 实现特定的默认选择 (的 GET_DEF 请求，如果某个终结点应以常规用途的方式工作 (即，不在人脸身份验证) 目的之外，则默认情况下，D0 应设置为 1;否则，默认情况下，D1 或 D2 (但不能同时设置为 1) 。 GET_DEF/GET_CUR 请求输出应包含 GET_MAX 请求输出中列出的所有终结点的信息;但是，SET_CUR 请求可能只包含 GET_MAX 请求输出中列出的终结点的子集。

##### <a name="2228-camera-extrinsics-control"></a>2.2.2.8 照相机 Extrinsics 控件

此控件允许主机软件获取与视频控件接口相关联的视频流接口上的终结点的照相机 extrinsics 数据。 因此，为每个终结点获取的数据将显示为使用 IMFDeviceTransform：： GetOutputStreamAttributes call) 获取的相应 (流的属性存储中的属性 MFStreamExtension_CameraExtrinsics。

![相机 extrinsics 控件](images/uvc-1-15-08.png)

GET_RES、GET_MIN、GET_MAX、GET_CUR 请求应将报表字段 **bNumEntries** 设置为0，因此没有其他字段。

GET_DEF 请求应列出具有可用的 extrinsics 信息的所有终结点。

##### <a name="2229-camera-intrinsics-control"></a>2.2.2.9 照相机内部函数控件

此控件允许主机软件获取与视频控件接口相关联的视频流接口上的终结点的照相机内部数据。 因此，为每个终结点获取的数据将显示为使用 IMFDeviceTransform：： GetOutputStreamAttributes call) 获取的相应 (流的属性存储中的属性 MFStreamExtension_PinholeCameraIntrinsics。

![照相机内部函数控件](images/uvc-1-15-09.png)

GET_RES、GET_MIN、GET_MAX、GET_CUR 请求应将报表字段 **bNumEntries** 设置为0，因此没有其他字段。

GET_DEF 请求应列出具有可用的内部函数的所有终结点。

##### <a name="22210-metadata-control"></a>2.2.2.10 元数据控件

此控件允许主机软件查询和控制照相机生成的元数据。 这是一个全局控件，该控件影响与视频控件接口相关联的所有视频流接口上的所有终结点。 此控件将被映射到相机驱动程序 [**KSPROPERTY_CAMERACONTROL_EXTENDED_METADATA**](ksproperty-cameracontrol-extended-metadata.md) 。

![元数据控件](images/uvc-1-15-metadata-control.png)

如果固件支持 SET_CUR 请求，以下内容适用：

- GET_MIN，GET_DEF 请求应将报表字段 dwValue 设置为0。
- GET_RES request 应报告字段 dwValue 与 GET_MAX 请求报告的值相同。
- 当 dwValue 设置为0时接收到 SET_CUR 请求时，照相机不会生成任何元数据。 如果收到的 SET_CUR 请求的 dwValue 设置为与 GET_MAX 请求报告的值相同，则照相机可以生成元数据，并且此类元数据的大小不能超过 dwValue 的任何帧。

如果固件不支持 SET_CUR 请求，以下内容适用：

- GET_MIN，GET_DEF 请求应报告字段 dwValue 与 GET_MAX 请求报告的值相同。
- GET_RES request 应将报表字段 dwValue 设置为0。
- 照相机可以生成元数据，此类元数据的总大小不能超过 dwValue GET_MAX 报告的-任何帧的 UsbVideoHeader 元数据负载的大小不能超过1024个字节。  
- UsbVideoHeader 元数据负载是 sizeof (KSCAMERA_METADATA_ITEMHEADER) + sizeof (KSTREAM_UVC_METADATA) 或24个字节。
生成的元数据应符合 Microsoft standard 格式的元数据，如2.2.3 部分中所述。

##### <a name="22211-ir-torch-control"></a>2.2.2.11 IR Torch 控件

此控件为 IR LED 硬件提供一种灵活的方法，以便报告可以对其进行控制的范围并提供对其进行控制的能力。  这是一个全局控件，它通过调整连接到照相机的 IR 灯泡的电源，影响与视频控制接口相关联的所有视频流式处理接口上的所有终结点。 此控件将被映射到相机驱动程序 [**KSPROPERTY_CAMERACONTROL_EXTENDED_IRTORCHMODE**](ksproperty-cameracontrol-extended-irtorchmode.md) 。

![IR Torch 控件](images/uvc-1-15-irtorch-control.png)

适用以下说明：

- GET_LEN request 应报告值8。
- GET_INFO request 应报告为3。  此值指示支持 GET_CUR 和 SET_CUR 的同步控件。
- GET_MIN request 应将报表字段 dwMode 设置为0，并将 dwValue 设置为一个值，该值指示最小电量。  电源级别0可能表示关闭，但最小操作电源级别不需要为0。
- GET_RES request 应将报表字段 dwMode 设置为0，dwValue 将设置为一个小于或等于 GET_MAX (dwValue) – GET_MIN () GET_MAX () GET_MIN dwValue (–) dwValue 可以均匀地除以该值。  dwValue 不能为零 (0) 。
- GET_MAX request 应为报表字段 dwMode 设置，并设置了位 D [0-2] 来标识此控件的功能。  dwMode 必须具有位 D0 集，指示支持 OFF，并且它必须至少具有一个其他位集，以支持活动状态。  必须将 dwValue 设置为指示正常电源的值。
- GET_DEF request 应将报表字段 dwMode 设置为系统在流式处理开始之前应处于的默认模式。  必须在) 或 4 (交替) 上将 dwMode 设置为 2 (。  dwValue 应设置为通常用于 FaceAuth 控件的电源级别。  dwValue 由制造商定义。
- GET_CUR request 应将报表字段 dwMode 设置为当前运行模式，将 dwValue 设置为当前照明。
- 接收到 SET_CUR 请求时，IR Torch 使用请求的操作模式将照明设置为按比例计算强度。

IR Torch 必须发出每个帧的 [**MF_CAPTURE_METADATA_FRAME_ILLUMINATION**](standardized-extended-controls-.md) 属性。  它可以通过设备 MFT 来提供此项，或通过将 **MetadataId_FrameIllumination** 特性包含在照相机的元数据负载中。  请参阅2.2.3.4.4 部分。  

此元数据的唯一用途是指示帧是否亮起。  这与 [**KSPROPERTY_CAMERACONTROL_EXTENDED_FACEAUTH_MODE**](ksproperty-cameracontrol-extended-faceauth-mode.md) DDI 和2.2.2.7 部分中定义的 **MSXU_FACE_AUTHENTICATION_CONTROL** 所需的元数据相同。  

#### <a name="223-metadata"></a>2.2.3 元数据

标准格式框架元数据的设计是基于 Windows 10 的 UVC 自定义元数据设计构建的。 在 Windows 10 中，使用自定义的 INF 作为照相机 (驱动程序支持 UVC 的自定义元数据，注意：照相机驱动程序可以基于 Windows USBVIDEO.SYS，但对于给定的硬件，需要自定义的 INF 才能通过) 。 如果 `MetadataBufferSizeInKB<PinIndex>` 注册表项存在且非零，则该 pin 支持自定义元数据，值指示用于元数据的缓冲区大小。 此 `<PinIndex>` 字段指示视频 pin 索引的从0开始的索引。

在 Windows 10 版本1703中，照相机驱动程序可以通过包含以下 AddReg 条目来向 Microsoft 标准格式元数据提供信号支持：

`StandardFormatMetadata<PinIndex>`： REG_DWORD： 0x0 (NotSupported) 到 0x1 (支持) 

此注册表项将由 DevProxy 读取，并通过在 KSSTREAM_METADATA_INFO 结构的 "标志" 字段中设置标志 KSSTREAM_METADATA_INFO_FLAG_STANDARDFORMAT，通知 UVC 驱动程序元数据为标准格式。

##### <a name="2231-microsoft-standard-format-metadata"></a>2.2.3.1 Microsoft 标准格式的元数据

Microsoft 标准格式的元数据是以下结构的一个或多个实例：

![标准格式元数据](images/extension-standard-format-metadata.png)

```cpp
typedef struct tagKSCAMERA_METADATA_ITEMHEADER {
    ULONG MetadataId;
    ULONG Size; // Size of this header + metadata payload following
} KSCAMERA_METADATA_ITEMHEADER, *PKSCAMERA_METADATA_ITEMHEADER;
```

MetadataId 字段由以下枚举定义中的标识符填充，其中包含定义良好的标识符以及自定义标识符 (标识符 >= MetadataId_Custom_Start) 。

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

"大小" 字段设置为 sizeof (KSCAMERA_METADATA_ITEMHEADER) + sizeof (元数据负载) 。

##### <a name="2232-firmware-generated-standard-format-metadata-from-usb-video-frame-packets"></a>2.2.3.2 固件-从 USB 视频帧包生成的标准格式元数据

在基于帧的视频的 UVC 传输过程中，视频帧会打包后到一系列包中，每个数据包前面都有一个 UVC 负载标头。 每个 UVC 负载标头都是通过基于 USB 视频类驱动程序帧的有效负载规范定义的：

**负载标头**

下面是基于帧格式的负载标头格式的说明。

![负载标头](images/uvc-1-15-10.png)

**HLE (标题长度) 字段**

标头长度字段指定标头的长度（以字节为单位）。

**位域标题字段**

*FID：帧标识符*

- 此位在每个帧开始边界处切换，并为框架的其余部分保持不变。

*EOF：帧结尾*

- 此位指示视频帧的末尾，并在属于帧的最后一个视频示例中设置。 使用此位是为了减少帧传输完成时的延迟，并且是可选的。

*PT：演示时间戳*

- 设置此位时，指示是否存在 PT 字段。

*SCR：源时钟引用*

- 设置此位后，表示 SCR 字段的状态。

*RES：保留。*

- 设置为0。

*STI：仍图像*

- 设置此位后，会将视频示例标识为属于静止图像。

*错误：错误位*

- 设置此位后，将指示设备流式处理中的错误。

*EOH：标头结尾*

- 设置此位后，将指示 BFH 字段的结尾。

*PT：演示时间戳，大小：4个字节，值：数字*

- 在 BFH [0] 字段中设置 PT 位时，将显示 "PT" 字段。 请参阅 *视频设备的 USB 设备类定义* 中的 2.4.3.3 "视频和静态图像负载标头" 部分。

*SCR：源时钟引用，大小：6个字节，值：数字*

- 当在 BFH [0] 字段中设置 SCR 位时，"SCR" 字段存在。 请参阅*视频设备的 USB 设备类定义*中的 2.4.3.3*视频和静止图像负载标头*部分。

现有 UVC 驱动程序中的 HLE 字段已固定为2个字节， (不存在磅/SCR) 或最多12个字节， (磅/SCR 存在) 。 但是，HLE 字段是字节大小的字段，可能最多可以指定255字节的标头数据。 如果同时存在 PT/SCR 和 HLE isgreater 12 个字节，则在设置了 INF 项时，将在特定于视频帧的标准元数据的情况下，将在负载标头的前12个字节后面添加任何其他数据 `StandardFormatMetadata<PinIndex>` 。

为帧生成的固件)  (标准格式的元数据是通过连接在视频帧中找到的部分 blob 来获取的。

![元数据帧数据包](images/extension-metadata-frame-packets.png)

##### <a name="2233-metadata-buffer-provided-to-user-mode-component"></a>提供给用户模式组件的2.2.3.3 元数据缓冲区

向用户模式组件提供的元数据缓冲区将具有 UVC 时间戳的元数据项， (由 UVC 驱动) 程序生成，然后是固件生成的元数据项，其布局如下：

![元数据缓冲区](images/extension-metadata-buffer.png)

##### <a name="2234-metadata-format-for-standard-metadata-identifiers"></a>标准元数据标识符的2.2.3.4 元数据格式

固件可以选择是否生成与标识符对应的元数据。 如果固件选择生成与标识符对应的元数据，则该标识符的元数据应出现在固件发出的所有帧中。

###### <a name="22341-metadataid_capturestats"></a>2.2.3.4.1 MetadataId_CaptureStats

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

" **标志** " 字段指示在结构中填充了哪些后面的字段并具有有效的数据。 "标志" 字段不应与帧不同。 目前，定义了以下标志：

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

**保留**字段保留供将来，并应设置为0。

**ExposureTime**字段包含捕获帧时应用于传感器的曝光时间（以100ns 为单位）。 这将显示为相应的 MF 示例上的属性 MF_CAPTURE_METADATA_EXPOSURE_TIME。

**ExposureCompensationFlags**字段包含 ev 补偿步骤 (应) 用于传递 EV 补偿值的 KSCAMERA_EXTENDEDPROP_EVCOMP_XXX 步骤标志之一。 **ExposureCompensationValue**字段包含在捕获帧时应用到传感器的步骤单位内的 EV 补偿值。 它们将显示为相应的 MF 示例上的属性 MF_CAPTURE_METADATA_EXPOSURE_COMPENSATION。

**IsoSpeed**字段包含捕获帧时应用于传感器的 ISO 速度值。 这是无单位的。 这将显示为相应的 MF 示例上的属性 MF_CAPTURE_METADATA_ISO_SPEED。

**FocusState**字段包含当前焦点状态，该状态可采用枚举 KSCAMERA_EXTENDEDPROP_FOCUSSTATE 中定义的值之一。 这将显示为相应的 MF 示例上的属性 MF_CAPTURE_METADATA_FOCUSSTATE。

**LensPosition**字段包含捕获帧时的逻辑镜头位置，这是无单位的。 此值与可通过 GET 调用中的 KSPROPERTY_CAMERACONTROL_EXTENDED_FOCUS 查询的值相同。 这将显示为相应的 MF 示例上的属性 MF_CAPTURE_METADATA_LENS_POSITION。

**WhiteBalance**字段包含在捕获帧时应用于传感器的白余额，这是一个开氏值。 这将显示为相应的 MF 示例上的属性 MF_CAPTURE_METADATA_WHITEBALANCE。

**Flash**字段包含一个布尔值，其中1表示闪光灯开启，0表示闪存关闭，在捕获帧时也是如此。 这将显示为相应的 MF 示例上的属性 MF_CAPTURE_METADATA_FLASH。

**FlashPower**字段包含应用到捕获帧的闪存功率，该帧是 [0，100] 范围内的值。 如果驱动程序不支持闪存的可调整功率，则应忽略此字段。 这将显示为相应的 MF 示例上的属性 MF_CAPTURE_METADATA_FLASH_POWER。

**ZoomFactor**字段包含应用到捕获帧的 Q16 格式的缩放值。 这将显示为相应的 MF 示例上的属性 MF_CAPTURE_METADATA_ZOOMFACTOR。

**SceneMode**字段包含应用到捕获帧的场景模式，这是一个64位 KSCAMERA_EXTENDEDPROP_SCENEMODE_XXX 标志。 这将显示为相应的 MF 示例上的属性 MF_CAPTURE_METADATA_SCENE_MODE。

在捕获帧时，" **SensorFramerate** " 字段包含度量的传感器读数率（以赫兹为单位），其中包含32位的分子值和较低32位的分母值。 这将显示为相应的 MF 示例上的属性 MF_CAPTURE_METADATA_SENSORFRAMERATE。

###### <a name="22342-metadataid_cameraextrinsics"></a>2.2.3.4.2 MetadataId_CameraExtrinsics

此标识符的元数据格式涉及标准 KSCAMERA_METADATA_ITEMHEADER 后跟字节数组有效负载。 有效负载应与后跟零个或多个[MFCameraExtrinsic_CalibratedTransform](https://docs.microsoft.com/windows/win32/api/mfapi/ns-mfapi-_mfcameraextrinsic_calibratedtransform)结构的[MFCameraExtrinsics](https://docs.microsoft.com/windows/win32/api/mfapi/ns-mfapi-_mfcameraextrinsics)结构对齐。 有效负载必须是8字节对齐的，所有未使用的字节应在负载结束时进行，并设置为0。

###### <a name="22343-metadataid_cameraintrinsics"></a>2.2.3.4.3 MetadataId_CameraIntrinsics

此标识符的元数据格式涉及标准 KSCAMERA_METADATA_ITEMHEADER 后跟字节数组有效负载。 有效负载应与 [MFPinholeCameraIntrinsics](https://docs.microsoft.com/windows/win32/api/mfapi/ns-mfapi-_mfpinholecameraintrinsics) 结构对齐。 有效负载必须是8字节对齐的，所有未使用的字节应在负载结束时进行，并设置为0。

###### <a name="22344-metadataid_frameillumination"></a>2.2.3.4.4 MetadataId_FrameIllumination

此标识符的元数据格式由以下结构定义：

```cpp
typedef struct tagKSCAMERA_METADATA_FRAMEILLUMINATION {
    KSCAMERA_METADATA_ITEMHEADER Header;
    ULONG Flags;
    ULONG Reserved;
} KSCAMERA_METADATA_FRAMEILLUMINATION, *PKSCAMERA_METADATA_FRAMEILLUMINATION;
```

" **标志** " 字段指示有关捕获的帧的信息。 目前，定义了以下标志：

```cpp
#define KSCAMERA_METADATA_FRAMEILLUMINATION_FLAG_ON 0x00000001
```

如果在启用照明时捕获帧，则应设置标志 KSCAMERA_METADATA_FRAMEILLUMINATION_FLAG_ON。 否则，不应设置此标志。

**保留**字段保留供将来使用，并且应设置为0。
