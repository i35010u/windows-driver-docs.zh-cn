---
title: 视频解码器属性
description: 视频解码器属性
keywords:
- 视频解码器属性 WDK 视频捕获
- 解码器属性 WDK 视频捕获
- PROPSETID_VIDCAP_VIDEODECODER
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e03f2aa1a64a264d6394b056a2e0bb2763db17ec
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96781999"
---
# <a name="video-decoder-properties"></a>视频解码器属性


[PROPSETID \_ VIDCAP \_ VIDEODECODER](./propsetid-vidcap-videodecoder.md)属性集包含与模拟视频解码器设备操作相关的属性，例如传输标准和计时信号。 下表描述了作为 PROPSETID \_ VIDCAP VIDEODECODER 属性集的一部分的属性 \_ 。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>PROPSETID_VIDCAP_VIDEODECODER KS 属性</th>
<th>属性说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/stream/ksproperty-videodecoder-caps" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEODECODER_CAPS&lt;/strong&gt;](./ksproperty-videodecoder-caps.md)"><strong>KSPROPERTY_VIDEODECODER_CAPS</strong></a></p></td>
<td><p>返回有关视频解码器设备功能的信息，如信号标准 (NTSC、PAL、SECAM) 和结算时间。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/stream/ksproperty-videodecoder-standard" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEODECODER_STANDARD&lt;/strong&gt;](./ksproperty-videodecoder-standard.md)"><strong>KSPROPERTY_VIDEODECODER_STANDARD</strong></a></p></td>
<td><p>控制当前的模拟视频标准。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/stream/ksproperty-videodecoder-status" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEODECODER_STATUS&lt;/strong&gt;](./ksproperty-videodecoder-status.md)"><strong>KSPROPERTY_VIDEODECODER_STATUS</strong></a></p></td>
<td><p>返回视频解码设备的状态，例如视频信号中的行数，以及信号是否锁定。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/stream/ksproperty-videodecoder-output-enable" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEODECODER_OUTPUT_ENABLE&lt;/strong&gt;](./ksproperty-videodecoder-output-enable.md)"><strong>KSPROPERTY_VIDEODECODER_OUTPUT_ENABLE</strong></a></p></td>
<td><p>控制视频解码器的三状态输出。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/stream/ksproperty-videodecoder-vcr-timing" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEODECODER_VCR_TIMING&lt;/strong&gt;](./ksproperty-videodecoder-vcr-timing.md)"><strong>KSPROPERTY_VIDEODECODER_VCR_TIMING</strong></a></p></td>
<td><p>控制视频解码器是使用 VCR 计时还是使用广播计时。</p></td>
</tr>
</tbody>
</table>

 

