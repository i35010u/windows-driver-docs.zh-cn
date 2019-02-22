---
title: 视频端口 VBI 类别
description: 视频端口 VBI 类别
ms.assetid: 99a4d204-45af-4b73-8d31-d745387a38ac
keywords:
- 流类别 WDK 视频捕获，视频端口 VBI
- 视频端口 VBI 类别 WDK 视频捕获
- VBI WDK 视频捕获
- 消隐 WDK 视频捕获
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 087b262ac037b362e7236a954840b42fe23992d1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554248"
---
# <a name="videoport-vbi-category"></a>视频端口 VBI 类别


以下 GUID 对应的视频端口垂直-消隐功能的时间间隔 (VBI) 类别：

-   **PINNAME\_VIDEO\_VIDEOPORT\_VBI**

    视频端口 VBI 类别 pin 将从模拟解码器 VBI 流传输直接到硬件连接 DirectDraw 图面。

指定时**PINNAME\_视频\_视频端口\_VBI**插针，使用下表中列出的信息。

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
<td><p>KSDATARANGE</p></td>
</tr>
<tr class="even">
<td><p><strong>DataFormat 结构</strong></p></td>
<td><p>KSDATAFORMAT</p></td>
</tr>
<tr class="odd">
<td><p><strong>MajorFormat GUID</strong></p></td>
<td><p>KSDATAFORMAT_TYPE_VIDEO</p></td>
</tr>
<tr class="even">
<td><p><strong>子设置的 GUID 格式</strong></p></td>
<td><p>KSDATAFORMAT_SUBTYPE_VPVBIVideo</p></td>
</tr>
<tr class="odd">
<td><p><strong>说明符 GUID</strong></p></td>
<td><p>KSDATAFORMAT_SPECIFIER_NONE</p></td>
</tr>
<tr class="even">
<td><p><strong>扩展标头大小</strong></p></td>
<td><p>0</p></td>
</tr>
<tr class="odd">
<td><p><strong>所需的属性集</strong></p></td>
<td><p>KSPROPSETID_VPVBIConfig</p></td>
</tr>
<tr class="even">
<td><p><strong>所需的事件集</strong></p></td>
<td><p>KSEVENTSETID_VPVBINotify</p></td>
</tr>
<tr class="odd">
<td><p><strong>DirectShow majortype</strong></p></td>
<td><p>MEDIATYPE_Video</p></td>
</tr>
<tr class="even">
<td><p><strong>DirectShow formattype</strong></p></td>
<td><p>无</p></td>
</tr>
</tbody>
</table>

 

 

 




