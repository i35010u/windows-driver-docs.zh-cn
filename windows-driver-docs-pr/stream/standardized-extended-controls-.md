---
title: 扩展的相机控制
description: 扩展控件使用 KSPROPERTY 机制向应用程序公开相机控件。
ms.date: 06/19/2020
ms.localizationpriority: medium
ms.openlocfilehash: da52b6cf5c56920b66f3f0965be9838e7b096c65
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96820447"
---
# <a name="extended-camera-controls"></a>扩展的相机控制

扩展控件使用 **KSPROPERTY** 机制向应用程序公开相机控件。

下面列出了媒体基础) 启用附加 Windows 相机功能 (定义的标准化扩展控件：

- Metadata 

- [焦点优先级](#focus-priority)

- [焦点状态](#focus-state)

- [) 投资 (的扩展区域 ](#extended-region-of-interest-roi)

- [照片确认](#photo-confirmation)

- [照片序列 submode](#photo-sequence-submode)

- [EXIF 和 HW JPEG 编码器](#exif-and-hw-jpeg-encoder)

- [整数 ISO](#integer-iso)

- [高级焦点](#advanced-focus)

- [Flash](#flash)

- [缩放](#zoom)

- [场景模式](#scene-mode)

某些控件作为异步控件向应用程序公开，其他控件作为同步控件公开。

## <a name="synchronous-controls"></a>同步控件

对于这些控件，捕获管道发出 **KSPROPERTY** 相机控制结构，并期望驱动程序以同步方式返回请求。

## <a name="asynchronous-controls"></a>异步控件

对于这些控件，捕获管道会发出 **KSPROPERTY**，使 **KSEVENT** 与该属性相关联，并等待事件发出信号。 驱动程序必须同步完成 **KSPROPERTY** ，并使用它作为触发器来启动异步操作。 异步操作完成后，驱动程序必须向关联的 **KSEVENT** （捕获管道正在等待）发出信号。 捕获管道在收到信号时通知应用程序完成操作。

如果异步控件可以取消，则必须在控件中指定 **KSCAMERA \_ EXTENDEDPROP \_ 标志 \_ CANCELOPERATION** 标志。 如果无法取消控件，则控件的操作不得超过5毫秒。

这些扩展控件是 ksmedia 中定义的以下 KS 属性集的一部分：

```cpp
#define STATIC_KSPROPERTYSETID_ExtendedCameraControl \
     0x1CB79112, 0xC0D2, 0x4213, 0x9C, 0xA6, 0xCD, 0x4F, 0xDB, 0x92, 0x79, 0x72
DEFINE_GUIDSTRUCT("1CB79112-C0D2-4213-9CA6-CD4FDB927972", KSPROPERTYSETID_ExtendedCameraControl);
#define KSPROPERTYSETID_ExtendedCameraControl DEFINE_GUIDNAMED(KSPROPERTYSETID_ExtendedCameraControl);
```

## <a name="metadata"></a>元数据

若要检索元数据， (DevProxy) 的用户模式组件必须查询驱动程序的元数据缓冲要求。 用户模式组件提供此信息后，它将为驱动程序分配适当的元数据缓冲区，以填充并返回到用户模式组件。

客户端使用 [**KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ 属性**](/windows-hardware/drivers/ddi/ksmedia/ne-ksmedia-ksproperty_cameracontrol_extended_property)枚举中定义的 [**KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ 元数据**](./ksproperty-cameracontrol-extended-metadata.md)属性 ID 来查询元数据缓冲区要求，例如所需的元数据大小、内存对齐要求和所需的内存分配类型（用于元数据缓冲区分配）。

用户模式组件从驱动程序获取了元数据缓冲区要求后，它会分配适当大小的元数据缓冲区，并将所需的内存与所需的内存池对齐。 此元数据缓冲区与实际框架缓冲区一起发送到驱动程序以完成，然后在填充时返回给用户模式组件。 对于 multishot 方案，会为每个分配的帧缓冲区分配相应的元数据缓冲区，并将其传递给照相机驱动程序。

[**KSSTREAM \_ 元数据 \_ 信息**](/windows-hardware/drivers/ddi/ks/ns-ks-ksstream_metadata_info)结构与以下标志一起用于将元数据缓冲区发送给驱动程序。

```cpp
#define KSSTREAM_HEADER_OPTIONSF_METADATA           0x00001000
```

一旦缓冲区 (元数据 + 帧) 排队给驱动程序，DevProxy 将发送一个标准 [**KSSTREAM \_ 标头**](/windows-hardware/drivers/ddi/ks/ns-ks-ksstream_header) 结构，后跟一个 [**KS \_ 帧 \_ 信息**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_frame_info) 结构，然后接 **KSSTREAM \_ 元数据 \_ 信息** 结构。 DevProxy 将进一步屏蔽 **KSSTREAM \_ 标头。** 在将缓冲区向下传递到驱动程序之前，OptionFlags 具有 **KSSTREAM \_ 标头 \_ OPTIONSF \_ 元数据** 。

如果该驱动程序不支持元数据，或者未实现 **KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ 元数据** ，则 **KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ 元数据** 属性控件将失败。 在这种情况下，DevProxy 将不会分配元数据缓冲区，并且从 DevProxy 向下传递到驱动程序的负载将不包含 **KSSTREAM \_ 元数据 \_ 信息** 结构。

如果驱动程序支持元数据，且客户端不需要任何元数据，则在将缓冲区发送到驱动程序时，DevProxy 将不会分配元数据缓冲区，也不会传递 **KSSTREAM \_ 元数据 \_ 信息** 。 如果应用程序不希望在给定的 pin 上使用元数据，则此行为会减少不必要的元数据内存分配。

下面的结构描述了要由照相机驱动程序在元数据缓冲区中填充的元数据项的布局。

- [**KSCAMERA \_ MetadataId**](/windows-hardware/drivers/ddi/ksmedia/ne-ksmedia-kscamera_metadataid)

- [**KSCAMERA \_ 元数据 \_ ITEMHEADER**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_metadata_itemheader)

- [**KSCAMERA \_ 元数据 \_ PHOTOCONFIRMATION**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_metadata_photoconfirmation)

下面的列表包含元数据项的布局。 这必须是8字节对齐的。

- [**KSCAMERA \_ 元数据 \_ ITEMHEADER**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_metadata_itemheader)

- 元数据

照片确认元数据由 **MetadataId \_ PhotoConfirmation** 标识。 如果存在，则表示与照片确认框架相关联。 照片确认元数据由 DevProxy 进行分析。

自定义元数据由 **MetadataId \_ 自定义 \_ 开始** 的 **MetadataId** 标识。 自定义元数据项可以包含元数据的 blob，这些元数据可以是针对预览 pin、EXIF 和/或图像 pin 的 OEM 元数据检测到的焦点状态和/或面部。 自定义 blob 的准确格式由实施驱动程序和 MFT0 的 OEM 决定。 MFT0 负责分析自定义 blob 并将每个元数据项附加为按 **MFSampleExtension \_ CaptureMetadata** 特性包分组的属性，该属性可由 MF 捕获管道和/或 WinRT 读取。

以下 IMFAttributes 是在 **mfapi** 中定义的。 它们是 MF 捕获管道和/或 WinRT 所必需的。 请注意，MFT0 不会为照片确认设置任何 IMFAttributes，因为照片确认框架不会流过 DevProxy。

| 属性 (GUID)  | 数据类型 |
|--|--|
| **MF \_ 捕获 \_ 元数据 \_ FOCUSSTATE** | UINT32 |
| **MF \_ 捕获 \_ 元数据 \_ FACEROIS** | Blob |
| **MF \_ 捕获 \_ 元数据 \_ 帧 \_ RAWSTREAM** | IUnknown |

DevProxy 会创建 **MF \_ 捕获 \_ 元数据 \_ 帧 \_ RAWSTREAM** IMFAttributes 并将其附加到 **MFSampleExtension \_ CaptureMetadata** ，其中包含指向与原始元数据缓冲区关联的 IMFMediaBuffer 接口的指针 (**KSSTREAM \_ 元数据 \_ 信息。数据**) 。

当 MFT0 收到 IMFSample 时，它将从 **MF \_ 捕获 \_ 元数据 \_ 帧 \_** 获取原始元数据缓冲区 RAWSTREAM 并分析任何其他自定义元数据项（如焦点状态）并将其转换为上面定义的相应 IMFAttributes，并将它们附加到 **MFSampleExtension \_ CaptureMetadata** 特性包。
以下 IMFAttributes 必须由 MF 管道和任何第三方提供的 MFTs 执行：

| 名称 | 类型 |
|--|--|
| **MFSampleExtension \_ CaptureMetadata** | **IUnknown** (IMFAttributes)  |
| **MFSampleExtension \_ EOS** | **UINT32** (布尔)  |
| **MFSampleExtension \_ PhotoThumbnail** | **IUnknown** (IMFMediaBuffer)  |
| **MFSampleExtension \_ PhotoThumbnailMediaType** | **IUnknown** (IMFMediaType)  |

若要访问原始元数据缓冲区，MFT0 执行以下操作：

1. 从 IMFSample 接口调用 **MFSampleExtension \_ CaptureMetadata** 上的 **GetUnknown** ，以获取特性包的 IMFAttributes 接口。

1. 从上一步获取的 IMFAttributes 接口调用 **MF \_ 捕获 \_ 元数据 \_ 帧 \_ RAWSTREAM** 上的 **GetUnknown** ，以获取 IMFMediaBuffer 接口。

1. 调用锁定以获取与 IMFMediaBuffer 关联的原始元数据缓冲区。

若要将所需的 IMFAttributes 添加到 **MFSampleExtension \_ CaptureMetadata** 特性包，MFT0 执行以下操作：

1. 从 IMFSample 接口调用 **MFSampleExtension \_ CaptureMetadata** 上的 **GetUnknown** ，以获取特性包的 IMFAttributes 接口。

1. 根据上表中指定的 GUID 和数据类型，从上一步获取的 IMFAttributes 接口中调用 **SetUINT32**、 **SetBlob** 或 **SetUnknown** on **MF \_ CAPTURE \_ METADATA \_ XXX** 。

### <a name="mandatory-metadata-attributes"></a>必需的元数据属性

可用的元数据属性的完整列表可在 [捕获统计信息元数据属性](mf-capture-metadata.md)

## <a name="focus-priority"></a>焦点优先级

[**KSPROPERTY \_ CAMERACONTROL \_ EXTENDED \_ FOCUSPRIORITY**](./ksproperty-cameracontrol-extended-focuspriority.md)属性 ID 是与焦点优先级 DDI 关联的唯一控件。

## <a name="focus-state"></a>焦点状态

[**KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ FOCUSSTATE**](./ksproperty-cameracontrol-extended-focusstate.md)属性 ID 是与焦点状态 DDI 关联的唯一控件。

## <a name="extended-region-of-interest-roi"></a>扩展的兴趣投资回报区域

以下属性 Id 是与 ROI DDI 关联的控件：

- [**KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ 投资回报 \_ CONFIGCAPS**](./ksproperty-cameracontrol-extended-roi-configcaps.md)

- [**KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ 投资回报 \_ ISPCONTROL**](./ksproperty-cameracontrol-extended-roi-ispcontrol.md)

## <a name="photo-confirmation"></a>照片确认

[**KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ PHOTOCONFIRMATION**](./ksproperty-cameracontrol-extended-photoconfirmation.md)属性 ID 是与照片确认 DDI 关联的唯一控件。

## <a name="photo-sequence-submode"></a>照片序列 submode

[**KSPROPERTY \_ CAMERACONTROL \_ EXTENDED \_ PHOTOMODE**](./ksproperty-cameracontrol-extended-photomode.md)属性 ID 是与照片序列 DDI 关联的唯一控件。

## <a name="exif-and-hw-jpeg-encoder"></a>EXIF 和 HW JPEG 编码器

管道不需要处理或弯曲 HW JPEG 编码器的任何 EXIF 数据;因此，EXIF 数据格式由驱动程序、MFT0 和 OEM 硬件 JPEG 编码器提供。 Oem 合作伙伴可以为 EXIF 属性定义任何自定义属性 GUID 和变体类型，并将其附加到 **MFSampleExtension \_ CaptureMetaData** 属性包，供 OEM 组件使用。 如果有 HW 编码器，管道照片接收器组件将加载 HW JPEG 编码器，并使用 [IPropertyBag2：： Write](/previous-versions/windows/internet-explorer/ie-developer/platform-apis/aa768195(v=vs.85))方法将 **MFSampleExtension \_ CaptureMetaData** 属性包中包含的 exif 数据设置为 exif 编码器选项。

编码器选项属性包包含指定可用编码选项属性的 PROPBAG2 结构的数组。 设置到 HW JPEG 编码器的 EXIF 编码器选项由编码器选项属性包中的以下属性标识：

| 属性名称 | VARTYPE | “值” | 适用的编解码器 |
|--|--|--|--|
| **SampleMetaData** | **VT \_ 未知** | 指向 **MFSampleExtension \_ CaptureMetaData** 特性包的 IMFAttributes 接口的指针，该接口包含包含 EXIF 数据的 OEM 子属性。 | JPEG |

**MFSampleExtension \_ CaptureMetaData** 属性包只能包含任何 OEM 定义的 EXIF 子属性，MFT0 和 HW JPEG 编码器都可以读取它来容纳 EXIF 数据。 若要将 EXIF 数据从驱动程序传递到 HW JPEG 编码器，驱动程序和 MFT0 必须执行以下操作：

1. 驱动程序在管道提供的元数据缓冲区中提供自定义 EXIF 元数据。 当示例返回到 DevProxy 时，此连接将作为 **MF \_ 捕获 \_ 元数据 \_ 帧 \_ RAWSTREAM** IMFAttribute 通过 DevProxy 附加到 **MFSampleExtension \_ CaptureMetadata** 。

1. 当 MFT0 收到 IMFSample 时，它将从 **MF \_ 捕获 \_ 元数据 \_ 帧 \_** 获取原始元数据缓冲区 RAWSTREAM 并分析自定义 EXIF 元数据项，并将其转换为 OEM 定义的 IMFAttribute 并将其附加到 **MFSampleExtension \_ CaptureMetadata** 特性包。

若要将 EXIF 数据从 MFT0 传递到 HW JPEG 编码器，管道照片接收器会执行以下操作：

1. 从 IMFSample 调用 **MFSampleExtension \_ CaptureMetadata** 上的 **GetUnknown** ，以获取 IMFAttributes 接收时属性包的 IMFSample 接口。

1. 调用 [IPropertyBag2：： Write](/previous-versions/windows/internet-explorer/ie-developer/platform-apis/aa768195(v=vs.85)) 将编码器选项属性（由 SampleMetadata 标识）设置为 HW JPEG 编码器。 编码器选项属性包含从上一步获得的 IMFAttributes 接口。 此接口包含所有自定义子属性，包括 OEM EXIF 子属性，以及本主题前面讨论的 **元数据** 部分中的标准化子属性。

若要检索用于进一步处理的 EXIF 数据，HW JPEG 编码器执行以下操作：

1. 调用 **IPropertyBag2：： Read** 以检索由 SampleMetadata 属性名称和 **VT \_ 未知** 类型标识的属性的属性值。 返回后， **punkVal** 将接收 **MFSampleExtension \_ CaptureMetadata** 的 IMFAttributes 接口。

1. 从上一步获取的接口调用 OEM EXIF 子属性上的 **GetBlob** 或 **GetUnknown** ，以根据 OEM EXIF 子属性的 GUID 和数据类型获取 EXIF 数据 blob。

## <a name="thumbnail"></a>缩略图

MFT0 不需要为相机驱动程序生成任何缩略图。 照相机应用程序应生成其自己的缩略图。 可以通过照片确认图像、HW JPEG 编码器或调整大小大小的图像来生成缩略图。 这取决于应用程序开发人员。 为了保持 API 和应用与 Windows 8.1 应用的兼容性，照相机驱动程序不得实现 **KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ PHOTOTHUMBNAIL** 控件。

## <a name="integer-iso"></a>整数 ISO

[**KSPROPERTY \_ CAMERACONTROL \_ EXTENDED \_ iso \_ 高级**](./ksproperty-cameracontrol-extended-iso-advanced.md)属性 ID 是与整数 ISO DDI 关联的唯一控件。

## <a name="advanced-focus"></a>高级焦点

[**KSPROPERTY \_ CAMERACONTROL \_ EXTENDED \_ FOCUSMODE**](./ksproperty-cameracontrol-extended-focusmode.md)属性 ID 是与整数 ISO DDI 关联的唯一控件。

## <a name="flash"></a>Flash

[**KSPROPERTY \_ CAMERACONTROL \_ EXTENDED \_ FLASHMODE**](./ksproperty-cameracontrol-extended-flashmode.md)属性 ID 是与 flash DDI 关联的唯一控件。

## <a name="zoom"></a>Zoom

[**KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ 缩放**](./ksproperty-cameracontrol-extended-zoom.md)属性 ID 是与缩放 DDI 关联的唯一控件。

## <a name="scene-mode"></a>场景模式

[**KSPROPERTY \_ CAMERACONTROL \_ EXTENDED \_ SCENEMODE**](./ksproperty-cameracontrol-extended-scenemode.md)属性 ID 是与场景模式 DDI 关联的唯一控件。
