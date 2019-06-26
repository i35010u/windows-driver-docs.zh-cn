---
title: 视频处理放大器属性
description: 视频处理放大器属性
ms.assetid: 1adc4fcc-c9a2-41a8-90db-1030ba7c257f
keywords:
- 视频处理放大器属性 WDK 视频捕获
- 放大属性 WDK 视频捕获
- 饱和度 WDK 视频捕获
- 对比度 WDK 视频捕获
- hue WDK 视频捕获
- PROPSETID_VIDCAP_VIDEOPROCAMP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cb01ffe1d21a54b6a3aa86b9771d341df1ae069d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385372"
---
# <a name="video-processing-amplifier-properties"></a>视频处理放大器属性


[PROPSETID\_VIDCAP\_VIDEOPROCAMP](https://docs.microsoft.com/windows-hardware/drivers/stream/propsetid-vidcap-videoprocamp)属性集包含与视频处理放大，例如视频属性，包括色调，对比而言，和饱和度相关的属性。 下表介绍的属性属于 PROPSETID\_VIDCAP\_VIDOPROCAMP 属性集。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>PROPSETID_VIDCAP_VIDEOPROCAMP KS 属性</th>
<th>属性说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videoprocamp-backlight-compensation" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOPROCAMP_BACKLIGHT_COMPENSATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videoprocamp-backlight-compensation)"><strong>KSPROPERTY_VIDEOPROCAMP_BACKLIGHT_COMPENSATION</strong></a></p></td>
<td><p>控制设置的照相机的背景光补偿。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videoprocamp-brightness" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOPROCAMP_BRIGHTNESS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videoprocamp-brightness)"><strong>KSPROPERTY_VIDEOPROCAMP_BRIGHTNESS</strong></a></p></td>
<td><p>控制照相机的亮度。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videoprocamp-colorenable" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOPROCAMP_COLORENABLE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videoprocamp-colorenable)"><strong>KSPROPERTY_VIDEOPROCAMP_COLORENABLE</strong></a></p></td>
<td><p>控制启用照相机的颜色设置。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videoprocamp-contrast" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOPROCAMP_CONTRAST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videoprocamp-contrast)"><strong>KSPROPERTY_VIDEOPROCAMP_CONTRAST</strong></a></p></td>
<td><p>控制设置的照相机的亮度。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videoprocamp-gamma" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOPROCAMP_GAMMA&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videoprocamp-gamma)"><strong>KSPROPERTY_VIDEOPROCAMP_GAMMA</strong></a></p></td>
<td><p>控制设置的照相机的整个范围。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videoprocamp-hue" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOPROCAMP_HUE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videoprocamp-hue)"><strong>KSPROPERTY_VIDEOPROCAMP_HUE</strong></a></p></td>
<td><p>控制设置的照相机的色调。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videoprocamp-saturation" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOPROCAMP_SATURATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videoprocamp-saturation)"><strong>KSPROPERTY_VIDEOPROCAMP_SATURATION</strong></a></p></td>
<td><p>控制设置的照相机的色度。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videoprocamp-sharpness" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOPROCAMP_SHARPNESS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videoprocamp-sharpness)"><strong>KSPROPERTY_VIDEOPROCAMP_SHARPNESS</strong></a></p></td>
<td><p>控制设置的照相机的清晰度。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videoprocamp-whitebalance" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOPROCAMP_WHITEBALANCE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videoprocamp-whitebalance)"><strong>KSPROPERTY_VIDEOPROCAMP_WHITEBALANCE</strong></a></p></td>
<td><p>控制照相机的白平衡设置。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videoprocamp-gain" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOPROCAMP_GAIN&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videoprocamp-gain)"><strong>KSPROPERTY_VIDEOPROCAMP_GAIN</strong></a></p></td>
<td><p>一个照相机的控件获取设置。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videoprocamp-digital-multiplier" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOPROCAMP_DIGITAL_MULTIPLIER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videoprocamp-digital-multiplier)"><strong>KSPROPERTY_VIDEOPROCAMP_DIGITAL_MULTIPLIER</strong></a></p></td>
<td><p>控制照相机的数字的缩放倍数。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videoprocamp-digital-multiplier-limit" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOPROCAMP_DIGITAL_MULTIPLIER_LIMIT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videoprocamp-digital-multiplier-limit)"><strong>KSPROPERTY_VIDEOPROCAMP_DIGITAL_MULTIPLIER_LIMIT</strong></a></p></td>
<td><p>控制照相机的数字缩放的上限。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videoprocamp-whitebalance-component" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOPROCAMP_WHITEBALANCE_COMPONENT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videoprocamp-whitebalance-component)"><strong>KSPROPERTY_VIDEOPROCAMP_WHITEBALANCE_COMPONENT</strong></a></p></td>
<td><p>控制照相机的白平衡设置。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videoprocamp-powerline-frequency" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOPROCAMP_POWERLINE_FREQUENCY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videoprocamp-powerline-frequency)"><strong>KSPROPERTY_VIDEOPROCAMP_POWERLINE_FREQUENCY</strong></a></p></td>
<td><p>控制照相机的操作环境的 powerline 频率。</p></td>
</tr>
</tbody>
</table>

 

 

 




