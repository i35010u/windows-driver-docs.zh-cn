---
title: KSPROPERTY \_ WAVE \_ 输入 \_ 功能
description: "\"KSPROPERTY \\_ wave \\_ 输入 \\_ 功能\" 属性返回波形设备的输入功能。"
ms.assetid: 84ed0f41-52b6-40e0-b334-c336e158cbfc
keywords:
- KSPROPERTY_WAVE_INPUT_CAPABILITIES 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_WAVE_INPUT_CAPABILITIES
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7791aa4aca9f07beb2f9b72459b67fc2247c87bc
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90104458"
---
# <a name="ksproperty_wave_input_capabilities"></a>KSPROPERTY \_ WAVE \_ 输入 \_ 功能


"KSPROPERTY \_ wave \_ 输入 \_ 功能" 属性返回波形设备的输入功能。

## <span id="ddk_ksproperty_wave_input_capabilities_ks"></span><span id="DDK_KSPROPERTY_WAVE_INPUT_CAPABILITIES_KS"></span>


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
<td><p>Pin</p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-kswave_input_capabilities" data-raw-source="[&lt;strong&gt;KSWAVE_INPUT_CAPABILITIES&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-kswave_input_capabilities)"><strong>KSWAVE_INPUT_CAPABILITIES</strong></a></p></td>
</tr>
</tbody>
</table>

 

 (操作数据) 的属性值是一个 KSWAVE \_ 输入 \_ 功能结构，用于描述 wave 设备的输入功能，其中包括音频通道的最大数量、每个采样的位数、采样频率范围以及连接的总数和总数量。

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

[**KSWAVE \_ 输入 \_ 功能**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-kswave_input_capabilities)

