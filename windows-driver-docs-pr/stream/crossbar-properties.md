---
title: 十字形属性
description: 十字形属性
ms.assetid: 41e46d45-90f8-4b0c-ab27-1fec4202b711
keywords:
- 纵横制属性 WDK 视频捕获
- PROPSETID_VIDCAP_CROSSBAR
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f62edd5409102f09098662342eef3c3c99326390
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378371"
---
# <a name="crossbar-properties"></a>十字形属性


[PROPSETID\_VIDCAP\_纵横制](https://docs.microsoft.com/windows-hardware/drivers/stream/propsetid-vidcap-crossbar)属性集包含与数据的从到的路由 （与对应的音频，如果存在） 的视频输入插针输出插针相关的属性。 下表介绍的属性属于 PROPSETID\_VIDCAP\_纵横制属性集。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>PROPSETID_VIDCAP_CROSSBAR KS 属性</th>
<th>属性说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-crossbar-can-route" data-raw-source="[&lt;strong&gt;KSPROPERTY_CROSSBAR_CAN_ROUTE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-crossbar-can-route)"><strong>KSPROPERTY_CROSSBAR_CAN_ROUTE</strong></a></p></td>
<td><p>返回有关是使用特定的路由信息。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-crossbar-caps" data-raw-source="[&lt;strong&gt;KSPROPERTY_CROSSBAR_CAPS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-crossbar-caps)"><strong>KSPROPERTY_CROSSBAR_CAPS</strong></a></p></td>
<td><p>返回的十字条，包括数输入插针和输出插针数的功能。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-crossbar-pininfo" data-raw-source="[&lt;strong&gt;KSPROPERTY_CROSSBAR_PININFO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-crossbar-pininfo)"><strong>KSPROPERTY_CROSSBAR_PININFO</strong></a></p></td>
<td><p>返回 pin 信息，例如方向的数据流中，固定中等 Guid，并将固定类型。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-crossbar-route" data-raw-source="[&lt;strong&gt;KSPROPERTY_CROSSBAR_ROUTE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-crossbar-route)"><strong>KSPROPERTY_CROSSBAR_ROUTE</strong></a></p></td>
<td><p>控制特定路由，其中包括哪些输入插针，若要将路由到哪个输出插针。</p></td>
</tr>
</tbody>
</table>

 

 

 




