---
title: KSPROPERTY\_BDA\_RF\_调谐器\_频率\_乘数
description: 客户端使用 KSPROPERTY\_BDA\_RF\_调谐器\_频率\_乘数以及 KSPROPERTY\_BDA\_RF\_调谐器\_频率若要控制调谐器节点的频率设置。
ms.assetid: bca395b5-3993-42c0-880d-eb38d3b933bb
keywords:
- KSPROPERTY_BDA_RF_TUNER_FREQUENCY_MULTIPLIER 流式处理媒体设备
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
ms.openlocfilehash: ba9ee46d03e14d844d637e67667c5befdcadc4a4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565732"
---
# <a name="kspropertybdarftunerfrequencymultiplier"></a>KSPROPERTY\_BDA\_RF\_调谐器\_频率\_乘数


客户端使用 KSPROPERTY\_BDA\_RF\_调谐器\_频率\_乘数以及 KSPROPERTY\_BDA\_RF\_调谐器\_频率若要控制调谐器节点的频率设置。

## <span id="ddk_ksproperty_bda_rf_tuner_frequency_multiplier_ks"></span><span id="DDK_KSPROPERTY_BDA_RF_TUNER_FREQUENCY_MULTIPLIER_KS"></span>


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

属性值指定要设置的频率乘数。

如果 KSPROPERTY\_BDA\_RF\_调谐器\_频率\_乘数属性指定倍增 BDA\_频率\_乘数\_不\_组 (− 1) 或 BDA\_频率\_乘数\_不\_定义 (0)，然后 KSPROPERTY\_BDA\_RF\_调谐器\_频率属性千赫 (kHz) 中指定的频率。 此外，如果微型驱动程序的一组处理程序 ([*KStrSetPropertyHandler*](https://msdn.microsoft.com/library/windows/hardware/ff567200)) 的频率的乘数属性未调用，微型驱动程序必须确定，表示提供的频率kHz (1 Hz x 1000) 为单位。 实际上，默认乘数值为 1000年。 有关详细信息，请参阅[BDA 调谐器节点的访问频率属性](https://msdn.microsoft.com/library/windows/hardware/ff554072)。

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


[**KSP\_NODE**](https://msdn.microsoft.com/library/windows/hardware/ff566720)

[**KSPROPERTY\_BDA\_RF\_调谐器\_频率**](ksproperty-bda-rf-tuner-frequency.md)

 

 






