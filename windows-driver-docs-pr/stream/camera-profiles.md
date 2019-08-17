---
title: 照相机配置文件
description: 本主题讨论照相机配置文件的格式和定义它们的各种方式
ms.date: 08/16/2019
ms.localizationpriority: medium
ms.openlocfilehash: 641bfb29715f3b846864a9ac90dc89007e1e750f
ms.sourcegitcommit: fec48fa5342d9cd4cd5ccc16aaa06e7c3d730112
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2019
ms.locfileid: "69565929"
---
# <a name="camera-profiles"></a>照相机配置文件

## <a name="ks-api-profile"></a>KS API 配置文件

### <a name="ksinitializedeviceprofile"></a>KsInitializeDeviceProfile

若要发布设备配置文件, 所有微型端口驱动程序都必须初始化配置文件存储区, 若要执行此操作, 必须调用以下 KS API:

```c
__drv_maxIRQL(PASSIVE_LEVEL)
KSDDKAPI
NTSTATUS
NTAPI
KsInitializeDeviceProfile(
    __in PKSFILTERFACTORY FilterFactory
    );
```

#### <a name="filterfactory-ksfilterfactory"></a>FilterFactory (KSFILTERFACTORY)

这是由相机驱动程序创建的 KSFILTERFACTORY, 用于唯一标识相机的筛选器工厂。

必须使用此筛选器类型的唯一 GUID 为\_KSFILTERFACTORY 中包含的 KSFILTER 描述符结构的 ReferenceGuid 字段进行设置。 而且, KSFILTER\_描述符的 Flags 字段具有 KSFILTER\_标志\_, 同时设置\_REFERENCEGUID 标志的优先级。

如果提供的 KSFILTERFACTORY 不包含与\_KSCATEGORY 视频\_相机关联的设备接口, 此 API\_调用将失败, 并显示 "无效\_" 参数。

若要从与此 KSFILTERFACTORY 的设备接口相关联的配置文件存储中删除所有配置文件, 驱动程序可能会调用 KsInitializeDeviceProfile, 后跟 KsPersistDeviceProfile。 这将导致空的配置文件信息, 这会从配置文件存储区中删除配置文件信息。

### <a name="kspublishdeviceprofile"></a>KsPublishDeviceProfile

为了发布此信息, 引入了以下新的 KS API:

```c
__drv_maxIRQL(PASSIVE_LEVEL)
KSDDKAPI
NTSTATUS
NTAPI
KsPublishDeviceProfile(
    __in PKSFILTERFACTORY FilterFactory,
    __in PKSDEVICE_PROFILE_INFO Profile
    );
```

对于照相机驱动程序支持的每个配置文件, 将重复调用此 API。 每个调用可以具有不同的并发和数据范围信息集。 KSCAMERA\_配置文件\_信息的配置文件 id 字段必须是唯一的。 如果使用相同的配置文件 id, 并且配置文件信息的内容不同, 则后续调用将覆盖以前的配置文件信息。

#### <a name="filterfactory-ksfilterfactory"></a>FilterFactory (KSFILTERFACTORY)

这与 KsInitializeDeviceProfile API 中使用的 FilterFactory 相同。

照相机配置文件信息将仅与 KSCATEGORY\_视频\_相机界面类别关联。 如果创建的任何筛选器工厂都没有此接口类别, 并且尝试注册照相机配置文件, 则会导致\_此\_API 返回状态 "无效参数"。

#### <a name="profile-ksdevice_profile_info"></a>配置文件 (\_KSDEVICE\_配置文件信息)

KSDEVICE\_配置文件\_信息是设计用于处理各种设备类型的配置文件信息的一般结构:

```c
##define KSDEVICE_PROFILE_TYPE_CAMERA 0x00000001

typedef struct _KSDEVICE_PROFILE_INFO
{
    UINT32 Type;
    UINT32 Size;
    union
    {
        struct
        {
            KSCAMERA_PROFILE_INFO Info;
            UINT32 Reserved;
            UINT32 ConcurrencyCount;
            PKSCAMERA_PROFILE_CONCURRENCYINFO Concurrency;
        } Camera;

        // Add other device type specific "profiles" here.
    };
} KSDEVICE_PROFILE_INFO, *PKSDEVICE_PROFILE_INFO;
```

