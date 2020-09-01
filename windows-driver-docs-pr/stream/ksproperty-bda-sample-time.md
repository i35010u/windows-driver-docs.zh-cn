---
title: KSPROPERTY \_ BDA \_ 采样 \_ 时间
description: 客户端使用 KSPROPERTY \_ BDA \_ 采样 \_ 时间来确定平均信号级别和质量的采样时间。
ms.assetid: 53252e11-2a18-42d5-aed8-99052a2b0f21
keywords:
- KSPROPERTY_BDA_SAMPLE_TIME 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_SAMPLE_TIME
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 352f0b278f86a71ef5078ce02b3c166e742660e7
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89190153"
---
# <a name="ksproperty_bda_sample_time"></a>KSPROPERTY \_ BDA \_ 采样 \_ 时间


客户端使用 KSPROPERTY \_ BDA \_ 采样 \_ 时间来确定平均信号级别和质量的采样时间。

## <span id="ddk_ksproperty_bda_sample_time_ks"></span><span id="DDK_KSPROPERTY_BDA_SAMPLE_TIME_KS"></span>


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
<td><p>固定或筛选</p></td>
<td><p>KSP_NODE</p></td>
<td><p>LONG</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

KSP **NodeId** \_ 节点的节点1指定了控制节点的标识符，或设置为−1以指定 pin。

返回的值指定采样时间（以毫秒为单位）。

每次客户端请求 "信号统计信息" 属性时，节点应报告最后 n 毫秒的平均值，其中 n 为 KSPROPERTY \_ BDA 采样时间指示的 \_ 值 \_ 。 如果未设置时间值或驱动程序不支持 KSPROPERTY \_ BDA \_ 采样 \_ 时间，则该驱动程序应默认为100毫秒的采样时间。

该驱动程序可以报告最近完成的采样期间的时间值。

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

[**KSPROPERTY \_ BDA \_ 信号 \_ 质量**](ksproperty-bda-signal-quality.md)

[**KSPROPERTY \_ BDA \_ 信号 \_ 强度**](ksproperty-bda-signal-strength.md)

 

