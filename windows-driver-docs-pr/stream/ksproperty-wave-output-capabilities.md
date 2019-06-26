---
title: KSPROPERTY\_批\_输出\_功能
description: KSPROPERTY\_批\_输出\_功能属性返回波形设备的 wave 输出功能。
ms.assetid: 9e5e8ed1-0d08-45b7-b683-df7ce4424c26
keywords:
- KSPROPERTY_WAVE_OUTPUT_CAPABILITIES 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_WAVE_OUTPUT_CAPABILITIES
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b3310c81f8498d7f8331a918e6949c3561055609
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386278"
---
# <a name="kspropertywaveoutputcapabilities"></a>KSPROPERTY\_批\_输出\_功能


KSPROPERTY\_批\_输出\_功能属性返回波形设备的 wave 输出功能。

## <span id="ddk_ksproperty_wave_output_capabilities_ks"></span><span id="DDK_KSPROPERTY_WAVE_OUTPUT_CAPABILITIES_KS"></span>


### <a name="usage-summary-table"></a>使用率摘要表

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
<th>Get</th>
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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-kswave_output_capabilities" data-raw-source="[&lt;strong&gt;KSWAVE_OUTPUT_CAPABILITIES&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-kswave_output_capabilities)"><strong>KSWAVE_OUTPUT_CAPABILITIES</strong></a></p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 是 KSWAVE\_输出\_描述波形设备，其中包括音频通道、 每样本位数范围的范围的最大数目的输出功能的功能结构采样频率，总并处于活动状态的连接数。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Ksmedia.h （包括 Ksmedia.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)

[**KSWAVE\_输出\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-kswave_output_capabilities)

 

 