类型

定义配置文件的类型。 目前唯一定义的类型是 KSDEVICE\_配置\_文件\_类型相机。

***大小***

这必须设置为 sizeof (KSDEVICE\_PROFILE\_INFO) 结构。

***Camera.Info***

定义相机的\_配置\_文件信息的 KSCAMERA 配置文件的结构。

***照相机。已保留***

用. 必须设置为0。

***ConcurrencyCount***

并发数组中\_的\_KSCAMERA PROFILE CONCURRENCYINFO 结构的数目。 对于 Windows 阈值, 此值必须小于或等于1。
>
如果值为 0 (将 "摄像" 设置为 NULL), 则表示此配置文件不是并发的。

***摄影机***

KSCAMERA\_配置文件\_CONCURRENCYINFO 结构的数组, 描述此配置文件的并发支持。 如果 CountOfConcurrency 为 0, 则此参数必须为 NULL。 如果 CountOfConcurrency 为\>0, 则此参数不得为 NULL。

#### <a name="kscamera_profile_info"></a>KSCAMERA_PROFILE_INFO

KSCAMERA\_配置文件\_信息结构用于唯一标识给定的配置文件:

```c
typedef struct _KSCAMERA_PROFILE_INFO
{
    UINT32 ProfileId;
    UINT32 Index;
    UINT32 PinCount;
    PKSCAMERA_PROFILE_PININFO Pins
} KSCAMERA_PROFILE_INFO, *PKSCAMERA_PROFILE_INFO;
```

***配置文件 id***

表示配置文件的唯一 ID 的 GUID。 此 GUID 可以是唯一的 IHV/OEM 创建的 GUID, 它表示一个自定义配置文件, 或者它可能是第3.1 节中所述的预定义 Guid 之一。

注意：不得将此字段设置为 KSCAMERAPROFILE\_旧版。 照相机驱动程序不得发布旧配置文件。 如果应用程序未指出它可以支持配置文件, 则会将旧配置文件 ID 发送到相机驱动程序。 在这种情况下, 照相机驱动程序必须将其行为恢复到 Windows 8.1 的操作模式, 并且只公开缩减的集媒体类型以及相应\_的\_KSPROPERTY\_CAMERACONTROL 图像 PIN\_\_具有RECORD\_和\_KSPROPERTY CAMERACONTROLIMAGE\_引脚功能序列的\_功能\_\_\_\_专用\_于\_记录功能位, 指示照相机驱动程序是否能够支持在缩减集媒体类型内同时进行录制/照片和/或录制/照片序列。

***索引***

给定配置文件 id 组中的每个配置文件必须具有唯一的索引值。 这允许使用配置文件 id + 索引唯一标识设备的任何配置文件。

***PinCount***

Pin 指向的 KSCAMERA\_配置\_文件 PININFO 结构的数目。 此值必须为\>0。

***根***

KSCAMERA\_配置文件\_PININFO 结构的数组, 用于定义此配置文件的每个 pin 上支持的媒体类型。

此字段不能为 NULL。

#### <a name="concurrency-kscamera_profile_concurrencyinfo"></a>Concurrency (KSCAMERA\_PROFILE\_CONCURRENCYINFO)

目前, 应用程序不知道它是否可以尝试从多个相机进行流式处理, 直到尝试成功或失败。
对于 Web 博客方案, 这意味着应用程序必须先尝试激活这两个流, 然后再使用 picture 视频元素中的图片绘制 UI。

Concurrency 参数将向应用程序提供提示: 可以使用特定配置文件 (或配置文件集) 同时激活前端和后端。 了解这一点后, 应用程序可以在激活前绘制两个流的 UI 元素。

对于多个应用程序, 并发性将不足以保证并发操作。 并发信息不会尝试解决此问题。 而是将利用 Windows 8 的现有照相机 Yanking 功能。

Concurrency 参数表示 KSCAMERA\_profile\_CONCURRENCYINFO 结构的数组 (其数组大小由 CountOfConcurrency 参数指定), 指示配置文件在KSCAMERA\_配置\_文件信息结构可以在不同相机上同时运行。

