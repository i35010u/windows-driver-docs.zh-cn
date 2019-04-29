---
title: 视频控件属性
description: 视频控件属性
ms.assetid: 3b39295f-b4fa-4d6a-bad8-f759bda284b1
keywords:
- 视频控件属性 WDK 视频捕获
- 控件属性 WDK 视频捕获
- PROPSETID_VIDCAP_VIDEOCONTROL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5bcf8a47ebf325b6a99e27dbc5a2d83179e64d33
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63355836"
---
# <a name="video-control-properties"></a>视频控件属性


[PROPSETID\_VIDCAP\_VIDEOCONTROL](https://msdn.microsoft.com/library/windows/hardware/ff568120)属性集包含控件和功能的视频硬件相关的属性，如可用的帧速率的硬件可以捕获在和当视频图像的方向。 下表介绍的属性属于 PROPSETID\_VIDCAP\_VIDEOCONTROL 属性集。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>PROPSETID_VIDCAP_VIDEOCONTROL KS 属性</th>
<th>属性说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566035" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOCONTROL_CAPS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566035)"><strong>KSPROPERTY_VIDEOCONTROL_CAPS</strong></a></p></td>
<td><p>返回有关视频流，如图像方向和触发的视频帧的流中获取的功能信息。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566024" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOCONTROL_ACTUAL_FRAME_RATE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566024)"><strong>KSPROPERTY_VIDEOCONTROL_ACTUAL_FRAME_RATE</strong></a></p></td>
<td><p>返回实际帧速率为其硬件流式处理特定 pin 的视频。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566040" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOCONTROL_FRAME_RATES&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566040)"><strong>KSPROPERTY_VIDEOCONTROL_FRAME_RATES</strong></a></p></td>
<td><p>返回设备可以流式传输的可用帧速率的数字视频，网址。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566042" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOCONTROL_MODE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566042)"><strong>KSPROPERTY_VIDEOCONTROL_MODE</strong></a></p></td>
<td><p>控制视频流，如翻转和触发的视频帧的流中获取图像的模式。</p></td>
</tr>
</tbody>
</table>

 

 

 




