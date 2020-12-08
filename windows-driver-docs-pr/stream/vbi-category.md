---
title: VBI 类别
description: VBI 类别
keywords:
- 流类别 WDK 视频捕获，VBI
- VBI WDK 视频捕获
- 垂直消隐间隔 WDK 视频捕获
- PINNAME_VIDEO_VBI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e71aad8f9954aaed1ed9f1fdfd9078f71d9ffb96
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96792089"
---
# <a name="vbi-category"></a>VBI 类别


以下 GUID 对应于垂直消隐间隔 (VBI) 类别：

-   **PINNAME \_ VIDEO \_ VBI**

    VBI 类别输出插针提供 VBI 波形示例流。 此流将传递到下游编解码器，这些编解码器 (CC) 、NABTS、WST、时间码和其他数字数据流提取隐藏式字幕。

指定 **PINNAME \_ VIDEO \_ VBI** pin 时，使用下表中列出的信息。

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
<td><p><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_datarange_video_vbi" data-raw-source="[&lt;strong&gt;KS_DATARANGE_VIDEO_VBI&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_datarange_video_vbi)"><strong>KS_DATARANGE_VIDEO_VBI</strong></a></p></td>
</tr>
<tr class="even">
<td><p><strong>DataFormat 结构</strong></p></td>
<td><p>KS_DATAFORMAT_VIDEO_VBI</p></td>
</tr>
<tr class="odd">
<td><p><strong>MajorFormat GUID</strong></p></td>
<td><p>KS_DATAFORMAT_TYPE_VBI</p></td>
</tr>
<tr class="even">
<td><p><strong>SubFormat GUID</strong></p></td>
<td><p>KSDATAFORMAT_SUBTYPE_RAW8</p></td>
</tr>
<tr class="odd">
<td><p><strong>说明符 GUID</strong></p></td>
<td><p>KSDATAFORMAT_SPECIFIER_VBI</p></td>
</tr>
<tr class="even">
<td><p><strong>扩展的标头大小</strong></p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_vbi_frame_info" data-raw-source="[&lt;strong&gt;KS_VBI_FRAME_INFO&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_vbi_frame_info)"><strong>KS_VBI_FRAME_INFO</strong></a></p></td>
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
<td><p>MEDIATYPE_VBI</p></td>
</tr>
<tr class="even">
<td><p><strong>DirectShow formattype</strong></p></td>
<td><p>FORMAT_VBI</p></td>
</tr>
</tbody>
</table>

 