如果 CountOfConcurrency 和字段分别为 0 & NULL, 则它向操作系统指示 KSCAMERA\_配置\_文件定义的配置文件不是并发配置文件。

```c
typedef struct _KSCAMERA_PROFILE_CONCURRENCYINFO
{
    GUID ReferenceGuid;
    UINT32 Reserved;
    UINT32 ProfileCount;
    PKSCAMERA_PROFILE_INFO Profiles;
} KSCAMERA_PROFILE_CONCURRENCYINFO,*PKSCAMERA_PROFILE_CONCURRENCYINFO;
```

***ReferenceGuid***

必须设置为 KSFILTER\_描述符的 ReferenceGuid, 它对应于此配置文件的其他设备。

***保护***

用. 必须为 0。

***ProfileCount***

配置文件数组中包含的配置文件 Id 的数量。 必须大于0。

***Profiles***

这是 KSCAMERA\_配置文件\_信息的数组, 可同时在 ReferenceGuid 指定的其他照相机设备上使用。

此字段不能为 NULL。

#### <a name="pins-kscamera_profile_pininfo"></a>Pin (KSCAMERA\_PROFILE\_PININFO)

若要指定每个 pin 的可用媒体类型列表, 必须指定 KSCAMERA\_配置文件\_PININFO 的数组, 其中的数组大小由 CountOfPins 参数指定。

```c
typedef struct _KSCAMERA_PROFILE_PININFO
{
    GUID PinCategory;
    UINT32 Reserved;
    UINT32 MediaInfoCount;
    PKSCAMERA_PROFILE_MEDIAINFO MediaInfos;
} KSCAMERA_PROFILE_PININFO, *PKSCAMERA_PROFILE_PININFO;
```

***PinCategory***

这是对应于捕获、预览或静止图像 pin 的 PINNAME 类别。 对于 Windows 阈值, 唯一支持的 pin 类别为:PINNAME\_\_视频\_捕获、PINNAME\_视频\_预览、PINNAME 视频\_。 所有其他类别将导致 "\_无效\_参数" 错误。

***保护***

用. 必须为 0。

***MediaInfoCount***

MediaInfos 字段中指定\_的\_KSCAMERA PROFILE mediainfo.xml 结构的数组大小。

***Mediainfo.xml***

KSCAMERA\_配置文件\_mediainfo.xml 结构的数组。

#### <a name="mediainfos-kscamera_profile_mediainfo"></a>MediaInfos (KSCAMERA\_PROFILE\_mediainfo.xml)

为每个配置文件提供的相关媒体类型信息如下所述:

```c
##define KSCAMERAPROFILE_FLAGS_VIDEOHDR              0x0000000000000002
##define KSCAMERAPROFILE_FLAGS_VARIABLEPHOTOSEQUENCE 0x0000000000000010

typedef struct _KSCAMERA_PROFILE_MEDIAINFO
{
    struct
    {
        UINT32 X;
        UINT32 Y;
    } Resolution;
    struct
    {
        UINT32 Numerator;
        UINT32 Denominator;
    } MaxFrameRate;
    ULONGLONG Flags;
    UINT32 Data0;
    UINT32 Data1;
    UINT32 Data2;
    UINT32 Data3;
} KSCAMERA_PROFILE_MEDIAINFO, *PKSCAMERA_PROFILE_MEDIAINFO;
```

***解决方法***

X (水平) 和 Y (垂直) 帧大小 (以像素为单位)。

***MaxFrameRate***

帧速率的 denom 比 (例如, 30/1 = 30fps)。 此帧速率表示在理想照明条件下指定分辨率的最大帧速率。 实际帧速率可能低于此值。

对于照片媒体信息, 如果由于给定照片分辨率的硬件限制而无法启用照片序列, 则帧速率必须设置为 0 (num = 0, denom = 0)。 这会通知应用程序层当选择特定照片媒体类型时, 驱动程序将拒绝照片序列控件。

***随意***

可以是以下一个或多个标志的位或:

- **KSCAMERAPROFILE\_标志\_VIDEOHDR**为媒体信息设置了视频 hdr 标志时, 可能会为记录流启用视频 hdr。

  不得为照片 pin 上的媒体信息设置此标志。
