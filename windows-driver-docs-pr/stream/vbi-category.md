---
title: VBI 类别
description: VBI 类别
ms.assetid: c33c0427-5162-435a-bb96-a230455a1035
keywords:
- 流类别 WDK 视频捕获 VBI
- VBI WDK 视频捕获
- 消隐 WDK 视频捕获
- PINNAME_VIDEO_VBI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c699c0a90aa83ae2405fc6afff50dbe1fe0a296c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556177"
---
# <a name="vbi-category"></a>VBI 类别


以下 GUID 对应于垂直遮蔽间隔 (VBI) 类别：

-   **PINNAME\_VIDEO\_VBI**

    输出插针，VBI 类别提供 VBI 波形样本的流。 此流将传递到下游提取隐藏字幕 (CC)、 NABTS、 WST、 时间码和其他数字的数据流的编解码器。

指定时**PINNAME\_视频\_VBI**插针，使用下表中列出的信息。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>属性</th>
<th>值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>DataRange 结构</strong></p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567631" data-raw-source="[&lt;strong&gt;KS_DATARANGE_VIDEO_VBI&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567631)"><strong>KS_DATARANGE_VIDEO_VBI</strong></a></p></td>
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
<td><p><strong>扩展标头大小</strong></p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567694" data-raw-source="[&lt;strong&gt;KS_VBI_FRAME_INFO&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567694)"><strong>KS_VBI_FRAME_INFO</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><strong>所需的属性集</strong></p></td>
<td><p>无</p></td>
</tr>
<tr class="even">
<td><p><strong>所需的事件集</strong></p></td>
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

 

 

 




