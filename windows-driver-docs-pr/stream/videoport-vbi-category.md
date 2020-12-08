---
title: 视频端口 VBI 类别
description: 视频端口 VBI 类别
keywords:
- 流类别 WDK 视频捕获，videoport VBI
- videoport VBI
- VBI WDK 视频捕获
- 垂直消隐间隔 WDK 视频捕获
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bd6059dc1fd607db4c4d56946d8491ee45bcc5f7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96806597"
---
# <a name="videoport-vbi-category"></a>视频端口 VBI 类别


以下 GUID 对应于视频端口垂直-消隐间隔 (VBI) 类别：

-   **PINNAME \_ VIDEO \_ VIDEOPORT \_ VBI**

    Videoport VBI 类别 pin 通过硬件连接从模拟解码器直接传输 VBI 流到 DirectDraw 表面。

指定 **PINNAME \_ VIDEO \_ VIDEOPORT \_ VBI** 引脚时，请使用下表中列出的信息。

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
<td><p><strong>子格式 GUID</strong></p></td>
<td><p>KSDATAFORMAT_SUBTYPE_VPVBIVideo</p></td>
</tr>
<tr class="odd">
<td><p><strong>说明符 GUID</strong></p></td>
<td><p>KSDATAFORMAT_SPECIFIER_NONE</p></td>
</tr>
<tr class="even">
<td><p><strong>扩展的标头大小</strong></p></td>
<td><p>0</p></td>
</tr>
<tr class="odd">
<td><p><strong>必需的属性集</strong></p></td>
<td><p>KSPROPSETID_VPVBIConfig</p></td>
</tr>
<tr class="even">
<td><p><strong>必需的事件集</strong></p></td>
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

 

 

 