- **KSCAMERAPROFILE\_FLAGS\_VARIABLEPHOTOSEQUENCE**当为媒体信息设置了可变照片序列标志时, 即使照片媒体信息未提供帧速率, VPS 支持也可用。

  如果设置此标志 & 帧速率为非零, 则照片媒体信息、VPS 和照片序列可用。

  如果设置此标志 & 帧速率为零, 则对于该照片媒体信息, VPS 可用, 但不是照片序列。

  如果未设置此标志 & 帧速率为非零, 则为该照片媒体信息, VPS 不可用, 但照片序列可用。

  如果未设置此标志 & 帧速率为零, 则 VPS 和照片序列都不能用于该媒体信息。

  只能为照片 pin 上的媒体信息设置此标志。 如果在非照片 pin 媒体信息上存在此标志, 将导致配置文件集被拒绝。

***Data0 。三维空间***

基于标志确定的值。 此时, 必须设置为0。

### <a name="kspersistdeviceprofile"></a>KsPersistDeviceProfile

若要将配置文件信息提交到持久存储区, 则必须调用以下 KS API。

```c
__drv_maxIRQL(PASSIVE_LEVEL)
KSDDKAPI
NTSTATUS
NTAPI
KsPersistDeviceProfile(
    __in PKSFILTERFACTORY FilterFactory
    );
```

#### <a name="filterfactory-ksfilterfactory"></a>FilterFactory (KSFILTERFACTORY)

这是用于在 KsInitializeDeviceProfile 中初始化配置文件存储区的 KSFILTERFACTORY。 如果在没有首次初始化配置文件存储区的情况下调用 KsPersistDeviceProfile, 则对 KsPersistDeviceProfile 的\_调用\_将\_失败, 状态为 "设备请求无效"。

此外, 如果在保留配置文件信息时\_,\_此 API 也可能失败, 并出现 "资源不足" 状态。

### <a name="ksproperty_cameracontrol_extended_profile"></a>KSPROPERTY_CAMERACONTROL_EXTENDED_PROFILE

> ***内版本1***
>
> ***控件筛选器***
>
> ***类型：异步, 不可取消***

引入了一个新的扩展属性控件, 以允许捕获框架通知照相机驱动程序已选择哪个配置文件。

#### <a name="kscamera_extendedprop_header"></a>KSCAMERA_EXTENDEDPROP_HEADER

**版本**

为扩展属性控制版本1定义。

**PinId**

必须为`KSCAMERA_EXTENDEDPROP_FILTERSCOPE` (0xffffffff)。

**大小**

必须是`sizeof(KSCAMERA_EXTENDEDPROP_HEADER) +
sizeof(KSCAMERA_EXTENDEDPROP_PROFILE)`。

**输出**

指示上一次设置操作的错误结果。 如果未执行任何设置操作, 则此必须为0。 0指示未检测到任何错误。

**功能**

必须是`KSCAMERA_EXTENDEDPROP_CAPS_ASYNCCONTROL`。 不支持任何其他模式。

**随意**

必须为 0。

#### <a name="kscamera_extendedprop_profile"></a>KSCAMERA_EXTENDEDPROP_PROFILE

KSPROPERTY\_\_CAMERACONTROL\_\_扩展配置文件控件的负载包含 KSCAMERA EXTENDEDPROP 标头 + KSCAMERA EXTENDEDPROP\_ \_\_简介.

```c
typedef struct _KSCAMERA_EXTENDEDPROP_PROFILE
{
    GUID ProfileId;
    UINT32 Index;
    UINT32 Reserved;
} KSCAMERA_EXTENDEDPROP_PROFILE, *PKSCAMERA_EXTENDEDPROP_PROFILE;
```

**配置文件 id**

表示所选配置文件的 GUID。 如果这是 KSCAMERAPROFILE\_, 则未选择任何配置文件, 照相机驱动程序必须公开精简的设置媒体类型。

如果此字段为 GUID\_NULL, 则未选择任何配置文件, 但该应用程序已识别配置文件, 因此照相机驱动程序必须公开所有媒体类型。

