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
ms.openlocfilehash: d86bca4979673244c4c10305fc96ce3b50abe419
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385378"
---
# <a name="video-control-properties"></a>视频控件属性


[PROPSETID\_VIDCAP\_VIDEOCONTROL](https://docs.microsoft.com/windows-hardware/drivers/stream/propsetid-vidcap-videocontrol)属性集包含控件和功能的视频硬件相关的属性，如可用的帧速率的硬件可以捕获在和当视频图像的方向。 下表介绍的属性属于 PROPSETID\_VIDCAP\_VIDEOCONTROL 属性集。

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videocontrol-caps" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOCONTROL_CAPS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videocontrol-caps)"><strong>KSPROPERTY_VIDEOCONTROL_CAPS</strong></a></p></td>
<td><p>返回有关视频流，如图像方向和触发的视频帧的流中获取的功能信息。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videocontrol-actual-frame-rate" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOCONTROL_ACTUAL_FRAME_RATE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videocontrol-actual-frame-rate)"><strong>KSPROPERTY_VIDEOCONTROL_ACTUAL_FRAME_RATE</strong></a></p></td>
<td><p>返回实际帧速率为其硬件流式处理特定 pin 的视频。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videocontrol-frame-rates" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOCONTROL_FRAME_RATES&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videocontrol-frame-rates)"><strong>KSPROPERTY_VIDEOCONTROL_FRAME_RATES</strong></a></p></td>
<td><p>返回设备可以流式传输的可用帧速率的数字视频，网址。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videocontrol-mode" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOCONTROL_MODE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videocontrol-mode)"><strong>KSPROPERTY_VIDEOCONTROL_MODE</strong></a></p></td>
<td><p>控制视频流，如翻转和触发的视频帧的流中获取图像的模式。</p></td>
</tr>
</tbody>
</table>

 

 

 




