---
title: 捕获、预览和静态类别
description: 捕获、预览和静态类别
keywords:
- 流类别 WDK 视频捕获、捕获视频流
- 流类别 WDK 视频捕获，预览视频流
- 流类别 WDK 视频捕获、捕获静态图像
- 捕获视频流类别 WDK 视频捕获
- 预览视频流类别 WDK 视频捕获
- 捕获静止映像类别 WDK 视频捕获
- PINNAME_VIDEO_CAPTURE
- NAME_VIDEO_PREVIEW
- PINNAME_VIDEO_STILL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 94c26fdafb909a02a0a7e1602eb69cac42447ca1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839977"
---
# <a name="capture-preview-and-still-category"></a>捕获、预览和静态类别


以下 Guid 对应于捕获视频流、预览视频流和捕获静态图像的类别， (如果硬件) 支持：

-   **PINNAME \_ 视频 \_ 捕获**

    捕获类别输出插针提供压缩或未压缩数字视频流。 此流类别用于将电影写入磁盘、视频会议和图像分析。

-   **PINNAME \_ 视频 \_ 预览**

    预览类别输出插针提供未压缩数字视频流。 使用此流类别可以通过 DirectDraw 直接显示的 RGB 或 YUV 格式查看本地监视器上的视频流。 在资源有限的情况下，捕获微型驱动程序应将预览流 pin 的优先级设置为低于捕获流 pin。

-   **PINNAME \_ 视频 \_**

    静止类别输出插针用于两种模式的相机，它们能够同时生成捕获流和静止图像流 (，这种情况通常比捕获流) 高。 静止图像流包括外部或以编程方式触发图像获取功能的功能。

"捕获"、"预览" 和 "静止流" pin 类别在数据格式和流特征方面几乎完全相同。

**注意**  ：由于很多照相机仅生成一个输出流，因此 Microsoft DirectShow 包含一个智能 t 筛选器，该筛选器将单个流拆分为捕获和预览流。 因此，仅生成一个流的照相机微型驱动程序不应在内部复制其数据流以生成预览流。

 

指定 **PINNAME \_ 视频 \_ 捕获**、 **PINNAME \_ 视频 \_ 预览** 或 **PINNAME \_ video \_ 静止** pin 时，请使用下表中列出的信息。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Attribute</th>
<th>值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>DataRange 结构</strong></p></td>
<td><p>仅<a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_datarange_video" data-raw-source="[&lt;strong&gt;KS_DATARANGE_VIDEO&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_datarange_video)"><strong>KS_DATARANGE_VIDEO</strong></a> (帧) </p>
<p><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_datarange_video2" data-raw-source="[&lt;strong&gt;KS_DATARANGE_VIDEO2&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_datarange_video2)"><strong>KS_DATARANGE_VIDEO2</strong></a> (字段或框架、bob 或编织设置) </p>
<p><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_datarange_mpeg1_video" data-raw-source="[&lt;strong&gt;KS_DATARANGE_MPEG1_VIDEO&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_datarange_mpeg1_video)"><strong>KS_DATARANGE_MPEG1_VIDEO</strong></a></p>
<p><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_datarange_mpeg2_video" data-raw-source="[&lt;strong&gt;KS_DATARANGE_MPEG2_VIDEO&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_datarange_mpeg2_video)"><strong>KS_DATARANGE_MPEG2_VIDEO</strong></a></p></td>
</tr>
<tr class="even">
<td><p><strong>DataFormat 结构</strong></p></td>
<td><p>仅 KS_DATAFORMAT_VIDEO (帧) </p>
<p>KS_DATAFORMAT_VIDEO2 (字段或框架、bob 或编织设置) </p>
<p>MPEG1 的<a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_mpeg1videoinfo" data-raw-source="[&lt;strong&gt;KS_MPEG1VIDEOINFO&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_mpeg1videoinfo)"><strong>KS_MPEG1VIDEOINFO</strong></a> () </p>
<p>MPEG2) <a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_mpegvideoinfo2" data-raw-source="[&lt;strong&gt;KS_MPEGVIDEOINFO2&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_mpegvideoinfo2)"><strong>KS_MPEGVIDEOINFO2</strong></a> (</p></td>
</tr>
<tr class="odd">
<td><p><strong>主要格式 GUID</strong></p></td>
<td><p>KSDATAFORMAT_TYPE_VIDEO</p></td>
</tr>
<tr class="even">
<td><p><strong>子格式 GUID</strong></p></td>
<td><p>RGB16、RGB24、UYVY、JPEG</p></td>
</tr>
<tr class="odd">
<td><p><strong>说明符 GUID</strong></p></td>
<td><p>仅 KSDATAFORMAT_SPECIFIER_VIDEOINFO (帧) </p>
<p>KSDATAFORMAT_SPECIFIER_VIDEOINFO2 (字段或框架) </p></td>
</tr>
<tr class="even">
<td><p><strong>扩展的标头大小</strong></p></td>
<td><p>如果不是 MPEG 格式，则<a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_frame_info" data-raw-source="[&lt;strong&gt;KS_FRAME_INFO&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_frame_info)"><strong>KS_FRAME_INFO</strong></a> 。 如果为 MPEG 格式，则为零。</p></td>
</tr>
<tr class="odd">
<td><p><strong>必需的属性集</strong></p></td>
<td><p><a href="/windows-hardware/drivers/stream/kspropsetid-connection" data-raw-source="[KSPROPSETID_Connection](./kspropsetid-connection.md)">KSPROPSETID_Connection</a></p>
<p><a href="/windows-hardware/drivers/stream/propsetid-vidcap-droppedframes" data-raw-source="[PROPSETID_VIDCAP_DROPPEDFRAMES](./propsetid-vidcap-droppedframes.md)">PROPSETID_VIDCAP_DROPPEDFRAMES</a></p></td>
</tr>
<tr class="even">
<td><p><strong>必需的事件集</strong></p></td>
<td><p>无</p></td>
</tr>
<tr class="odd">
<td><p><strong>DirectShow majortype</strong></p></td>
<td><p>MEDIATYPE_Video</p></td>
</tr>
<tr class="even">
<td><p><strong>DirectShow formattype</strong></p></td>
<td><p>仅 FORMAT_VideoInfo (帧) </p>
<p>FORMAT_VideoInfo2 (字段或框架) </p></td>
</tr>
</tbody>
</table>

 