**索引**

与标识的配置文件关联的索引值。

**保护**

用. 必须为 0。

## <a name="inf-profile"></a>INF 配置文件

若要允许 Oem 基于不同 Sku (可能使用相同的引用驱动程序但不同的传感器, 甚至在不同的性能级别的情况下), 可以通过使用以下 INF 部分来发布或覆盖配置文件:

每个配置文件 (新的或现有的\[) 都必须在\] "设备接口" 节点下存储的以分号分隔的字符串中具有其 ProfildId GUID、索引值:

```reg
OEMCameraProfiles: REG_SZ:
KSCAMERAPROFILE_VideoRecording,0;KSCAMERAPROFILE_HighQualityPhoto,0;KSCAMERAPROFILE_BalancedVideoPhoto,0;KSCAMERAPROFILE_VideoConferencing,0;{3074C75C-1D69-4A0A-895D-EB9EFDE1CF30},0
```

在上面的示例中, 我们将覆盖<sup>第</sup>0 个索引的\_KSCAMERAPROFILE VideoRecording、\_KSCAMERAPROFILE HighQualityPhoto、\_KSCAMERAPROFILE BalancedVideoPhoto 和\_ KSCAMERAPROFILE视频视频, 以及 ID 为 {3074C75C-1D69-4A0A-895D-EB9EFDE1CF30} 的新自定义配置文件

对于 OEMCameraProfiles 中的每个配置文件 GUID, 必须在与分隔字符串中指定的名称相匹配的 "设备接口" 节点中创建新的子项。

在此子项下, OEM 可能会通过添加以下值来指示已禁用配置文件 (从而替代驱动程序发布的设置):

```reg
Disabled: REG_DWORD: 0x1
```

如果 OEM 要更改或发布可用的媒体类型, 而不是只是禁用该配置文件, 则必须创建与该流的 PinCategory 相匹配的子项。

例如, 若要发布<sup>第</sup>0 个索引的 KSCAMERAPROFILE\_VideoRecording 的预览 pin:

```reg
<Device Interface Node>KSCAMERAPROFILE_VideoRecording,0\PINNAME_VIDEO_PREVIEW

MediaCount: REG_DWORD: N
Media0: REG_SZ: <MediaInfo Format>
...
MediaN-1: REG_SZ: <MediaInfo Format>
```

MediaCount 注册表值指示此 pin 存在的 Mediainfo.xml 数。 必须为每个 mediainfo.xml 指定一个注册表项名称 "Media\#", 其中, \ 表示从0开始的索引 (即, Media0、Media1、Media2,..., 中值为-1)。

Media0 指定的 Mediainfo.xml 将被视为该配置文件的首选媒体类型。

上面的 Mediainfo.xml 格式采用以下语法:

```reg
MediaInfo Format = <ResolutionX>, <ResolutionY>, <MaxFrameRateNum>,<MaxFrameRateDenom>, Flags, Data0, Data1, Data2, Data3
```

如下所示:

```reg
<Device Interface Node>KSCAMERAPROFILE_VideoRecording,0\PINNAME_VIDEO_PREVIEW

MediaCount: REG_DWORD: 2
Media0: REG_SZ: 1280,720,30,1,0,0,0,0,0
Media1: REG_SZ: 640,360,30,1,0,0,0,0,0

<Device Interface
Node>KSCAMERAPROFILE_VideoRecording,0\PINNAME_VIDEO_CAPTURE

MediaCount: REG_DWORD: 3
Media0: REG_SZ: 1280,720,30,1,0,0,0,0,0
Media1: REG_SZ: 1920,1080,30,1,0,0,0,0,0
Media2: REG_SZ: 640,360,30,1,0,0,0,0,0
```

将从 IHV 的设置中发布 VideoRecording 配置文件, 以仅允许1080p 和360p 预览, 同时仅允许720p 和预览, 无需任何照片支持。

若要定义自定义配置文件, 可以使用相同的语法, 但使用自定义配置文件的 GUID ID 替换配置文件名称:

