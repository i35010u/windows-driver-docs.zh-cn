---
title: 扩展的相机控制
description: 扩展的控件使用 KSPROPERTY 机制来公开给应用程序的照相机控件。
ms.assetid: B480C007-7DCA-4CFB-9169-BE2D0B2D2137
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 648b53e5828d4af6179feeacc0fba072b42c5be1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377843"
---
# <a name="extended-camera-controls"></a>扩展的相机控制


扩展控件使用**KSPROPERTY**公开给应用程序的照相机控件的机制。

以下列表 （由媒体基础定义） 的标准化扩展控件的内容启用其他 Windows 相机功能：

-   [Metadata](#metadata)
-   [焦点优先级](#focus-priority)
-   [焦点状态](#focus-state)
-   [扩展的兴趣区域 (ROI)](#extended-region-of-interest-roi)
-   [照片确认](#photo-confirmation)
-   [照片序列子模式](#photo-sequence-submode)
-   [照片捕获反馈应用设备设置](#photo-capture-feedback-applied-device-settings)
-   [整数 ISO](#integer-iso)
-   [高级的焦点](#advanced-focus)
-   [Flash](#flash)
-   [Zoom](#zoom)
-   [场景模式](#scene-mode)

某些控件公开为异步控件的应用程序和其他人公开为同步的控件。

-   **同步控件**– 这些控件，捕获管道问题**KSPROPERTY**照相机控制结构和要求以同步方式返回请求的驱动程序。

-   **异步控件**– 这些控件，捕获管道问题**KSPROPERTY**，使**KSEVENT**与该属性，并等待事件收到信号相关联。 该驱动程序必须完成**KSPROPERTY**以同步方式并将其用作触发器来启动异步操作。 在异步操作完成时，该驱动程序必须发出信号关联**KSEVENT**上的捕获管道正在等待。 当它收到信号时，捕获管道通知有关在操作完成的应用程序。

    如果可以取消的异步控件，它必须指定标志**KSCAMERA\_EXTENDEDPROP\_标志\_CANCELOPERATION**控件中。 如果不能取消该控件，该控件的操作不能超过 5 毫秒。

这些扩展控件是设置 ksmedia.h 中定义的以下 KS 属性的一部分：

```cpp
#define STATIC_KSPROPERTYSETID_ExtendedCameraControl \
     0x1CB79112, 0xC0D2, 0x4213, 0x9C, 0xA6, 0xCD, 0x4F, 0xDB, 0x92, 0x79, 0x72
DEFINE_GUIDSTRUCT("1CB79112-C0D2-4213-9CA6-CD4FDB927972", KSPROPERTYSETID_ExtendedCameraControl);
#define KSPROPERTYSETID_ExtendedCameraControl DEFINE_GUIDNAMED(KSPROPERTYSETID_ExtendedCameraControl);
```

## <a name="metadata"></a>元数据


若要检索元数据，用户模式组件 (DevProxy) 必须查询元数据缓冲区要求的驱动程序。 一旦用户模式组件后，此信息，它会分配相应的元数据缓冲区填充并返回给用户模式组件的驱动程序。

[ **KSPROPERTY\_CAMERACONTROL\_扩展\_元数据**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-metadata)中定义的属性 ID [ **KSPROPERTY\_CAMERACONTROL\_扩展\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ne-ksmedia-ksproperty_cameracontrol_extended_property)枚举由元数据缓冲区要求，例如所需的元数据大小，内存对齐要求，客户端查询和所需的针对元数据缓冲区分配内存分配类型。

一旦用户模式组件具有获取元数据缓冲区要求从驱动程序，它会分配具有所需的内存池中的所需的内存对齐方式的相应大小的元数据缓冲区。 此元数据缓冲区，以及实际帧缓冲区中，将发送到该驱动程序以满足，然后返回到用户模式组件时填充。 对于 multishot 方案，相应的元数据缓冲区进行分配和传递到每个帧缓冲区分配的照相机驱动程序。

[ **KSSTREAM\_元数据\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksstream_metadata_info)结构，以及以下标志，用于将元数据缓冲区发送到该驱动程序。

```cpp
#define KSSTREAM_HEADER_OPTIONSF_METADATA           0x00001000
```

一旦缓冲区 （元数据 + 帧） 排队发送至该驱动程序，DevProxy 会发送标准[ **KSSTREAM\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksstream_header)结构后, 跟[ **KS\_帧\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagks_frame_info)结构，并跟**KSSTREAM\_元数据\_信息**结构。 将进一步屏蔽 DevProxy **KSSTREAM\_标头。OptionFlags**与**KSSTREAM\_标头\_OPTIONSF\_元数据**将传递到驱动程序缓冲区之前。

如果该驱动程序不支持元数据，或如果**KSPROPERTY\_CAMERACONTROL\_扩展\_元数据**未实现**KSPROPERTY\_CAMERACONTROL\_扩展\_元数据**属性控件将会失败。 在这种情况下，DevProxy 将不会收集元数据缓冲区并将不包含有效负载传递到驱动程序从 DevProxy **KSSTREAM\_元数据\_信息**结构。

如果该驱动程序支持元数据和客户端不希望任何元数据，DevProxy 将既不分配元数据缓冲区也不将向下传递**KSSTREAM\_元数据\_信息**将缓冲区发送到该驱动程序时。 此行为可以减少不必要的元数据内存分配，如果应用不希望对给定的 pin 的元数据。

以下结构描述要填充的元数据缓冲区中的照相机驱动程序的元数据项的布局。

-   [**KSCAMERA\_MetadataId**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ne-ksmedia-kscamera_metadataid)

-   [**KSCAMERA\_元数据\_ITEMHEADER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_metadata_itemheader)

-   [**KSCAMERA\_元数据\_PHOTOCONFIRMATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_metadata_photoconfirmation)

以下列表包含的元数据项的布局。 这必须是 8 字节对齐。

-   [**KSCAMERA\_元数据\_ITEMHEADER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_metadata_itemheader)

-   元数据

照片确认元数据由**MetadataId\_PhotoConfirmation**。 当存在时，它指示关联预览帧照片确认帧。 照片确认元数据是由 DevProxy 分析得到的。

自定义元数据由**MetadataId** ，从开始**MetadataId\_自定义\_启动**。 自定义元数据项目可以包含一个可以是焦点状态和/或人脸检测到预览针、 EXIF 和/或图像插针的 OEM 元数据的元数据的 blob。 自定义 blob 的确切格式取决于实现该驱动程序的 OEM 和 MFT0。 MFT0 负责分析自定义 blob 并附加每个元数据项，如在下一个属性进行分组**MFSampleExtension\_CaptureMetadata** MF 捕获可读的格式中的属性包管道和/或 WinRT。

在中定义以下 IMFAttributes **mfapi.h**。 MF 捕获管道和/或 WinRT 需要这些。 请注意 MFT0 不会因为照片确认帧不会将流入超出 DevProxy 设置照片确认任何 IMFAttributes。

| 属性 (GUID)                            | 数据类型 |
|---------------------------------------------|-----------|
| **MF\_捕获\_元数据\_FOCUSSTATE**       | UINT32    |
| **MF\_捕获\_元数据\_FACEROIS**         | Blob      |
| **MF\_CAPTURE\_METADATA\_FRAME\_RAWSTREAM** | IUnknown  |

 

**MF\_捕获\_元数据\_帧\_RAWSTREAM**创建并附加到 IMFAttributes **MFSampleExtension\_CaptureMetadata**通过 DevProxy，其中包含指向与原始的元数据缓冲区关联的 IMFMediaBuffer 接口的指针 (**KSSTREAM\_元数据\_信息。数据**)。 当 MFT0 收到 IMFSample 时，它将获取中的原始元数据缓冲区**MF\_捕获\_元数据\_帧\_RAWSTREAM**并分析任何其他自定义元数据的项如焦点状态和转换为其相应 IMFAttributes 上面定义并将它们添加到**MFSampleExtension\_CaptureMetadata**属性包。

若要访问的原始元数据缓冲区，MFT0 执行以下任务：

1.  调用**GetUnknown**上**MFSampleExtension\_CaptureMetadata** IMFSample 接口来获取 IMFAttributes 接口的属性包中。

2.  调用**GetUnknown**上**MF\_捕获\_元数据\_帧\_RAWSTREAM**从上一步骤中获取的 IMFAttributes 接口若要获取 IMFMediaBuffer 接口。

3.  调用锁来获得与 IMFMediaBuffer 关联的原始元数据缓冲区。

若要添加到所需的 IMFAttributes **MFSampleExtension\_CaptureMetadata**属性包，MFT0 执行以下操作：

1.  调用**GetUnknown**上**MFSampleExtension\_CaptureMetadata** IMFSample 接口来获取 IMFAttributes 接口的属性包中。

2.  调用**SetUINT32**， **SetBlob**，或**SetUnknown**上**MF\_捕获\_元数据\_XXX**从基于上表中指定的 GUID 和数据类型上一步骤中获取的 IMFAttributes 接口。

## <a name="focus-priority"></a>焦点优先级


[ **KSPROPERTY\_CAMERACONTROL\_扩展\_FOCUSPRIORITY** ](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-focuspriority)属性 ID 是唯一的焦点优先级 DDI 与相关联的控件。

## <a name="focus-state"></a>焦点状态


[ **KSPROPERTY\_CAMERACONTROL\_扩展\_FOCUSSTATE** ](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-focusstate)属性 ID 是唯一使用 DDI 的焦点状态相关联的控件。

## <a name="extended-region-of-interest-roi"></a>扩展感兴趣区域的投资回报率


下面的属性 Id 是与投资回报率 DDI 相关联的控件：

-   [**KSPROPERTY\_CAMERACONTROL\_EXTENDED\_ROI\_CONFIGCAPS**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-roi-configcaps)

-   [**KSPROPERTY\_CAMERACONTROL\_扩展\_投资回报率\_ISPCONTROL**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-roi-ispcontrol)

## <a name="photo-confirmation"></a>照片确认


[ **KSPROPERTY\_CAMERACONTROL\_扩展\_PHOTOCONFIRMATION** ](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-photoconfirmation)属性 ID 是唯一使用 DDI 的照片确认相关联的控件。

## <a name="photo-sequence-submode"></a>照片序列子模式


[ **KSPROPERTY\_CAMERACONTROL\_扩展\_PHOTOMODE** ](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-photomode)属性 ID 是唯一的控件与照片序列 DDI 相关联。

## <a name="photo-capture-feedback-applied-device-settings"></a>照片捕获反馈应用设备设置


MFT0 分析提供的驱动程序和所需应用的设备设置附加到 IMFAttributes 的元数据缓冲区**MFSampleExtension\_CaptureMetadata**与每个 IMFSample 关联的属性包。 以下 IMFAttributes 必须转移 MF 管道执行和任何第三方提供 Mft:

| 名称                                           | 在任务栏的搜索框中键入                          |
|------------------------------------------------|-------------------------------|
| **MFSampleExtension\_CaptureMetadata**         | **IUnknown** (IMFAttributes)  |
| **MFSampleExtension\_EOS**                     | **UINT32** （布尔值）          |
| **MFSampleExtension\_PhotoThumbnail**          | **IUnknown** (IMFMediaBuffer) |
| **MFSampleExtension\_PhotoThumbnailMediaType** | **IUnknown** (IMFMediaType)   |

 

**必需的元数据属性**

**MFSampleExtension\_CaptureMetaData**是可以具有以下属性的元数据属性包：

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>名称</th>
<th>在任务栏的搜索框中键入</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>MF_CAPTURE_METADATA_REQUESTED_FRAME_SETTING_ID</strong></td>
<td><strong>UINT32</strong></td>
<td>此属性包含变量照片序列中的相应帧的帧 ID。 此属性只能设置为变量照片序列捕获。</td>
</tr>
<tr class="even">
<td><strong>MF_CAPTURE_METADATA_EXPOSURE_TIME</strong></td>
<td><strong>UINT64</strong></td>
<td>此属性包含应用以 100 纳秒的暴露时间。</td>
</tr>
<tr class="odd">
<td><strong>MF_CAPTURE_METADATA_EXPOSURE_COMPENSATION</strong></td>
<td><strong>Blob</strong></td>
<td>此属性包含 EV 补偿步骤标志以及时捕获照片应用到该驱动程序的步骤的单位中的 EV 补偿值。 <a href="https://docs.microsoft.com/windows/desktop/api/mfapi/ns-mfapi-tagcapturedmetadataexposurecompensation" data-raw-source="[&lt;strong&gt;CapturedMetadataExposureCompensation&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/mfapi/ns-mfapi-tagcapturedmetadataexposurecompensation)"> <strong>CapturedMetadataExposureCompensation</strong> </a>数据结构描述仅限此属性的 blob 格式。 EV 补偿的元数据项目结构格式 (<strong>KSCAMERA_METADATA_ITEMHEADER</strong> + EV 补偿元数据有效负载) 驱动程序提供，并且必须是对齐的 8 字节。</td>
</tr>
<tr class="even">
<td><strong>MF_CAPTURE_METADATA_ISO_SPEED</strong></td>
<td><strong>UINT32</strong></td>
<td>此属性包含一个整数作为应用的 ISO 速度值。</td>
</tr>
<tr class="odd">
<td><strong>MF_CAPTURE_METADATA_LENS_POSITION</strong></td>
<td><strong>UINT32</strong></td>
<td>当焦点已应用于捕获的照片时，该属性包含的逻辑可重用功能区位置。 此值不具有特定的单元。</td>
</tr>
<tr class="even">
<td><strong>MF_CAPTURE_METADATA_SCENE_MODE</strong></td>
<td><strong>UINT64</strong></td>
<td>此属性包含作为应用场景模式<strong>UINT64KSCAMERA_EXTENDEDPROP_SCENEMODE_XXX</strong>标志。</td>
</tr>
<tr class="odd">
<td><strong>MF_CAPTURE_METADATA_FLASH</strong></td>
<td><p><strong>UINT32</strong></p>
<p>(Boolean)</p></td>
<td>此属性包含一个布尔值，包含闪存的状态。 值为 1 指定 flash 位于值为 0 指定处于关闭状态的 flash 捕获照片。</td>
</tr>
<tr class="even">
<td><strong>MF_CAPTURE_METADATA_FLASH_POWER</strong></td>
<td><p><strong>UINT32</strong></p></td>
<td>此属性包含 0 和 100 之间的百分比值作为应用的闪存强大。</td>
</tr>
<tr class="odd">
<td><strong>MF_CAPTURE_METADATA_WHITEBALANCE</strong></td>
<td><p><strong>UINT32</strong></p>
<p>(Kelvin)</p></td>
<td>此特性包含在 kelvin 值作为应用白平衡。</td>
</tr>
<tr class="even">
<td><strong>MF_CAPTURE_METADATA_ZOOMFACTOR</strong></td>
<td><p><strong>UINT32</strong></p>
<p>(Q16)</p></td>
<td>此属性包含应用的缩放值，这是相同的值可以从查询<a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-zoom" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_EXTENDED_ZOOM&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-zoom)"> <strong>KSPROPERTY_CAMERACONTROL_EXTENDED_ZOOM</strong> </a> GET 调用中。 值必须为 Q16。</td>
</tr>
<tr class="odd">
<td><strong>MF_CAPTURE_METADATA_FRAME_ILLUMINATION</strong></td>
<td><strong>UINT64</strong></td>
<td><p><strong>MF_CAPTURE_METADATA_FRAME_ILLUMINATION</strong>用于红外线 （ir） 摄像机属性指定是否正在使用 active IR 照明帧，并应结合使用<strong>FACEAUTH_MODE_ALTERNATIVE_FRAME_照明</strong>。 它仅用于红外线 （ir） 示例并不应为 RGB 帧上存在的如果照相机支持红外线 （ir） 和颜色示例。</p>
<p>如果当 active 照明上，并且如果没有照明捕获帧时存在设置为 0xXXXXXXXXXXXXXXX0 捕获帧时，值应设置为 0xXXXXXXXXXXXXXXX1。</p></td>
</tr>
<tr class="even">
<td>任何自定义 GUID</td>
<td>任何变体类型</td>
<td>此属性包含与自定义 GUID 关联的自定义数据。</td>
</tr>
</tbody>
</table>

 

**EXIF 和 HW JPEG 编码器**

不需要处理或 warp 的 HW JPEG 编码器; 任何 EXIF 数据管道因此，EXIF 数据格式提供驱动程序、 MFT0，和 OEM 硬件 JPEG 编码器。 Oem 合作伙伴可以定义任何自定义属性的 GUID 和 EXIF 特性的变体类型并将其附加到**MFSampleExtension\_CaptureMetaData** ，才能将由 OEM 组件使用的属性包。 如果可用的 HW JPEG 编码器，管道照片接收器组件将加载 HW JPEG 编码器，并将设置保存在中的 EXIF 数据**MFSampleExtension\_CaptureMetaData**到作为 EXIF HW JPEG 编码器上的属性包编码器选项使用[IPropertyBag2::Write](https://go.microsoft.com/fwlink/?LinkId=331589)方法。

编码器选项属性包包含由指定可用的编码选项属性 PROPBAG2 结构组成的数组。 设置到 HW JPEG 编码器上的 EXIF 编码器选项标识由编码器选项属性包中的以下属性：

| 属性名      | VARTYPE         | ReplTest1                                                                                                                                                       | 适用的编解码器 |
|--------------------|-----------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------|
| **SampleMetaData** | **VT\_UNKNOWN** | 指向的 IMFAttributes 接口指针**MFSampleExtension\_CaptureMetaData**属性包，包含含有 EXIF 数据的 OEM 子属性。 | JPEG              |

 

**MFSampleExtension\_CaptureMetaData**属性包仅可包含任何 OEM 定义 MFT0 和 HW JPEG 编码器可以读取来保存数据的 EXIF 数据的 EXIF 子属性。 将从驱动程序的 EXIF 数据传递给 HW JPEG 编码器，驱动程序和 MFT0 必须执行以下操作：

1.  该驱动程序提供自定义管道提供的元数据缓冲区中的 EXIF 元数据。 这附加到**MFSampleExtension\_CaptureMetadata**作为**MF\_捕获\_元数据\_帧\_RAWSTREAM**通过 DevProxy 时该示例返回给 DevProxy IMFAttribute。

2.  当 MFT0 收到 IMFSample 时，它将获取中的原始元数据缓冲区**MF\_捕获\_元数据\_帧\_RAWSTREAM**和解析自定义的 EXIF 元数据项，并将为它为 OEM 定义 IMFAttribute 并将其附加到**MFSampleExtension\_CaptureMetadata**属性包。

将 MFT0 的 EXIF 数据传递给 HW JPEG 编码器中，管道照片接收器将执行以下操作：

1.  调用**GetUnknown**上**MFSampleExtension\_CaptureMetadata**从 IMFSample 为收到 IMFSample 时获取 IMFAttributes 接口的属性包。

2.  调用[IPropertyBag2::Write](https://go.microsoft.com/fwlink/?LinkId=331589)设置 SampleMetadata，通过标识到 HW JPEG 编码器的编码器选项属性。 编码器选项属性包含上一步骤中获取的 IMFAttributes 接口。 此接口包含所有自定义子属性，包括 OEM EXIF 子属性和中的标准化的子属性**元数据**本主题前面所述的部分。

若要检索的 EXIF 数据进行进一步处理，HW JPEG 编码器执行以下任务：

1.  调用**IPropertyBag2::Read**来检索通过 SampleMetadata 属性名称标识的属性的属性值和**VT\_未知**类型。 返回时， **VARIANT.punkVal**接收的 IMFAttributes 界面**MFSampleExtension\_CaptureMetadata**。

2.  调用**GetBlob**或**GetUnknown**上 OEM EXIF EXIF 数据 blob 前一步骤中获取的接口中的子属性根据 OEM EXIF 子属性的 GUID 和数据类型。

**缩略图**

MFT0 不需要生成照相机驱动程序的任何缩略图。 相机应用程序应生成自己的缩略图。 无法从照片确认图像 HW JPEG 编码器生成缩略图或调整其大小完整尺寸的图像。 这是取决于应用程序开发人员。 若要保持与 Windows 8.1 应用的 API 和应用程序兼容性，照相机驱动程序必须不实现**KSPROPERTY\_CAMERACONTROL\_扩展\_PHOTOTHUMBNAIL**控件。

## <a name="integer-iso"></a>整数 ISO


[ **KSPROPERTY\_CAMERACONTROL\_扩展\_ISO\_高级**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-iso-advanced)属性 ID 是唯一的整数 ISO DDI 与关联的控件。

## <a name="advanced-focus"></a>高级的焦点


[ **KSPROPERTY\_CAMERACONTROL\_扩展\_FOCUSMODE** ](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-focusmode)属性 ID 是唯一的整数 ISO DDI 与关联的控件。

## <a name="flash"></a>Flash


[ **KSPROPERTY\_CAMERACONTROL\_扩展\_FLASHMODE** ](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-flashmode)属性 ID 是唯一与闪存 DDI 相关联的控件。

## <a name="zoom"></a>Zoom


[ **KSPROPERTY\_CAMERACONTROL\_扩展\_缩放**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-zoom)属性 ID 是唯一使用 DDI 的缩放相关联的控件。

## <a name="scene-mode"></a>场景模式


[ **KSPROPERTY\_CAMERACONTROL\_扩展\_SCENEMODE** ](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-scenemode)属性 ID 是唯一使用 DDI 的场景模式相关联的控件。

 

 




