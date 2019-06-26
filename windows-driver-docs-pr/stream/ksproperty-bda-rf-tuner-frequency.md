---
title: KSPROPERTY\_BDA\_RF\_调谐器\_频率
description: 客户端使用 KSPROPERTY\_BDA\_RF\_调谐器\_频率以及 KSPROPERTY\_BDA\_RF\_调谐器\_频率\_乘数若要控制调谐器节点的频率设置。
ms.assetid: 0bcecf33-06d5-4b07-8602-da97db5c1306
keywords:
- KSPROPERTY_BDA_RF_TUNER_FREQUENCY 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_RF_TUNER_FREQUENCY
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ad98d3a8ad0d35ff82e63001b260fc4dd372b061
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368849"
---
# <a name="kspropertybdarftunerfrequency"></a>KSPROPERTY\_BDA\_RF\_调谐器\_频率


客户端使用 KSPROPERTY\_BDA\_RF\_调谐器\_频率以及 KSPROPERTY\_BDA\_RF\_调谐器\_频率\_乘数若要控制调谐器节点的频率设置。

## <span id="ddk_ksproperty_bda_rf_tuner_frequency_ks"></span><span id="DDK_KSPROPERTY_BDA_RF_TUNER_FREQUENCY_KS"></span>


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
<td><p>是</p></td>
<td><p>Filter</p></td>
<td><p>KSP_NODE</p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

**NodeId** KSP 成员\_节点指定调谐器节点的标识符。

属性值指定基的频率设置。

指定 KSPROPERTY\_BDA\_RF\_调谐器\_频率属性：

-   BDA\_频率\_不\_设定 (− 1)，表示未设置频率。

-   BDA\_频率\_不\_定义 (0) 指示未定义的频率。

如果 KSPROPERTY\_BDA\_RF\_调谐器\_频率\_乘数属性指定倍增 BDA\_频率\_乘数\_不\_组 (− 1) 或 BDA\_频率\_乘数\_不\_定义 (0)，然后 KSPROPERTY\_BDA\_RF\_调谐器\_频率属性千赫 (kHz) 中指定的频率。 此外，如果微型驱动程序的一组处理程序 ([*KStrSetPropertyHandler*](https://docs.microsoft.com/previous-versions/ff567200(v=vs.85))) 的频率的乘数属性未调用，微型驱动程序必须确定，表示提供的频率kHz (1 Hz x 1000) 为单位。 实际上，默认乘数值为 1000年。 有关详细信息，请参阅[BDA 调谐器节点的访问频率属性](https://docs.microsoft.com/windows-hardware/drivers/stream/accessing-frequency-properties-of-a-bda-tuner-node)。

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
<td>Bdamedia.h （包括 Bdamedia.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**KSP\_NODE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksp_node)

[**KSPROPERTY\_BDA\_RF\_调谐器\_频率\_乘数**](ksproperty-bda-rf-tuner-frequency-multiplier.md)

 

 






