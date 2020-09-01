---
title: KSPROPERTY \_ BDA \_ RF \_ 调谐器 \_ 频率
description: 客户端使用 KSPROPERTY \_ bda \_ rf 射频射频和 \_ \_ KSPROPERTY \_ bda \_ rf \_ 射频 \_ \_ 乘法器来控制调谐器节点的频率设置。
ms.assetid: 0bcecf33-06d5-4b07-8602-da97db5c1306
keywords:
- KSPROPERTY_BDA_RF_TUNER_FREQUENCY 流媒体设备
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
ms.openlocfilehash: 5c42dab6b0c1ea315edb8042e5b63464fd4da8e9
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89186601"
---
# <a name="ksproperty_bda_rf_tuner_frequency"></a>KSPROPERTY \_ BDA \_ RF \_ 调谐器 \_ 频率


客户端使用 KSPROPERTY \_ bda \_ rf 射频射频和 \_ \_ KSPROPERTY \_ bda \_ rf \_ 射频 \_ \_ 乘法器来控制调谐器节点的频率设置。

## <span id="ddk_ksproperty_bda_rf_tuner_frequency_ks"></span><span id="DDK_KSPROPERTY_BDA_RF_TUNER_FREQUENCY_KS"></span>


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
<td><p>筛选器</p></td>
<td><p>KSP_NODE</p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

KSP **NodeId** \_ 节点的节点标识号指定调谐器节点的标识符。

属性值指定要设置的基本频率。

\_ \_ 用以下内容指定 KSPROPERTY BDA RF \_ 调谐器 \_ 频率属性：

-   \_ \_ 未设置 BDA 频率 \_ (− 1) 指示未设置频率。

-   \_ \_ 未定义 BDA FREQUENCY \_ (0) 指示未定义频率。

如果 KSPROPERTY \_ bda \_ rf \_ 调谐器 \_ frequency \_ 乘数属性指定的 \_ \_ \_ 未 \_ 设置 (− 1) 或 \_ 未定义 bda 频率 \_ 倍数 \_ \_ (0) ，则 KSPROPERTY \_ BDA \_ rf \_ 调谐器 \_ frequency 属性指定千赫 (kHz) 中的频率。 此外，如果未调用微型驱动程序的集处理程序 ([*KStrSetPropertyHandler*](/previous-versions/ff567200(v=vs.85))) ，则微型驱动程序必须确定所提供的频率以 KHz (1Hz x 1000) 的单位表示。 实际上，默认乘数为1000。 有关详细信息，请参阅 [访问 BDA 调谐器节点的频率属性](./accessing-frequency-properties-of-a-bda-tuner-node.md)。

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
<td>Bdamedia (包含 Bdamedia) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**KSP \_ 节点**](/windows-hardware/drivers/ddi/ks/ns-ks-ksp_node)

[**KSPROPERTY \_ BDA \_ RF \_ 调谐器 \_ 频率 \_ 乘数**](ksproperty-bda-rf-tuner-frequency-multiplier.md)

 

