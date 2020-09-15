---
title: KSPROPERTY \_ VIDEOCONTROL \_ 实际 \_ 帧 \_ 速率
description: "\"KSPROPERTY \\_ VIDEOCONTROL \\_ 实际 \\_ 帧 \\_ 速率\" 属性检索指定 pin 的设备流式传输的帧速率。 此属性是可选的。"
ms.assetid: 1681bb54-bdd8-499d-b544-c0e8b14deaa5
keywords:
- KSPROPERTY_VIDEOCONTROL_ACTUAL_FRAME_RATE 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_VIDEOCONTROL_ACTUAL_FRAME_RATE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: caa3ad52b272236d89d70be99af7ec4761131517
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90102378"
---
# <a name="ksproperty_videocontrol_actual_frame_rate"></a>KSPROPERTY \_ VIDEOCONTROL \_ 实际 \_ 帧 \_ 速率


"KSPROPERTY \_ VIDEOCONTROL \_ 实际 \_ 帧 \_ 速率" 属性检索指定 pin 的设备流式传输的帧速率。 此属性是可选的。

## <span id="ddk_ksproperty_videocontrol_actual_frame_rate_ks"></span><span id="DDK_KSPROPERTY_VIDEOCONTROL_ACTUAL_FRAME_RATE_KS"></span>


### <a name="usage-summary-table"></a>使用情况摘要表

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th>获取</th>
<th>设置</th>
<th>目标</th>
<th>属性描述符类型</th>
<th>属性值类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>是</p></td>
<td><p>否</p></td>
<td><p>筛选器</p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videocontrol_actual_frame_rate_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOCONTROL_ACTUAL_FRAME_RATE_S&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videocontrol_actual_frame_rate_s)"><strong>KSPROPERTY_VIDEOCONTROL_ACTUAL_FRAME_RATE_S</strong></a></p></td>
<td><p>KSPROPERTY_VIDEOCONTROL</p>
<p>_ACTUAL_FRAME_RATE_S</p></td>
</tr>
</tbody>
</table>

 

 (操作数据) 的属性值是一个 KSPROPERTY \_ VIDEOCONTROL \_ 实际 \_ 帧 \_ 速率的 \_ 结构，它指定查询时的实际帧速率信息，如图像 (宽度和高度) 、当前实际帧速率和当前最大可用帧速率。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>标头</p></td>
<td>Ksmedia (包含 Ksmedia) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**KSPROPERTY**](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

[**KSPROPERTY \_ VIDEOCONTROL \_ 实际 \_ 帧 \_ 速率 \_ S**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videocontrol_actual_frame_rate_s)

