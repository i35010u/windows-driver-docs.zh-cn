---
title: KSPROPERTY \_ 波浪 \_ 平移
description: "\"KSPROPERTY \\_ wave \\_ 平移\" 属性指定波形设备的平移设置。"
ms.assetid: 5ec4dc6d-44cb-4716-9f5b-dd044cd38239
keywords:
- KSPROPERTY_WAVE_PAN 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_WAVE_PAN
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 215718f2271aa6bff356d93f0a5f27b588134c82
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90102370"
---
# <a name="ksproperty_wave_pan"></a>KSPROPERTY \_ 波浪 \_ 平移


"KSPROPERTY \_ wave \_ 平移" 属性指定波形设备的平移设置。

## <span id="ddk_ksproperty_wave_pan_ks"></span><span id="DDK_KSPROPERTY_WAVE_PAN_KS"></span>


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
<td><p>是</p></td>
<td><p>Pin</p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="/previous-versions/ff567249(v=vs.85)" data-raw-source="[&lt;strong&gt;KSWAVE_PAN&lt;/strong&gt;](/previous-versions/ff567249(v=vs.85))"><strong>KSWAVE_PAN</strong></a></p></td>
</tr>
</tbody>
</table>

 

 (操作数据) 的属性值是一个 KSWAVE \_ 平移结构，描述了左平移和右平移级别。

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

## <a name="see-also"></a>另请参阅


[**KSPROPERTY**](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

[**KSWAVE \_ 平移**](/previous-versions/ff567249(v=vs.85))

