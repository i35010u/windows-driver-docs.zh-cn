---
title: KSPROPERTY\_BDA\_RF\_调谐器\_频率\_乘数
description: 客户端使用 KSPROPERTY\_BDA\_RF\_调谐器\_频率\_乘数，同时使用 KSPROPERTY\_BDA\_RF\_射频来控制调谐器节点的频率设置。
ms.assetid: bca395b5-3993-42c0-880d-eb38d3b933bb
keywords:
- KSPROPERTY_BDA_RF_TUNER_FREQUENCY_MULTIPLIER 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_RF_TUNER_FREQUENCY_MULTIPLIER
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0103dff1e18d96a9019521d2ae79d0fdfbbaf56d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838082"
---
# <a name="ksproperty_bda_rf_tuner_frequency_multiplier"></a>KSPROPERTY\_BDA\_RF\_调谐器\_频率\_乘数


客户端使用 KSPROPERTY\_BDA\_RF\_调谐器\_频率\_乘数，同时使用 KSPROPERTY\_BDA\_RF\_射频来控制调谐器节点的频率设置。

## <span id="ddk_ksproperty_bda_rf_tuner_frequency_multiplier_ks"></span><span id="DDK_KSPROPERTY_BDA_RF_TUNER_FREQUENCY_MULTIPLIER_KS"></span>


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
<th>“获取”</th>
<th>设置</th>
<th>目标</th>
<th>属性描述符类型</th>
<th>属性值类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>“是”</p></td>
<td><p>“是”</p></td>
<td><p>Filter</p></td>
<td><p>KSP_NODE</p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

KSP\_**节点的节点**标识符指定调谐器节点的标识符。

属性值指定要设置的频率乘数。

如果 KSPROPERTY\_BDA\_RF\_调谐器\_频率\_乘数属性指定的乘数为 BDA\_FREQUENCY\_乘数\_不\_集（−1）或 BDA\_频率\_乘数\_未\_定义（0），则 KSPROPERTY\_BDA\_RF\_调谐器\_FREQUENCY 属性指定千赫（kHz）中的频率。 此外，如果未调用 frequency 乘数属性的微型驱动程序的集处理程序（[*KStrSetPropertyHandler*](https://docs.microsoft.com/previous-versions/ff567200(v=vs.85))），则微型驱动程序必须确定所提供的频率以 KHz （1Hz x 1000）单位表示。 实际上，默认乘数为1000。 有关详细信息，请参阅[访问 BDA 调谐器节点的频率属性](https://docs.microsoft.com/windows-hardware/drivers/stream/accessing-frequency-properties-of-a-bda-tuner-node)。

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
<td>Bdamedia （包括 Bdamedia）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**KSP\_节点**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_node)

[**KSPROPERTY\_BDA\_RF\_调谐器\_频率**](ksproperty-bda-rf-tuner-frequency.md)

 

 






