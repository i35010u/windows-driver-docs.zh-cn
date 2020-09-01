---
title: 捕获统计信息元数据属性
description: 本主题讨论应由 MFT0 填充或转发的可用捕获统计信息元数据 IMFAttributes
ms.date: 08/16/2019
ms.localizationpriority: medium
ms.openlocfilehash: c54483b94a5707671f6aa0e3ba34fc16d21986a7
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89184378"
---
# <a name="capture-stats-metadata-attributes"></a>捕获统计信息元数据属性

下表汇总了用于预览、视频和仍捕获的 MFT0's **MFSampleExtension \_ CaptureMetaData** 元数据属性包的可用捕获统计信息 IMFAttributes。

除非另有说明，否则，为每个已捕获的照片强制执行列出的捕获统计信息。 为预览和视频列出的捕获统计信息应作为最大努力提供，驱动程序可能会，也可能不会基于可用性和性能注意事项来提供所有帧上的所有捕获统计信息。

| 名称                                                                                              | 类型             | Pin                   | 描述            |
| ------------------------------------------------------------------------------------------------- | ---------------- | --------------------- | ---------------------- |
| [MF \_ 捕获 \_ 元数据 \_ FOCUSSTATE](#mf_capture_metadata_focusstate)                              | UINT32           | 预览               | 此属性包含可采用以下值之一的当前焦点状态。 |
| [MF \_ 捕获 \_ 元数据 \_ SENSORFRAMERATE](#mf_capture_metadata_sensorframerate)                    | UINT64           | 预览               | 此属性包含在捕获预览帧时以赫兹计量的传感器读数率，其中包含32位的分子值和低于32位的分母值。 |
| [MF \_ 捕获 \_ 元数据 \_ FACEROIS](#mf_capture_metadata_facerois)                                  | Blob             | 预览，视频        | 此属性包含驱动程序检测到的人脸矩形信息。 |
| [MF \_ 捕获 \_ 元数据 \_ FACEROITIMESTAMPS](#mf_capture_metadata_faceroitimestamps)                | Blob             | 预览，视频        | 此属性包含 **MF \_ 捕获 \_ 元数据 \_ FACEROIS**中标识的面部 ROIs 的时间戳信息。 |
| [MF \_ 捕获 \_ 元数据 \_ FACEROICHARACTERIZATIONS](#mf_capture_metadata_faceroicharacterizations)  | Blob             | 预览，视频        | 此属性包含 \\ **MF \_ 捕获 \_ 元数据 \_ FACEROIS**中标识的面部 ROIs 的闪烁和或面部表达式状态。 |
| [MF \_ 捕获 \_ 元数据 \_ 公开 \_ 时间](#mf_capture_metadata_exposure_time)                       | UINT64           | 预览，仍        | 此属性包含应用于100毫微秒的曝光时间 |
| [MF \_ 捕获 \_ 元数据 \_ 公开 \_ 补偿](#mf_capture_metadata_exposure_compensation)       | Blob             | 预览，仍        | 此属性包含在捕获照片时应用到驱动程序的步骤中的 EV 补偿步骤标志和 EV 补偿值。 |
| [MF \_ 捕获 \_ 元数据 \_ ISO \_ 速度](#mf_capture_metadata_iso_speed)                               | UINT32           | 预览，仍        | 此属性包含应用于整数的 ISO 速度值。 |
| [MF \_ 捕获 \_ 元数据 \_ 镜头 \_ 位置](#mf_capture_metadata_lens_position)                       | UINT32           | 预览，仍        | 当焦点应用于捕获的照片时，此属性包含逻辑镜头位置。 此值没有特定的单位。 |
| [MF \_ 捕获 \_ 元数据 \_ 场景 \_ 模式](#mf_capture_metadata_scene_mode)                             | UINT64           | 正常                 | 此属性包含作为 **UINT64KSCAMERA_EXTENDEDPROP_SCENEMODE_XXX** 标志应用场景模式。 |
| [MF \_ 捕获 \_ 元数据 \_ 闪存](#mf_capture_metadata_flash)                                        | UINT32 (布尔)  | 预览，仍        | 此属性包含一个包含闪存状态的布尔值。 如果值为1，则表示闪存为 on，值为0时，表示已捕获照片的闪光灯处于关闭状态。 |
| [MF \_ 捕获 \_ 元数据 \_ 闪存 \_](#mf_capture_metadata_flash_power)                           | UINT32           | 正常                 | \[可选： \] 此属性包含应用于0到100之间的百分比值的闪存电源。 |
| [MF \_ 捕获 \_ 元数据 \_ WHITEBALANCE](#mf_capture_metadata_whitebalance)                          | UINT32 (开氏)   | 预览，仍        | 此属性包含应用为 "开氏度" 的值的白平衡。 |
| [MF \_ 捕获 \_ 元数据 \_ ZOOMFACTOR](#mf_capture_metadata_zoomfactor)                              | UINT32 (Q16)      | 正常                 | 此属性包含应用的缩放值，它是可从 GET 调用中的 [**KSPROPERTY_CAMERACONTROL_EXTENDED_ZOOM**](./ksproperty-cameracontrol-extended-zoom.md) 查询的相同值。 该值必须在 Q16 中。 |
| [MF \_ 捕获 \_ 元数据 \_ EXIF](#mf_capture_metadata_exif)                                          | Blob             | 正常                 | \[可选 \] 此属性包含在 " [blob 定义" 部分](#blob-definition)中指定的 EXIF 元数据 |
| [MF \_ 捕获 \_ 元数据 \_ 请求的 \_ 帧 \_ 设置 \_ ID](#mf_capture_metadata_requested_frame_setting_id) | UINT32           | 正常                | \[可选 \] 此属性包含可变照片序列中相应帧的帧 ID。 仅为可变照片序列捕获设置此属性。 |
| [MF \_ 捕获 \_ 元数据 \_ ISO \_ 收益](#mf_capture_metadata_iso_gains)                               | Blob             | 预览               | 此属性包含在捕获预览帧时应用到 senor 的模拟和数字提升。 这是无单位的。 |
| [MF \_ 捕获 \_ 元数据 \_ WHITEBALANCE \_](#mf_capture_metadata_whitebalance_gains)             | Blob             | 预览               | 此属性包含在捕获帧时，按传感器和或 ISP 对 R、G、B 应用的白余额收益 \\ 。 这是一个无单位的。 |
| [MF \_ 捕获 \_ 元数据 \_ 直方图](#mf_capture_metadata_histogram)                                | Blob             | 预览               | 捕获 apreview 帧时，此属性包含直方图。 |
| [MF \_ 捕获 \_ 元数据 \_ 帧 \_ 照明](#mf_capture_metadata_frame_illumination)             | UINT64           | 用于 Hello 的 IR Pin | IR 相机的此属性指定帧是否使用活动 IR 照明，并应与 **FACEAUTH_MODE_ALTERNATIVE_FRAME_ILLUMINATION**结合使用。 |
| 任何自定义 GUID                                                                                   | 任何 variant 类型 |                       | 此属性包含与自定义 GUID 关联的自定义数据 |

## <a name="mf_capture_metadata_focusstate"></a>MF_CAPTURE_METADATA_FOCUSSTATE

MF \_ CAPTURE \_ METADATA \_ FOCUSSTATE 属性包含可采用以下值之一的当前焦点状态。

```cpp
typedef enum
{
    KSCAMERA_EXTENDEDPROP_FOCUSSTATE_UNINITIALIZED = 0,
    KSCAMERA_EXTENDEDPROP_FOCUSSTATE_LOST,
    KSCAMERA_EXTENDEDPROP_FOCUSSTATE_SEARCHING,
    KSCAMERA_EXTENDEDPROP_FOCUSSTATE_FOCUSED,
    KSCAMERA_EXTENDEDPROP_FOCUSSTATE_FAILED,
} KSCAMERA_EXTENDEDPROP_FOCUSSTATE;
```

## <a name="mf_capture_metadata_sensorframerate"></a>MF_CAPTURE_METADATA_SENSORFRAMERATE

MF \_ 捕获 \_ 元数据 \_ SENSORFRAMERATE 属性包含在捕获预览帧时以赫兹计量的传感器读数率，其中包含32位的分子值和低于32位的分母值。

## <a name="mf_capture_metadata_facerois"></a>MF_CAPTURE_METADATA_FACEROIS

MF \_ CAPTURE \_ METADATA \_ FACEROIS 属性包含驱动程序检测到的人脸矩形信息。 默认情况下，驱动程序 \\ MFT0 应在预览流上提供面部信息。 如果驱动程序在其他流上公布功能， \\ 则当应用程序对这些流启用人脸检测时，驱动程序 MFT 必须提供相应流上的面部信息。 在驱动程序上启用视频稳定性后，应提供 "面部信息"，使视频不稳定。 下面的数据结构描述了 MF \_ 捕获 \_ 元数据 FACEROIS 的 blob 格式 \_ 。 占主导面必须是该 blob 中的第一个 FaceRectInfo。

```cpp
typedef struct tagFaceRectInfoBlobHeader
{
    ULONG Size;             // Size of this header + all FaceRectInfo following
    ULONG Count;            // Number of FaceRectInfo’s in the blob
} FaceRectInfoBlobHeader;

typedef struct tagFaceRectInfo
{
    RECT Region;            // Relative coordinates on the frame that face detection is running (Q31 format)
    LONG ConfidenceLevel;   // Confidence level of the region being a face ([0, 100])
} FaceRectInfo;
```

请注意，FaceRectinfoBlobHeader 和 FaceRectInfo 结构仅描述 MF \_ 捕获 \_ 元数据 FACEROIS 特性的 blob 格式 \_ 。 面部 ROIs (KSCAMERA \_ metadata \_ ITEMHEADER + 面部 ROIs metadata 负载) 的元数据项结构是最高的驱动程序，必须是8字节对齐的。

按照设计，如果在启用了人脸检测的情况下配置了流，但所涉及的场景在捕获过程中未包含任何人脸，则驱动程序仍需要将 "虚拟" MF \_ 捕获 \_ 元数据 \_ FACEROIS 属性附加到没有任何人脸信息的每个示例。  ("虚拟" 面部投资回报率属性将*FaceRectInfoBlobHeader*结构的*Count*字段设置为零。 ) 

## <a name="mf_capture_metadata_faceroitimestamps"></a>MF_CAPTURE_METADATA_FACEROITIMESTAMPS

MF \_ 捕获 \_ metadata \_ FACEROITIMESTAMPS 属性包含 MF \_ 捕获 \_ 元数据 FACEROIS 中标识的面部 ROIs 的时间戳信息 \_ 。 对于无法提供面部 ROIs 时间戳的设备，应省略此属性。

下面的数据结构描述了 MF \_ 捕获 \_ 元数据 FACEROITIMESTAMPS 的 blob 格式 \_ 。

```cpp
typedef struct tagMetadataTimeStamps
{
    ULONG Flags;            // Bitwise OR of MF_METADATATIMESTAMPS_XXX flags
    LONGLONG Device;        // QPC time for the sample where the face rect is derived from (in 100ns)
    LONGLONG Presentation;  // PTS for the sample where the face rect is derived from (in 100ns)
} MetadataTimeStamps;
```

对于 "标志" 字段，我们将定义以下位标志来指示哪个时间戳有效。 \_ \_ 如果驱动程序为面部 ROIs 提供时间戳元数据，则 MFT0 必须为 MF METADATATIEMSTAMPS 设备设置标志，并为设备设置相应的 QPC 时间。

\#定义 MF \_ METADATATIMESTAMPS \_ DEVICE 0x00000001

\#定义 MF \_ METADATATIMESTAMPS \_ 表示0x00000002

请注意，MetadataTimeStamps 结构仅描述 MF \_ 捕获 \_ 元数据 FACEROITIMESTAMPS 属性的 blob 格式 \_ 。 Timestamp (KSCAMERA \_ metadata \_ ITEMHEADER + timestamp metadata 负载) 的元数据项结构是最多的驱动程序，必须是8字节对齐的。

## <a name="mf_capture_metadata_faceroicharacterizations"></a>MF_CAPTURE_METADATA_FACEROICHARACTERIZATIONS

MF \_ capture \_ metadata \_ FACEROICHARACTERIZATIONS 属性包含 \\ MF \_ 捕获 \_ 元数据 FACEROIS 中标识的面部 ROIs 的闪烁和或面部表达式状态 \_ 。对于不支持闪烁和 \\ 或面部表达式检测的设备，应省略此属性。

下面的数据结构描述了 MF \_ 捕获 \_ 元数据 FACEROICHARACTERIZATIONS 的 blob 格式 \_ 。

请注意，FaceCharacterizationBlobHeader 和 FaceCharacterization 结构仅描述 MF \_ 捕获 \_ 元数据 FACEROICHARACTERIZATIONS 特性的 blob 格式 \_ 。 面部特征描述 (KSCAMERA \_ metadata \_ ITEMHEADER + 面部特征描述元数据负载) 的元数据项结构是最高的驱动程序，必须是8字节对齐的。

```cpp
typedef struct tagFaceCharacterizationBlobHeader
{
    ULONG Size;     // Size of this header + all FaceCharacterization following
    ULONG Count;    // Number of FaceCharacterization’s in the blob. Must match the number of FaceRectInfo’s in FaceRectInfoBlobHeader
} FaceCharacterizationBlobHeader;

typedef struct tagFaceCharacterization
{
    ULONG BlinkScoreLeft;   // [0, 100]. 0 indicates no blink for the left eye. 100 indicates definite blink for the left eye
    ULONG BlinkScoreRight;  // [0, 100]. 0 indicates no blink for the right eye. 100 indicates definite blink for the right eye
    ULONG FacialExpression; // Any one of the MF_METADATAFACIALEXPRESSION_XXX defined
    ULONG FacialExpressionScore; // [0, 100]. 0 indicates no such facial expression as identified. 100 indicates definite such facial expression as defined
} FaceCharacterization;
```

下面定义了可检测到的可能面部表达式。  

```cpp
#define MF_METADATAFACIALEXPRESSION_SMILE             0x00000001
```

如果 MF \_ 捕获 \_ metadata \_ FACEROICHARACTERIZATIONS 属性显示，则其 blob 中 FaceCharacterization 条目的数量和顺序必须与 MF \_ 捕获元数据的 blob 中的 FaceRectInfo 条目的数量和顺序相匹配 \_ \_ 。每个 FaceCharacterization 条目都表示 \\ 位于同一索引的相应 FaceRectInfo 条目中的表面的闪烁和或面部表达式状态。

下图说明了面部特征描述 blob 和四面的面部 ROIs blob 的布局，其中第一个指示灯不闪烁，第三个为正面闪烁，第三个为正面闪烁，第四个面闪烁 (两个眼睛均) 和微笑。

## <a name="mf_capture_metadata_exposure_time"></a>MF_CAPTURE_METADATA_EXPOSURE_TIME

\_"MF 捕获 \_ 元数据 \_ 公开时间" \_ 属性包含在捕获预览版时应用于传感器的曝光时间， \\ 或捕获的照片帧是 UINT64，以100ns 为单位。

## <a name="mf_capture_metadata_exposure_compensation"></a>MF_CAPTURE_METADATA_EXPOSURE_COMPENSATION

MF \_ 捕获 \_ 元数据 \_ 公开 \_ 补偿属性包含一个 ev 补偿步骤标志和一个 ev 补偿值（在捕获预览和 \\ 或拍摄照片帧时应用于传感器的步骤）。

下面的数据结构描述了 MF \_ 捕获 \_ 元数据 \_ 公开补偿的 blob 格式 \_ 。

```cpp
typedef struct tagCapturedMetadataExposureCompensation
{
    UINT64 Flags;   // KSCAMERA_EXTENDEDPROP_EVCOMP_XXX step flag
    INT32 Value;    // EV Compensation value in units of the step
} CapturedMetadataExposureCompensation;
```

请注意，CapturedMetadataExposureCompensation 结构仅介绍了 MF \_ 捕获 \_ 元数据 \_ 公开 \_ 补偿特性的 blob 格式。 用于 EV 补偿的元数据项结构 (KSCAMERA \_ metadata \_ ITEMHEADER + EV 补偿元数据负载) 是最高为驱动程序，必须为8字节对齐。

## <a name="mf_capture_metadata_iso_speed"></a>MF_CAPTURE_METADATA_ISO_SPEED

MF \_ 捕获 \_ 元数据 \_ ISO \_ 速度属性包含在预览预览 \\ 或拍摄照片帧时应用于传感器的 iso 速度值。 这是无单位的。

## <a name="mf_capture_metadata_iso_gains"></a>MF_CAPTURE_METADATA_ISO_GAINS

\_ \_ \_ 在捕获预览帧后，MF 捕获元数据 ISO \_ 增益属性包含应用于 senor 的模拟和数字提升。
这是无单位的。

下面的数据结构介绍了 MF \_ 捕获 \_ 元数据 \_ ISO 收益的 blob 格式 \_ 。

```cpp
typedef struct tagCapturedMetadataISOGains
{
    FLOAT AnalogGain;
    FLOAT DigitalGain;
} CapturedMetadataISOGains;
```

请注意，CapturedMetadataISOGains struct 仅介绍了 MF \_ 捕获 \_ 元数据 \_ ISO \_ 增益属性的 blob 格式。 ISO 收益的元数据项结构 (KSCAMERA \_ 元数据 \_ ITEMHEADER + ISO 获取元数据负载，) 是最多驱动程序，必须是8字节对齐。

## <a name="mf_capture_metadata_lens_position"></a>MF_CAPTURE_METADATA_LENS_POSITION

\_"MF 捕获 \_ 元数据 \_ 镜头 \_ 位置" 属性包含在捕获预览和或照片帧时的逻辑镜头位置 \\ ，无单位为单位。 此值与可从 KSPROPERTY CAMERACONTROL 中查询的值相同，可 \_ \_ \_ 在 GET 调用中进行扩展。

## <a name="mf_capture_metadata_scene_mode"></a>MF_CAPTURE_METADATA_SCENE_MODE

MF \_ 捕获 \_ 元数据 \_ 场景 \_ 模式属性包含应用于捕获的照片的场景模式，这是一个64位 KSCAMERA \_ EXTENDEDPROP \_ SCENEMODE \_ XXX 标志。

## <a name="mf_capture_metadata_flash"></a>MF_CAPTURE_METADATA_FLASH

在 \_ \_ \_ 捕获预览和或照片帧时，MF 捕获元数据闪存属性包含一个布尔值 \\ ，1表示闪烁，0表示闪烁关闭。

## <a name="mf_capture_metadata_flash_power"></a>MF_CAPTURE_METADATA_FLASH_POWER

MF \_ 捕获 \_ 元数据 \_ 闪存 \_ power 特性包含应用于捕获的照片的闪存电源，该照片是 \[ 0、100范围内的值 \] 。 如果驱动程序不支持闪存的可调整功率，则应该省略此属性。

## <a name="mf_capture_metadata_whitebalance"></a>MF_CAPTURE_METADATA_WHITEBALANCE

MF \_ 捕获 \_ 元数据 \_ WHITEBALANCE 属性包含在捕获预览时应用于传感器的白余额 \\ ，或捕获照片帧后的值（古柯中的值）。

## <a name="mf_capture_metadata_whitebalance_gains"></a>MF_CAPTURE_METADATA_WHITEBALANCE_GAINS

MF \_ 捕获 \_ 元数据 \_ WHITEBALANCE " \_ 增益" 属性包含在捕获帧时，由传感器和或 ISP 应用于 R、G、B 的白余额收益 \\ 。 这是一个无单位的。

下面的数据结构说明了 MF \_ 捕获 \_ 元数据 WHITEBALANCE 的 blob 格式 \_ \_ 。

```cpp
typedef struct tagCapturedMetadataWhiteBalanceGains
{
    FLOAT R;
    FLOAT G;
    FLOAT B;
} CapturedMetadataWhiteBalanceGains;
```

请注意，CapturedMetadataWhiteBalanceGains 结构仅介绍了 MF \_ 捕获 \_ 元数据 \_ WHITEBALANCE \_ 增益属性的 blob 格式。 白平衡收益的元数据项结构 (KSCAMERA \_ 元数据 \_ ITEMHEADER + 白余额获取元数据负载，) 是最多驱动程序，并且必须以8字节对齐。

## <a name="mf_capture_metadata_zoomfactor"></a>MF_CAPTURE_METADATA_ZOOMFACTOR

MF \_ 捕获 \_ 元数据 \_ ZOOMFACTOR 属性包含应用于捕获的照片的缩放值，此值是可从 KSPROPERTY \_ CAMERACONTROL \_ \_ 在 GET 调用中查询的值。
这应该在 Q16 中。

## <a name="mf_capture_metadata_exif"></a>MF_CAPTURE_METADATA_EXIF

MF \_ 捕获 \_ 元数据 \_ exif 包含 3.1 (Blob 定义) 部分中指定的 EXIF 元数据。 MFT0 应 \> \_ \_ 从 \_ \_ 驱动程序提供的 MF 捕获元数据 \_ 帧 \_ RAWSTREAM 缓冲区中提取原始 EXIF 元数据，它被标识为自定义元数据项 (MetadataId = MetadataId 自定义开始) 。
然后，MFT0 应将原始数据转换为 MF \_ 捕获 \_ 元数据 \_ EXIF 属性。

### <a name="blob-definition"></a>Blob 定义

该 blob 应由 EXIF 2.3 和 TIFF 6.0 规范定义的完整 TIFF 标头、第0个 IFD 和 EXIF 子 IFD 组成。 Blob 不应在 TIFF 标头之前包含任何数据。 Blob 不应包含在第0个 IFD 结束后的任何数据。 例如，包括包含缩略图数据的 IFD 是无效的。

以下关系图（从 TIFF 规范复制）说明了预期的内存布局：

![EXIF blob 定义](images/exif-blob-definition.png)

以下要求与 EXIF 和 TIFF 规范一致，但被称为强调：

- 字节顺序应为 little endian ( "II" ) 或大字节序 ( "MM" ) 。
- TIFF 规范) 中 ( "字节偏移量" 的指针应相对于 TIFF 标头的开头。

下面是比 EXIF 和 TIFF 规范更严格的要求：

- 与下一 IFD 的偏移量应为0（即，不指向任何其他 IFDs）。
- TIFF 标头和第0个 IFD 应是连续的，也就是说，以字节4-7 为单位存储的第0个 IFD 的偏移量应为0x8。

### <a name="mandatory-exif-metadata"></a>必需的 EXIF 元数据

以下部分介绍了 MF \_ 捕获 \_ 元数据 exif 中必须包含的 EXIF 元数据 \_ 。

| 名称                  | EXIF 标记  | 描述                                                           |
| --------------------- | --------- | --------------------------------------------------------------------- |
| 方向           | 274       | 在行和列中查看的图像方向。 有关完整说明，请参阅 EXIF 规范 |
| 制造商                  | 271       | 录制设备的制造商                           |
| 型号                 | 272       | 设备的型号名称或型号                      |
| XResolution           | 282       | ImageWidth 方向的每个解析单元的像素数  |
| YResolution           | 283       | ImageLength 方向的每个解析单元的像素数 |
| ResolutionUnit        | 296       | 用于测量 XResolution 和 YResolution 的单位                    |
| 软件              | 305       | 固件的名称和版本                                      |
| ColorSpace            | 40961     | 颜色空间信息，通常为 sRGB                           |
| SubsSecTimeOriginal   | 37521     | 记录与 DateTimeOriginal 标记相关的秒数     |
| SubSecTimeDigitized   | 37522     | 记录与 DateTimeDigitized 标记相关的秒数    |
| ExposureTime          | 33434     | 曝光时间（秒） (精确到0.001 秒)                          |
| FNumber               | 33437     | 用于捕获的 F 编号                                         |
| ISOSpeedRatings       | 34855     | Iso 12322 中定义的 ISO 速度值，基于饱和度             |
| DateTimeOriginal      | 36867     | 原始图像数据的生成日期和时间              |
| DateTimeDIgitized     | 36868     | Theimage 存储为数字数据的日期和时间             |
| 快门 SpeedValue    | 37377     | 在增量系统中的快门速度 (顶点) 单位|
| 口径值        | 37378     | 顶点单元中的镜头口径                                       |
| ExposureBias 值    | 37380     | 顶点单元中的曝光偏差值                                     |
| MeteringMode          | 37383     | AE 计量模式 (参阅 EXIF 规范)                                       |
| LightSource           | 37384     | 光源的类型 (参阅 EXIF 规范)                               |
| 闪烁                 | 37385     | 映像捕获期间的闪存状态                              |
| FocalLength           | 37386     | 镜头的实际焦距                                   |
| ExposureMode          | 41986     | 捕获过程中的曝光模式                                          |
| WhiteBalance          | 41987     | 捕获过程中的白平衡模式                                     |
| DigitalZoomRatio      | 41988     | 图像捕获过程中的数字缩放比率                               |
| FocalLengthIn35mmFilm | 41989     | 35 mm 等效焦距                                         |
| SceneCaptureType      | 41990     | 拍摄的场景的类型                                           |

### <a name="optionaloem-defined-metadata"></a>可选/OEM 定义的元数据

照相机驱动程序可能包含自定义 EXIF 标记形式的任何其他元数据，前提是它符合 EXIF 规范并存储在第0个 TIFF IFD 或 EXIF 子 IFD 中。

### <a name="makernote-requirements-and-binary-layout-expectations"></a>MakerNote 要求和二进制布局预期

照相机驱动程序可能会以 maker 便笺的形式包含制造商专有信息 (tag 37500) 。 "Maker" 附注不得包含任何指向或依赖于 "maker" 注释外数据的指针，包括文件的开头和 TIFF 标题的位置。 此外，它还不得假设 TIFF 标头中指定的文件的字节序。

通常情况下，操作系统不保证元数据 blob 的二进制布局会在写入到输出 JPEG 流时保留。 它仅保证与 EXIF 规范一起写入元数据。 例如，它仅保证将 maker 便笺复制为一个连续的块，并通过正确的 IFD 标记、类型和偏移量进行标识。

### <a name="usage-with-wic-jpeg-encoder"></a>使用 WIC JPEG 编码器

MF \_ 捕获 \_ 元数据 EXIF 的预期用法 \_ 是操作系统提供的 Windows 映像组件 (WIC) JPEG 编码器。 Windows 相机管道使用 Windows WIC JPEG 编码器来使用从 MF 捕获元数据 exif 获取的 EXIF 元数据， \_ \_ 并在 \_ 应用程序未直接从相机捕获 jpeg 时将此数据和图像像素数据 mux 到 jpeg 文件，但将管道配置为捕获到 NV12/YUY2 并通过操作系统进行编码

## <a name="mf_capture_metadata_requested_frame_setting_id"></a>MF_CAPTURE_METADATA_REQUESTED_FRAME_SETTING_ID

MF \_ 捕获 \_ 元 \_ 数据 \_ 请求 \_ 的帧 SETTING_ID 属性包含可变照片序列中相应帧的帧 ID。 仅为可变照片序列捕获设置此属性。

## <a name="mf_capture_metadata_frame_illumination"></a>MF_CAPTURE_METADATA_FRAME_ILLUMINATION

\_ \_ 用于 IR 相机的 MF 捕获元数据 \_ 帧 \_ 照明属性指定帧是否使用活动 IR 照明，并应与 FACEAUTH \_ 模式 \_ 替代 \_ 帧 \_ 照明结合使用。 它仅用于 IR 示例，如果照相机支持 IR 和颜色样本，则不应存在于 RGB 帧中。

如果在捕获帧时捕获到了活动的照明，则值应设置为0xXXXXXXXXXXXXXXX1，并将其设置为0xXXXXXXXXXXXXXXX0。

## <a name="mf_capture_metadata_histogram"></a>MF_CAPTURE_METADATA_HISTOGRAM

\_ \_ \_ 当捕获 apreview 帧时，MF 捕获元数据直方图属性包含直方图。

下面的数据结构描述了 MF \_ 捕获 \_ 元数据直方图的 blob 格式 \_ 。

```cpp
typedef struct tagHistogramGrid
{
    ULONG Width;    // Width of the sensor output that histogram is collected from
    ULONG Height;   // Height of the sensor output that histogram is collected from
    RECT Region;    // Absolute coordinates of the region on the sensor output that the histogram is collected for
} HistogramGrid;

typedef struct tagHistogramBlobHeader
{
    ULONG Size;         // Size of the entire histogram blob in bytes
    ULONG Histograms;   // Number of histograms in the blob. Each histogram is identified by a HistogramHeader
} HistogramBlobHeader;

typedef struct tagHistogramHeader
{
    ULONG Size;         // Size of this header + (HistogramDataHeader + histogram data following) * number of channels available
    ULONG Bins;         // Number of bins in the histogram
    ULONG FourCC;       // Color space that the histogram is collected from
    ULONG ChannelMasks; // Masks of the color channels that the histogram is collected for
    HistogramGrid Grid; // Grid that the histogram is collected from
} HistogramHeader;

typedef struct tagHistogramDataHeader
{
    ULONG Size;         // Size in bytes of this header + histogram data following
    ULONG ChannelMask;  // Mask of the color channel for the histogram data
    ULONG Linear;       // 1, if linear; 0 nonlinear
} HistogramDataHeader;
```

对于 ChannelMasks 字段，我们将定义以下位掩码以指示直方图中的可用通道。

```cpp
#define MF_HISTOGRAM_CHANNEL_Y  0x00000001
#define MF_HISTOGRAM_CHANNEL_R  0x00000002
#define MF_HISTOGRAM_CHANNEL_G  0x00000004
#define MF_HISTOGRAM_CHANNEL_B  0x00000008
#define MF_HISTOGRAM_CHANNEL_Cb 0x00000010
#define MF_HISTOGRAM_CHANNEL_Cr 0x00000020
```

注意：

1. 每个 blob 可以包含从不同区域收集的多个直方图或相同帧的不同颜色空间
2. Blob 中的每个直方图由其自己的 HistogramHeader 标识。
3. 每个直方图均有其自己的区域和传感器输出大小。
   对于全帧直方图，该区域将与 HistogramGrid 中指定的传感器输出大小匹配。
4. 所有可用通道的直方图数据都在一个直方图下进行分组。 每个通道的直方图数据都通过数据上的 HistogramDataHeader 立即标识。ChannelMasks 指示哪些通道包含直方图数据，这是上面定义的受支持的 MF \_ 直方图 \_ 通道 XXX 位掩码的按位 "或" \_ 。 ChannelMask 指示数据所针对的通道，由上面定义的任何一个 MF \_ 直方图 \_ 通道 \_ XXX 位掩码标识。

下图说明了直方图 blob 的布局，其中包含完整帧仅限 Y 的直方图。

直方图数据是一个 ULONG 数组，其中每个条目表示一组按 bin 分类的色调值下的像素数。 数组中的数据应从 "bin 0" 开始，即 "bin"-1，其中 N 是直方图中的储箱数，即 HistogramBlobHeader。

下图说明了直方图数据部分的布局。

下图说明了直方图 blob 的布局，其中包含具有四个通道的全帧 YRGB 直方图。

下图说明了直方图 blob 的布局，该 blob 具有仅包含 Y 个直方图并带有三个通道的 RGB 直方图。

对于阈值，如果 \_ 支持 KSPROPERTY CAMERACONTROL \_ 扩展直方图，则必须至少提供包含 Y 通道的全帧直方图，其中应该是直方图 blob 中的第一个直方图 \_ 。

请注意，HistogramBlobHeader、HistogramHeader、HistogramDataHeader 和直方图数据仅描述 MF \_ 捕获 \_ 元数据直方图属性的 blob 格式 \_ 。 直方图 (KSCAMERA \_ metadata \_ ITEMHEADER + 所有直方图元数据负载) 的元数据项结构都是最新的，并且必须以8字节对齐。

## <a name="histogram-metadata-control"></a>直方图元数据控件

KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ 直方图是用于控制驱动程序生成的直方图元数据的属性 ID。
这只是针对预览 pin 的 pin 级别控制，定义如下：

```cpp
typedef enum {
    …
#if (NTDDI_VERSION >= NTDDI_WIN8)
    KSPROPERTY_CAMERACONTROL_EXTENDED_HISTOGRAM
#endif
} KSPROPERTY_CAMERACONTROL_EXTENDED_PROPERTY;
```

对于 KSCAMERA \_ EXTENDEDPROP \_ 标头，我们将定义以下位标志来控制驱动程序中的直方图元数据。 默认为 OFF。

```cpp
#define KSCAMERA_EXTENDEDPROP_HISTOGRAM_OFF 0x0000000000000000
#define KSCAMERA_EXTENDEDPROP_HISTOGRAM_ON  0x0000000000000001
```

必须先在 KSPROPERTY \_ CAMERACONTROL \_ 扩展元数据控件之前使用此控件 \_ ，以确保分配适当大小的元数据缓冲区。

如果设置为 "直方图" \_ ，驱动程序不应在预览 pin 上传递直方图元数据。 驱动程序不应在其元数据缓冲区大小要求中包含直方图元数据大小。

如果设置为 \_ "直方图 on"，则驱动程序应在预览 pin 上传递直方图元数据。 驱动程序必须在其元数据缓冲区大小要求中包含直方图元数据大小。

如果驱动程序没有生成直方图元数据的功能，驱动程序不应实现此控制。 如果驱动程序支持此控件，则它还必须支持 KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ 元数据控件。

当预览 pin 的 inany 状态高于 KSSTATE 停止状态时，此控件的 SET 调用不起作用 \_ 。 如果预览不处于停止状态，则驱动程序将拒绝收到的设置呼叫，并且返回状态 " \_ 无效 \_ 设备 \_ 状态"。 在 GET 调用中，驱动程序应返回 "标志" 字段中的当前设置。

这是一个同步控件。 没有为此控件定义任何功能。

### <a name="kscamera_extendedprop_header"></a>KSCAMERA_EXTENDEDPROP_HEADER

#### <a name="version"></a>版本

必须为 1。

#### <a name="pinid"></a>PinId

必须是与预览 pin 关联的 Pin ID。

#### <a name="size"></a>大小

必须是 `sizeof(KSCAMERA_EXTENDEDPROP_HEADER) + sizeof(KSCAMERA_EXTENDEDPROP_VALUE)`

#### <a name="result"></a>结果

指示上一次设置操作的错误结果。 如果未执行任何设置操作，则此必须为0。

#### <a name="capability"></a>功能

必须为 0。

#### <a name="flags"></a>Flags

这是一个读/写字段。 这可以是上面定义的任何一个 `KSCAMERA_EXTENDEDPROP_HISTOGRAM_XXX` 标志。

### <a name="kscamera_extendedprop_value"></a>KSCAMERA_EXTENDEDPROP_VALUE

未使用