```reg
<Device Interface
Node>{3074C75C-1D69-4A0A-895D-EB9EFDE1CF30},0\PINNAME_VIDEO_PREVIEW

MediaCount: REG_DWORD: 2
Media0: REG_SZ: 1280,720,30,1,0,0,0,0,0
Media1: REG_SZ: 640,360,30,1,0,0,0,0,0

<Device Interface
Node>{3074C75C-1D69-4A0A-895D-EB9EFDE1CF30},0\PINNAME_VIDEO_CAPTURE
MediaCount: REG_DWORD: 2
Media0: REG_SZ: 1280,720,30,1,0,0,0,0,0
Media2: REG_SZ: 640,360,30,1,0,0,0,0,0

<Device Interface
Node>{3074C75C-1D69-4A0A-895D-EB9EFDE1CF30},0\PINNAME_IMAGE
MediaCount: REG_DWORD: 2
Media0: REG_SZ: 1920,1080,0,0,0,0,0,0,0
Media1: REG_SZ: 1280,720,0,0,0,0,0,0,0
```

可以采用适用于 OEM 的任何方式来处理对注册表的修改。 建议的过程是为照相机驱动程序的 INF 文件创建一个 AddReg 部分, 以便在照相机安装过程中创建注册表项 (并在删除驱动程序时删除):

```INF
[SampleDriver.DeviceInterface.AddReg]
HKR,,”OEMCameraProfiles”,0,”KSCAMERAPROFILE_VideoRecording,0”,
HKR,”KSCAMERAPROFILE_VideoRecording,0\PINNAME_VIDEO_PREVIEW”,”MediaCount”,0x00010001,2,
HKR,”KSCAMERAPROFILE_VideoRecording,0\PINNAME_VIDEO_PREVIEW”,”Media0”,0,”1280,720,30,1,0,0,0,0,0”,
HKR,”KSCAMERAPROFILE_VideoRecording,0\PINNAME_VIDEO_PREVIEW”,”Media1”,0,”640,360,30,1,0,0,0,0,0”,
```

…

### <a name="inf-profile--concurrency"></a>INF 配置文件:能力

若要发布配置文件的并发设置, 可以添加以下注册表值:

```reg
<Device Interface Node>KSCAMERAPROFILE_VideoConferencing,0

Concurrency: REG_SZ:
{ConcurrentDeviceReferenceGUID};{ProfileID},{Index};…
```

ConcurrentDeviceRefefenceGUID 是与照相机相关联的 KSFILTER\_描述符的 ReferenceGUID, 此配置文件可以同时运行。

### <a name="example-inf"></a>示例 INF

