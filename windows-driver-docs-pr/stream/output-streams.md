---
title: 输出流
description: 输出流
ms.assetid: 91be637c-f195-4713-bfb0-b41c0346e390
keywords:
- 输出流的 WDK DVD 解码器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 732f192f3ff95a972cd9ca6941162a64a1f6585c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370395"
---
# <a name="output-streams"></a>输出流





下表介绍了使用 Dvd 的视频端口输出流媒体类型：

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
<td><p>主要格式 GUID</p></td>
<td><p>KSDATAFORMAT_TYPE_VIDEO</p></td>
</tr>
<tr class="even">
<td><p>次要格式 GUID</p></td>
<td><p>KSDATAFORMAT_SUBTYPE_VPVideo</p></td>
</tr>
<tr class="odd">
<td><p>设置格式块说明符 GUID</p></td>
<td><p>KSDATAFORMAT_SPECIFIER_NULL</p>
<div>
 
</div>
任何格式设置块。</td>
</tr>
</tbody>
</table>

 

内核模式接口提供的视频端口扩展 (VPE) 设置的控件。 有关详细信息，请参阅[视频端口扩展后台](https://docs.microsoft.com/windows-hardware/drivers/display/video-port-extensions-background)。

下表介绍了使用 Dvd 的隐藏式字幕 (CC) 输出流媒体类型：

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
<td><p>主要格式 GUID</p></td>
<td><p>KSDATAFORMAT_TYPE_AUXLine21Data</p></td>
</tr>
<tr class="even">
<td><p>次要格式 GUID</p></td>
<td><p>KSDATAFORMAT_SUBTYPE_Line21_GOPPacket</p></td>
</tr>
<tr class="odd">
<td><p>设置格式块说明符 GUID</p></td>
<td><p>KSDATAFORMAT_SPECIFIER_NONE</p>
<div>
 
</div>
任何格式设置块。</td>
</tr>
</tbody>
</table>

 

帧大小为 200 （十进制） 中**SampleSize**的成员[ **KSDATAFORMAT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksdataformat)必须指定结构。 有关详细信息，请参阅[已关闭隐藏字幕流](closed-captioning-streams.md)。

 

 




