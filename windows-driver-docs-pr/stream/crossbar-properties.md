---
title: 十字形属性
description: 十字形属性
keywords:
- 横线属性 WDK 视频捕获
- PROPSETID_VIDCAP_CROSSBAR
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a3af6caecb166f0f8a94dadb11ea01440b7b6734
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96811381"
---
# <a name="crossbar-properties"></a>十字形属性


[PROPSETID \_ VIDCAP \_ 纵横](./propsetid-vidcap-crossbar.md)比属性集包含与 (带有相应音频的视频输入插针中的数据进行路由有关的属性（如果存在) 输出插针）。 下表描述作为 PROPSETID \_ VIDCAP 纵横数属性集的一部分的属性 \_ 。

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
<td><p><a href="/windows-hardware/drivers/stream/ksproperty-crossbar-can-route" data-raw-source="[&lt;strong&gt;KSPROPERTY_CROSSBAR_CAN_ROUTE&lt;/strong&gt;](./ksproperty-crossbar-can-route.md)"><strong>KSPROPERTY_CROSSBAR_CAN_ROUTE</strong></a></p></td>
<td><p>返回有关是否可以进行特定路由的信息。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/stream/ksproperty-crossbar-caps" data-raw-source="[&lt;strong&gt;KSPROPERTY_CROSSBAR_CAPS&lt;/strong&gt;](./ksproperty-crossbar-caps.md)"><strong>KSPROPERTY_CROSSBAR_CAPS</strong></a></p></td>
<td><p>返回纵横比的功能，包括输入插针的数量和输出插针的数目。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/stream/ksproperty-crossbar-pininfo" data-raw-source="[&lt;strong&gt;KSPROPERTY_CROSSBAR_PININFO&lt;/strong&gt;](./ksproperty-crossbar-pininfo.md)"><strong>KSPROPERTY_CROSSBAR_PININFO</strong></a></p></td>
<td><p>返回 pin 信息，如数据流的方向、pin 媒体 Guid 和 pin 类型。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/stream/ksproperty-crossbar-route" data-raw-source="[&lt;strong&gt;KSPROPERTY_CROSSBAR_ROUTE&lt;/strong&gt;](./ksproperty-crossbar-route.md)"><strong>KSPROPERTY_CROSSBAR_ROUTE</strong></a></p></td>
<td><p>控制特定的路由，包括要路由到哪些输出插针的输入插针。</p></td>
</tr>
</tbody>
</table>

 

