---
title: 扩展的相机控制
description: 扩展控件使用 KSPROPERTY 机制向应用程序公开相机控件。
ms.assetid: B480C007-7DCA-4CFB-9169-BE2D0B2D2137
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f4ad1343a95f3f1678168995577e530f8f864930
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837694"
---
# <a name="extended-camera-controls"></a>扩展的相机控制

扩展控件使用**KSPROPERTY**机制向应用程序公开相机控件。

以下标准化扩展控件列表（由媒体基础定义）启用其他 Windows 相机功能：

- [新元](#metadata)
- [焦点优先级](#focus-priority)
- [焦点状态](#focus-state)
- [感兴趣的扩展区域（ROI）](#extended-region-of-interest-roi)
- [照片确认](#photo-confirmation)
- [照片序列 submode](#photo-sequence-submode)
- [EXIF 和 HW JPEG 编码器](#exif-and-hw-jpeg-encoder)
- [整数 ISO](#integer-iso)
- [高级焦点](#advanced-focus)
- [写](#flash)
- [贴近](#zoom)
- [场景模式](#scene-mode)

某些控件作为异步控件向应用程序公开，其他控件作为同步控件公开。

## <a name="synchronous-controls"></a>同步控件

对于这些控件，捕获管道发出**KSPROPERTY**相机控制结构，并期望驱动程序以同步方式返回请求。

## <a name="asynchronous-controls"></a>异步控件

对于这些控件，捕获管道会发出**KSPROPERTY**，使**KSEVENT**与该属性相关联，并等待事件发出信号。 驱动程序必须同步完成**KSPROPERTY** ，并使用它作为触发器来启动异步操作。 异步操作完成后，驱动程序必须向关联的**KSEVENT** （捕获管道正在等待）发出信号。 捕获管道在收到信号时通知应用程序完成操作。

如果异步控件可以取消，则它必须在控件中指定标记**KSCAMERA\_EXTENDEDPROP\_标志\_CANCELOPERATION** 。 如果无法取消控件，则控件的操作不得超过5毫秒。

这些扩展控件是 ksmedia 中定义的以下 KS 属性集的一部分：

```cpp
#define STATIC_KSPROPERTYSETID_ExtendedCameraControl \
     0x1CB79112, 0xC0D2, 0x4213, 0x9C, 0xA6, 0xCD, 0x4F, 0xDB, 0x92, 0x79, 0x72
DEFINE_GUIDSTRUCT("1CB79112-C0D2-4213-9CA6-CD4FDB927972", KSPROPERTYSETID_ExtendedCameraControl);
#define KSPROPERTYSETID_ExtendedCameraControl DEFINE_GUIDNAMED(KSPROPERTYSETID_ExtendedCameraControl);
```

## <a name="metadata"></a>元数据

若要检索元数据，用户模式组件（DevProxy）必须查询驱动程序的元数据缓冲要求。 用户模式组件提供此信息后，它将为驱动程序分配适当的元数据缓冲区，以填充并返回到用户模式组件。

[**KSPROPERTY\_CAMERACONTROL\_** ](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-metadata)在 KSPROPERTY\_CAMERACONTROL 中定义的扩展\_元数据属性 ID。客户端使用[**扩展\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ne-ksmedia-ksproperty_cameracontrol_extended_property)枚举来查询针对元数据缓冲区分配的元数据缓冲区要求，例如所需的元数据大小、内存对齐要求和所需的内存分配类型。

用户模式组件从驱动程序获取了元数据缓冲区要求后，它会分配适当大小的元数据缓冲区，并将所需的内存与所需的内存池对齐。 此元数据缓冲区与实际框架缓冲区一起发送到驱动程序以完成，然后在填充时返回给用户模式组件。 对于 multishot 方案，会为每个分配的帧缓冲区分配相应的元数据缓冲区，并将其传递给照相机驱动程序。

[**KSSTREAM\_元数据\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksstream_metadata_info)结构与以下标志一起用于将元数据缓冲区发送给驱动程序。

```cpp
#define KSSTREAM_HEADER_OPTIONSF_METADATA           0x00001000
```

一旦将缓冲区（元数据 + 帧）排队给驱动程序，DevProxy 就会发送标准的[**KSSTREAM\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksstream_header)结构，后跟一个[**KS\_帧\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_frame_info)结构，后跟**KSSTREAM\_元数据\_信息**结构。 DevProxy 将进一步屏蔽**KSSTREAM\_标头。** 在将缓冲区向下传递到驱动程序之前，OptionFlags 具有**KSSTREAM\_标头\_OPTIONSF\_元数据**。

如果该驱动程序不支持元数据，或者未实现**KSPROPERTY\_CAMERACONTROL\_扩展\_元数据**，则**KSPROPERTY\_CAMERACONTROL\_扩展\_metadata**属性控件将失败。 在这种情况下，DevProxy 将不会分配元数据缓冲区，并且从 DevProxy 向下传递到驱动程序的负载将不包含**KSSTREAM\_元数据\_信息**结构。

如果驱动程序支持元数据，且客户端不需要任何元数据，则在将缓冲区发送到驱动程序时，DevProxy 将不会分配元数据缓冲区，也不会向下传递**KSSTREAM\_元数据\_信息**。 如果应用程序不希望在给定的 pin 上使用元数据，则此行为会减少不必要的元数据内存分配。

下面的结构描述了要由照相机驱动程序在元数据缓冲区中填充的元数据项的布局。

- [**KSCAMERA\_MetadataId**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ne-ksmedia-kscamera_metadataid)
- [**KSCAMERA\_ITEMHEADER\_元数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_metadata_itemheader)
- [**KSCAMERA\_PHOTOCONFIRMATION\_元数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_metadata_photoconfirmation)

下面的列表包含元数据项的布局。 这必须是8字节对齐的。

- [**KSCAMERA\_ITEMHEADER\_元数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_metadata_itemheader)
- 元数据

照片确认元数据由**MetadataId\_PhotoConfirmation**标识。 如果存在，则表示与照片确认框架相关联。 照片确认元数据由 DevProxy 进行分析。

自定义元数据由从**MetadataId 开始\_自定义\_开始**的**MetadataId**标识。 自定义元数据项可以包含元数据的 blob，这些元数据可以是针对预览 pin、EXIF 和/或图像 pin 的 OEM 元数据检测到的焦点状态和/或面部。 自定义 blob 的准确格式由实施驱动程序和 MFT0 的 OEM 决定。 MFT0 负责分析自定义 blob 并将每个元数据项附加为按**MFSampleExtension\_CaptureMetadata**特性包分组的属性，该属性可由 MF 捕获管道和/或 WinRT 读取。

以下 IMFAttributes 是在**mfapi**中定义的。 它们是 MF 捕获管道和/或 WinRT 所必需的。 请注意，MFT0 不会为照片确认设置任何 IMFAttributes，因为照片确认框架不会流过 DevProxy。

| Attribute （GUID）                            | 数据类型 |
|---------------------------------------------|-----------|
| **MF\_捕获\_元数据\_FOCUSSTATE**       | UINT32    |
| **MF\_捕获\_元数据\_FACEROIS**         | Blob      |
| **MF\_捕获\_的元数据\_框架\_RAWSTREAM** | IUnknown  |

**MF\_捕获\_的元数据\_框架\_RAWSTREAM** IMFAttributes 创建并附加到 DevProxy 的**MFSampleExtension\_CaptureMetadata** ，其中包含指向 IMFMediaBuffer 的指针与原始元数据缓冲区关联的接口（**KSSTREAM\_元数据\_信息。数据**）。

当 MFT0 收到 IMFSample 时，它将从 MF 获取原始元数据缓冲区， **\_捕获\_元数据\_帧\_RAWSTREAM**并分析任何其他自定义元数据项（如焦点状态）并将其转换为上面定义的相应 IMFAttributes，并将其附加到**MFSampleExtension\_CaptureMetadata**特性包。
以下 IMFAttributes 必须由 MF 管道和任何第三方提供的 MFTs 执行：

| 名称                                           | 在任务栏的搜索框中键入                          |
|------------------------------------------------|-------------------------------|
| **MFSampleExtension\_CaptureMetadata**         | **IUnknown** （IMFAttributes）  |
| **MFSampleExtension\_EOS**                     | **UINT32** （布尔值）          |
| **MFSampleExtension\_PhotoThumbnail**          | **IUnknown** （IMFMediaBuffer） |
| **MFSampleExtension\_PhotoThumbnailMediaType** | **IUnknown** （IMFMediaType）   |

若要访问原始元数据缓冲区，MFT0 执行以下操作：

1. 从 IMFSample 接口调用**MFSampleExtension\_CaptureMetadata**上的**GetUnknown** ，以获取特性包的 IMFAttributes 接口。
2. 在 MF\_上调用**GetUnknown** ，从上一步获取的 IMFAttributes 接口 **\_元数据\_帧\_RAWSTREAM** ，以获取 IMFMediaBuffer 接口。
3. 调用锁定以获取与 IMFMediaBuffer 关联的原始元数据缓冲区。

若要将所需的 IMFAttributes 添加到**MFSampleExtension\_CaptureMetadata**特性包，MFT0 执行以下操作：

1. 从 IMFSample 接口调用**MFSampleExtension\_CaptureMetadata**上的**GetUnknown** ，以获取特性包的 IMFAttributes 接口。
2. 在 MF 上调用**SetUINT32**、 **SetBlob**或**SetUnknown**\_根据上表中指定的 GUID 和数据类型从上一步获取的 IMFAttributes 接口**捕获\_元数据\_XXX**.

### <a name="mandatory-metadata-attributes"></a>必需的元数据属性

可用的元数据属性的完整列表可在[捕获统计信息元数据属性](mf-capture-metadata.md)

## <a name="focus-priority"></a>焦点优先级

[**KSPROPERTY\_CAMERACONTROL\_扩展\_FOCUSPRIORITY**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-focuspriority)属性 ID 是与焦点优先级 DDI 关联的唯一控件。

## <a name="focus-state"></a>焦点状态

[**KSPROPERTY\_CAMERACONTROL\_扩展\_FOCUSSTATE**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-focusstate)属性 ID 是与焦点状态 DDI 关联的唯一控件。

## <a name="extended-region-of-interest-roi"></a>扩展的兴趣投资回报区域

以下属性 Id 是与 ROI DDI 关联的控件：

- [**KSPROPERTY\_CAMERACONTROL\_扩展\_投资回报\_CONFIGCAPS**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-roi-configcaps)

- [**KSPROPERTY\_CAMERACONTROL\_扩展\_投资回报\_ISPCONTROL**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-roi-ispcontrol)

## <a name="photo-confirmation"></a>照片确认

[**KSPROPERTY\_CAMERACONTROL\_扩展\_PHOTOCONFIRMATION**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-photoconfirmation)属性 ID 是与照片确认 DDI 关联的唯一控件。

## <a name="photo-sequence-submode"></a>照片序列 submode

[**KSPROPERTY\_CAMERACONTROL\_扩展\_PHOTOMODE**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-photomode)属性 ID 是与照片序列 DDI 关联的唯一控件。

## <a name="exif-and-hw-jpeg-encoder"></a>EXIF 和 HW JPEG 编码器

管道不需要处理或弯曲 HW JPEG 编码器的任何 EXIF 数据;因此，EXIF 数据格式由驱动程序、MFT0 和 OEM 硬件 JPEG 编码器提供。 Oem 合作伙伴可以为 EXIF 属性定义任何自定义属性 GUID 和变体类型，并将其附加到**MFSampleExtension\_CaptureMetaData**属性包，供 OEM 组件使用。 如果 HW JPEG 编码器可用，管道照片接收器组件会加载 HW JPEG 编码器，并将 **\_MFSampleExtension**中包含的 exif 数据设置为 exif 编码器选项，使用[IPropertyBag2：： Write](https://go.microsoft.com/fwlink/?LinkId=331589)方法。

编码器选项属性包包含指定可用编码选项属性的 PROPBAG2 结构的数组。 设置到 HW JPEG 编码器的 EXIF 编码器选项由编码器选项属性包中的以下属性标识：

| 属性名      | VARTYPE         | Value                                                                                                                                                       | 适用的编解码器 |
|--------------------|-----------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------|
| **SampleMetaData** | **VT\_未知** | 指向**MFSampleExtension\_CaptureMetaData**特性包（包含包含 EXIF 数据的 OEM 子属性）的 IMFAttributes 接口的指针。 | JPEG              |

**MFSampleExtension\_CaptureMetaData**属性包只能包含任何 OEM 定义的 EXIF 子属性，MFT0 和 HW JPEG 编码器都可以读取它来容纳 EXIF 数据。 若要将 EXIF 数据从驱动程序传递到 HW JPEG 编码器，驱动程序和 MFT0 必须执行以下操作：

1. 驱动程序在管道提供的元数据缓冲区中提供自定义 EXIF 元数据。 此方法附加到**MFSampleExtension\_CaptureMetadata**作为**MF\_捕获\_元数据\_帧\_RAWSTREAM** IMFAttribute，前提是将该示例返回到 DevProxy。

2. 当 MFT0 收到 IMFSample 时，它将从 MF 获取原始元数据缓冲区， **\_捕获\_元数据\_帧\_RAWSTREAM**并分析自定义 EXIF 元数据项，并将其转换为 OEM 定义的 IMFAttribute 并将其附加到**MFSampleExtension\_CaptureMetadata**属性包。

若要将 EXIF 数据从 MFT0 传递到 HW JPEG 编码器，管道照片接收器会执行以下操作：

1. 从 IMFSample 调用**MFSampleExtension\_CaptureMetadata**上的**GetUnknown** ，以获取 IMFAttributes 接收时属性包的 IMFSample 接口。

2. 调用[IPropertyBag2：： Write](https://go.microsoft.com/fwlink/?LinkId=331589)将编码器选项属性（由 SampleMetadata 标识）设置为 HW JPEG 编码器。 编码器选项属性包含从上一步获得的 IMFAttributes 接口。 此接口包含所有自定义子属性，包括 OEM EXIF 子属性，以及本主题前面讨论的**元数据**部分中的标准化子属性。

若要检索用于进一步处理的 EXIF 数据，HW JPEG 编码器执行以下操作：

1. 调用**IPropertyBag2：： Read**以检索由 SampleMetadata 属性名称和 VT 标识的属性的属性值 **\_未知**类型。 返回后， **punkVal**将接收**MFSampleExtension\_CaptureMetadata**的 IMFAttributes 接口。

2. 从上一步获取的接口调用 OEM EXIF 子属性上的**GetBlob**或**GetUnknown** ，以根据 OEM EXIF 子属性的 GUID 和数据类型获取 EXIF 数据 blob。

## <a name="thumbnail"></a>缩略图

MFT0 不需要为相机驱动程序生成任何缩略图。 照相机应用程序应生成其自己的缩略图。 可以通过照片确认图像、HW JPEG 编码器或调整大小大小的图像来生成缩略图。 这取决于应用程序开发人员。 为了保持 API 和应用与 Windows 8.1 应用的兼容性，照相机驱动程序不得实现**KSPROPERTY\_CAMERACONTROL\_扩展\_PHOTOTHUMBNAIL**控件。

## <a name="integer-iso"></a>整数 ISO

[**KSPROPERTY\_CAMERACONTROL\_扩展\_ISO\_高级**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-iso-advanced)属性 ID 是与整数 ISO DDI 关联的唯一控件。

## <a name="advanced-focus"></a>高级焦点

[**KSPROPERTY\_CAMERACONTROL\_扩展\_FOCUSMODE**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-focusmode)属性 ID 是与整数 ISO DDI 关联的唯一控件。

## <a name="flash"></a>Flash

[**KSPROPERTY\_CAMERACONTROL\_扩展\_FLASHMODE**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-flashmode)属性 ID 是与 flash DDI 关联的唯一控件。

## <a name="zoom"></a>缩放

[**KSPROPERTY\_CAMERACONTROL\_扩展\_缩放**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-zoom)属性 ID 是与缩放 DDI 关联的唯一控件。

## <a name="scene-mode"></a>场景模式

[**KSPROPERTY\_CAMERACONTROL\_扩展\_SCENEMODE**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-scenemode)属性 ID 是与场景模式 DDI 关联的唯一控件。
