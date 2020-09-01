---
title: 输出流
description: 输出流
ms.assetid: 91be637c-f195-4713-bfb0-b41c0346e390
keywords:
- 输出流 WDK DVD 解码器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 60e1464df559a35005406527c6d7ea25bba35870
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89190385"
---
# <a name="output-streams"></a>输出流





下表描述了 Dvd 使用的视频端口输出流媒体类型：

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
<td><p>主要格式 GUID</p></td>
<td><p>KSDATAFORMAT_TYPE_VIDEO</p></td>
</tr>
<tr class="even">
<td><p>次要格式 GUID</p></td>
<td><p>KSDATAFORMAT_SUBTYPE_VPVideo</p></td>
</tr>
<tr class="odd">
<td><p>格式块说明符 GUID</p></td>
<td><p>KSDATAFORMAT_SPECIFIER_NULL</p>
<div>
 
</div>
无格式块。</td>
</tr>
</tbody>
</table>

 

内核模式接口可控制视频端口扩展 (VPE) 设置。 有关详细信息，请参阅 [VideoPort 扩展背景](../display/video-port-extensions-background.md)。

下表描述了 Dvd 使用的隐藏字幕 (CC) 输出流媒体类型：

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
<td><p>主要格式 GUID</p></td>
<td><p>KSDATAFORMAT_TYPE_AUXLine21Data</p></td>
</tr>
<tr class="even">
<td><p>次要格式 GUID</p></td>
<td><p>KSDATAFORMAT_SUBTYPE_Line21_GOPPacket</p></td>
</tr>
<tr class="odd">
<td><p>格式块说明符 GUID</p></td>
<td><p>KSDATAFORMAT_SPECIFIER_NONE</p>
<div>
 
</div>
无格式块。</td>
</tr>
</tbody>
</table>

 

必须指定[**KSDATAFORMAT**](/windows-hardware/drivers/ddi/ks/ns-ks-ksdataformat)结构的**SampleSize**成员中的帧大小 200 (decimal) 。 有关详细信息，请参阅 [隐藏式字幕流](closed-captioning-streams.md)。

 