```INF
;---------------------------------------------------------------
; S t r i n g s
;---------------------------------------------------------------

[Strings]
; non-localizable
RefGUIDFrontCamera="{C3FDE193-01D1-4A78-AA0F-0D2395611C3D}"
RefGUIDRearCamera="{3E5169E8-8DB8-4951-A33F-CFF94F2C87BE}"

;---------------------------------------------------------------
; A d d R e g
;---------------------------------------------------------------

[SampleDriver.FrontCameraInterface.AddReg]
HKR,,"OEMCameraProfiles",0,"KSCAMERAPROFILE_VideoRecording;KSCAMERAPROFILE_VideoConferencing;KSCAMERAPROFILE_HighQualityPhoto;KSCAMERAPROFILE_PhotoSequence",
HKR,,"ReferenceGUID",0,%RefGUIDFrontCamera%
HKR,"KSCAMERAPROFILE_VideoRecording,0\PINNAME_VIDEO_PREVIEW","MediaCount",0x00010001,2,
HKR,"KSCAMERAPROFILE_VideoRecording,0\PINNAME_VIDEO_PREVIEW","Media0",0,"1280,720,30,1,0,0,0,0,0",
HKR,"KSCAMERAPROFILE_VideoRecording,0\PINNAME_VIDEO_PREVIEW","Media1",0,"640,360,30,1,0,0,0,0,0",
HKR,"KSCAMERAPROFILE_VideoRecording,0\PINNAME_VIDEO_CAPTURE","MediaCount",0x00010001,2,
HKR,"KSCAMERAPROFILE_VideoRecording,0\PINNAME_VIDEO_CAPTURE","Media0",0,"1280,720,30,1,0,0,0,0,0",
HKR,"KSCAMERAPROFILE_VideoRecording,0\PINNAME_VIDEO_CAPTURE","Media1",0,"640,360,30,1,0,0,0,0,0",
HKR,"KSCAMERAPROFILE_PhotoSequence,0","Disabled",0x00010001,1,
HKR,"KSCAMERAPROFILE_HighQualityPhoto,0\PINNAME_VIDEO_PREVIEW","Media0",0,"1280,720,30,1,0,0,0,0,0",
HKR,"KSCAMERAPROFILE_HighQualityPhoto,0\PINNAME_VIDEO_PREVIEW","Media1",0,"640,360,30,1,0,0,0,0,0",
HKR,"KSCAMERAPROFILE_HighQualityPhoto,0\PINNAME_IMAGE","MediaCount",0x00010001,2,
HKR,"KSCAMERAPROFILE_HighQualityPhoto,0\PINNAME_IMAGE","Media0",0,"1920,1080,0,0,0,0,0,0,0",
HKR,"KSCAMERAPROFILE_HighQualityPhoto,0\PINNAME_IMAGE","Media1",0,"1280,720,5,1,0,0,0,0,0",
HKR,"KSCAMERAPROFILE_VideoConferencing,0\PINNAME_VIDEO_PREVIEW","MediaCount",0x00010001,2,
HKR,"KSCAMERAPROFILE_VideoConferencing,0\PINNAME_VIDEO_PREVIEW","Media0",0,"1280,720,30,1,0,0,0,0,0",
HKR,"KSCAMERAPROFILE_VideoConferencing,0\PINNAME_VIDEO_PREVIEW","Media1",0,"640,360,30,1,0,0,0,0,0",
HKR,"KSCAMERAPROFILE_VideoConferencing,0\PINNAME_VIDEO_CAPTURE","MediaCount",0x00010001,2,
HKR,"KSCAMERAPROFILE_VideoConferencing,0\PINNAME_VIDEO_CAPTURE","Media0",0,"1280,720,30,1,0,0,0,0,0",
HKR,"KSCAMERAPROFILE_VideoConferencing,0\PINNAME_VIDEO_CAPTURE","Media1",0,"640,360,30,1,0,0,0,0,0",
HKR,"KSCAMERAPROFILE_VideoConferencing,0","Concurrency",0,"%RefGUIDRearCamera%;KSCAMERAPROFILE_VideoConferencing,0",
```

上述 INF 的 "示例" 部分显示了和 OEM 可以为配置文件发布 (或替代默认 IHV) 设置的方式。 在上面的示例中, 第0个的 VideoRecording 索引仅限预览和记录的 720p30, 无相片支持。

还禁用了前面照相机的 PhotoSequence (替代 IHV 的已发布配置文件)。

HighQualityPhoto 配置文件仅限在5fps 上提供1080p 单一拍摄或720p 照片的720p 预览。

视频视频配置文件仅用于预览和捕获, 同时表明可以同时与后摄像机视频配置文件一起运行 (后摄像机的视频记录配置文件不会显示在 INF 中,在 INF 中指定的后端摄像机视频配置文件将使用已发布的任何 IHV, 如果不存在, 则将禁用配置文件, 因为上述替代无效。

## <a name="inf-vs-ks-api-profile"></a>INF 与KS API 配置文件

INF 配置文件信息将始终取代 KS API 发布的配置文件信息。 优先级为每个配置文件级别。

如果驱动程序使用 KS API 发布 VideoRecording、HighQualityPhoto、视频记录配置文件, 并且 INF 设置包含 HighQualityPhoto 的配置文件条目, 则只会覆盖驱动程序发布的 HighQualityPhoto 配置文件INF 中的配置文件信息。

这样做的目的是, 单个引用驱动程序 (由 IHV 实现) 可能会发布一组可用于给定传感器的配置文件, 但 OEM 可能会决定选择其他传感器和/或由于最终外形规格, 可以选择更改/限制可用的配置文件。

INF 配置文件还允许 Oem 不更改驱动程序二进制文件, 只需更新其 INF 即可发布现有 Windows 8.1 驱动程序的配置文件。
