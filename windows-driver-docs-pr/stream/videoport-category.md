---
title: 视频端口类别
description: 视频端口类别
ms.assetid: c11a407f-4ff0-4337-b989-e3ec42418ec3
keywords:
- 流类别 WDK 视频捕获，视频端口
- 视频端口类别 WDK 视频捕获
- 视频端口类别 WDK 视频捕获
- PINNAME_VIDEO_VIDEOPORT
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6765c37b0a6172dab192afde45a3e8c66d31d6f5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385365"
---
# <a name="videoport-category"></a>视频端口类别


以下 GUID 对应的视频端口类别：

-   **PINNAME\_VIDEO\_VIDEOPORT**

    视频端口类别插针从模拟视频解码器直接到通过硬件的视频端口连接的 DirectDraw 表面方式传输图像流。

指定时**PINNAME\_视频\_视频端口**插针，使用下表中列出的信息。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>特性</th>
<th>ReplTest1</th>
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
<td><p><strong>子设置的 GUID 格式</strong></p></td>
<td><p>KSDATAFORMAT_SUBTYPE_VPVideo</p></td>
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
<td><p>KSPROPSETID_VPConfig</p></td>
</tr>
<tr class="even">
<td><p><strong>所需的事件集</strong></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/kseventsetid-vpnotify" data-raw-source="[KSEVENTSETID_VPNotify](https://docs.microsoft.com/windows-hardware/drivers/stream/kseventsetid-vpnotify)">KSEVENTSETID_VPNotify</a></p></td>
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

 

 

 




