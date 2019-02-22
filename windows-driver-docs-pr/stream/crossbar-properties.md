---
title: 纵横制属性
description: 纵横制属性
ms.assetid: 41e46d45-90f8-4b0c-ab27-1fec4202b711
keywords:
- 纵横制属性 WDK 视频捕获
- PROPSETID_VIDCAP_CROSSBAR
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9a1cbf2e50f7127c05801abf08ed14a4d8b2bb4b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546396"
---
# <a name="crossbar-properties"></a>纵横制属性


[PROPSETID\_VIDCAP\_纵横制](https://msdn.microsoft.com/library/windows/hardware/ff567804)属性集包含与数据的从到的路由 （与对应的音频，如果存在） 的视频输入插针输出插针相关的属性。 下表介绍的属性属于 PROPSETID\_VIDCAP\_纵横制属性集。

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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565117" data-raw-source="[&lt;strong&gt;KSPROPERTY_CROSSBAR_CAN_ROUTE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565117)"><strong>KSPROPERTY_CROSSBAR_CAN_ROUTE</strong></a></p></td>
<td><p>返回有关是使用特定的路由信息。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565118" data-raw-source="[&lt;strong&gt;KSPROPERTY_CROSSBAR_CAPS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565118)"><strong>KSPROPERTY_CROSSBAR_CAPS</strong></a></p></td>
<td><p>返回的十字条，包括数输入插针和输出插针数的功能。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565121" data-raw-source="[&lt;strong&gt;KSPROPERTY_CROSSBAR_PININFO&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565121)"><strong>KSPROPERTY_CROSSBAR_PININFO</strong></a></p></td>
<td><p>返回 pin 信息，例如方向的数据流中，固定中等 Guid，并将固定类型。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565126" data-raw-source="[&lt;strong&gt;KSPROPERTY_CROSSBAR_ROUTE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565126)"><strong>KSPROPERTY_CROSSBAR_ROUTE</strong></a></p></td>
<td><p>控制特定路由，其中包括哪些输入插针，若要将路由到哪个输出插针。</p></td>
</tr>
</tbody>
</table>

 

 

 




