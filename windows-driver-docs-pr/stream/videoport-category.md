---
title: 视频端口类别
description: 视频端口类别
keywords:
- 流类别 WDK 视频捕获，videoport
- videoport 类别 WDK 视频捕获
- 视频端口类别 WDK 视频捕获
- PINNAME_VIDEO_VIDEOPORT
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b3c70b8d42b60c6e7f802e9e9f2207a9d3293573
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96808543"
---
# <a name="videoport-category"></a>视频端口类别


以下 GUID 对应于视频端口类别：

-   **PINNAME \_ VIDEO \_ VIDEOPORT**

    Videoport 类别 pin 通过硬件视频端口连接将图像从模拟视频解码器直接传输到 DirectDraw 表面。

指定 **PINNAME \_ VIDEO \_ VIDEOPORT** pin 时，使用下表中列出的信息。

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
<td><p><strong>主要格式 GUID</strong></p></td>
<td><p>KSDATAFORMAT_TYPE_VIDEO</p></td>
</tr>
<tr class="even">
<td><p><strong>子格式 GUID</strong></p></td>
<td><p>KSDATAFORMAT_SUBTYPE_VPVideo</p></td>
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
<td><p>KSPROPSETID_VPConfig</p></td>
</tr>
<tr class="even">
<td><p><strong>必需的事件集</strong></p></td>
<td><p><a href="/windows-hardware/drivers/stream/kseventsetid-vpnotify" data-raw-source="[KSEVENTSETID_VPNotify](./kseventsetid-vpnotify.md)">KSEVENTSETID_VPNotify</a></p></td>
</tr>
<tr class="odd">
<td><p><strong>DirectShow majortype</strong></p></td>
<td><p>Mediatype_Video</p></td>
</tr>
<tr class="even">
<td><p><strong>DirectShow formattype</strong></p></td>
<td><p>无</p></td>
</tr>
</tbody>
</table>

 

