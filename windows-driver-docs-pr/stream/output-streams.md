---
title: 输出流
description: 输出流
ms.assetid: 91be637c-f195-4713-bfb0-b41c0346e390
keywords:
- 输出流 WDK DVD 解码器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5c6a6545857cceb4b747d30b19fef5ab2d55a60d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72823507"
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
<th>属性</th>
<th>Value</th>
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

 

内核模式接口提供对视频端口扩展（VPE）设置的控制。 有关详细信息，请参阅[VideoPort 扩展背景](https://docs.microsoft.com/windows-hardware/drivers/display/video-port-extensions-background)。

下表描述了 Dvd 使用的隐藏式字幕（CC）输出流媒体类型：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>属性</th>
<th>Value</th>
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

 

必须在[**KSDATAFORMAT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksdataformat)结构的**SampleSize**成员中指定帧大小200（十进制）。 有关详细信息，请参阅[隐藏式字幕流](closed-captioning-streams.md)。

 

 




