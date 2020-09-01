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
ms.openlocfilehash: 768355d6f512a74750799b345757f47cbee3c222
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89184331"
---
# <a name="video-control-properties"></a>视频控件属性


[PROPSETID \_ VIDCAP \_ VIDEOCONTROL](./propsetid-vidcap-videocontrol.md)属性集包含与视频硬件的控制和功能相关的属性，如硬件可以捕获的可用帧速率和视频图像的方向。 下表描述了作为 PROPSETID \_ VIDCAP VIDEOCONTROL 属性集的一部分的属性 \_ 。

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videocontrol-caps" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOCONTROL_CAPS&lt;/strong&gt;](./ksproperty-videocontrol-caps.md)"><strong>KSPROPERTY_VIDEOCONTROL_CAPS</strong></a></p></td>
<td><p>返回有关视频流功能的信息，如图像方向和从流中触发视频帧。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videocontrol-actual-frame-rate" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOCONTROL_ACTUAL_FRAME_RATE&lt;/strong&gt;](./ksproperty-videocontrol-actual-frame-rate.md)"><strong>KSPROPERTY_VIDEOCONTROL_ACTUAL_FRAME_RATE</strong></a></p></td>
<td><p>返回硬件正在流式传输特定 pin 的视频的实际帧速率。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videocontrol-frame-rates" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOCONTROL_FRAME_RATES&lt;/strong&gt;](./ksproperty-videocontrol-frame-rates.md)"><strong>KSPROPERTY_VIDEOCONTROL_FRAME_RATES</strong></a></p></td>
<td><p>返回设备可用于传输视频的可用帧速率的数目。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videocontrol-mode" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOCONTROL_MODE&lt;/strong&gt;](./ksproperty-videocontrol-mode.md)"><strong>KSPROPERTY_VIDEOCONTROL_MODE</strong></a></p></td>
<td><p>控制视频流的模式，例如图像翻转和触发从流中获取视频帧。</p></td>
</tr>
</tbody>
</table>

 

 

