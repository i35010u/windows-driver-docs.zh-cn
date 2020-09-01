---
title: 模拟视频类别
description: 模拟视频类别
ms.assetid: 64564c81-b1e1-482b-ae70-59b229a5e86f
keywords:
- 流类别 WDK 视频捕获、模拟视频
- 模拟视频类别 WDK 视频捕获
- PINNAME_VIDEO_ANALOGVIDEOIN
- 模拟音频 WDK 视频捕获
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 90da319b6a2c4ced05cc7a16b266f06670f8ded3
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89186853"
---
# <a name="analog-video-category"></a>模拟视频类别


以下 GUID 对应于分类中的模拟视频：

-   **PINNAME \_ VIDEO \_ ANALOGVIDEOIN**

    分类中的模拟视频表示视频解码器筛选器的模拟视频输入流。

指定 **PINNAME \_ VIDEO \_ ANALOGVIDEOIN**时，请使用下表中列出的信息。

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_datarange_analogvideo" data-raw-source="[&lt;strong&gt;KS_DATARANGE_ANALOGVIDEO&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_datarange_analogvideo)"><strong>KS_DATARANGE_ANALOGVIDEO</strong></a></p></td>
</tr>
<tr class="even">
<td><p><strong>DataFormat 结构</strong></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_datarange_analogvideo" data-raw-source="[&lt;strong&gt;KS_DATARANGE_ANALOGVIDEO&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_datarange_analogvideo)"><strong>KS_DATARANGE_ANALOGVIDEO</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><strong>MajorFormat GUID</strong></p></td>
<td><p>KSDATAFORMAT_TYPE_ANALOGVIDEO</p></td>
</tr>
<tr class="even">
<td><p><strong>子格式 GUID</strong></p></td>
<td><p>KSDATAFORMAT_SUBTYPE_NONE</p></td>
</tr>
<tr class="odd">
<td><p><strong>说明符 GUID</strong></p></td>
<td><p>KSDATAFORMAT_SPECIFIER_ANALOGVIDEO</p></td>
</tr>
<tr class="even">
<td><p><strong>扩展的标头大小</strong></p></td>
<td><p>0</p></td>
</tr>
<tr class="odd">
<td><p><strong>必需的属性集</strong></p></td>
<td><p>无</p></td>
</tr>
<tr class="even">
<td><p><strong>必需的事件集</strong></p></td>
<td><p>无</p></td>
</tr>
<tr class="odd">
<td><p><strong>DirectShow majortype</strong></p></td>
<td><p>MEDIATYPE_AnalogVideo</p></td>
</tr>
<tr class="even">
<td><p><strong>DirectShow formattype</strong></p></td>
<td><p>FORMAT_AnalogVideo</p></td>
</tr>
</tbody>
</table>

 

没有为模拟音频定义的特殊类别，如电视或无线电音频。 为带有模拟音频 pin 的设备指定类别时， **MajorFormat** 成员的值应为 KSDATAFORMAT \_ 类型 \_ ANALOGAUDIO。 **说明符**成员的值应为 KSDATAFORMAT \_ 说明符 \_ none，并且**子类型**成员和格式块应设置为 KSDATAFORMAT \_ 子类型 \_ none。 有关收音机音频的详细信息，请参阅 [带有收音机调谐器的视频捕获设备](video-capture-devices-with-radio-tuners.md)。

尽管模拟视频流实质上是模拟模拟视频解码器的输入，但它同时充当用于优化信息的数据传输。 在每次优化操作开始和结束时，会通过任何干预的纵横制筛选器来调整来自电视调谐器筛选器的数据包。 数据包是一个 [**KS \_ TVTUNER \_ 更改 \_ 信息**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_tvtuner_change_info) 结构，其中包含使用的国家/地区代码、频道、频率和模拟视频标准。

捕获筛选器必须在 VBI 输出流扩展的标头中将此优化数据包传播到下游 VBI 编解码器。

 

