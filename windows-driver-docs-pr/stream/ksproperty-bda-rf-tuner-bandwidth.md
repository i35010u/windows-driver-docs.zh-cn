---
title: KSPROPERTY \_ BDA \_ RF \_ 调谐器 \_ 带宽
description: 客户端使用 KSPROPERTY \_ BDA \_ RF \_ 调谐器 \_ 带宽来控制调谐器节点的带宽设置。
keywords:
- KSPROPERTY_BDA_RF_TUNER_BANDWIDTH 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_RF_TUNER_BANDWIDTH
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 83c3ffbdee1b20761deb49413d0c55c49f5bed61
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96832563"
---
# <a name="ksproperty_bda_rf_tuner_bandwidth"></a>KSPROPERTY \_ BDA \_ RF \_ 调谐器 \_ 带宽


客户端使用 KSPROPERTY \_ BDA \_ RF \_ 调谐器 \_ 带宽来控制调谐器节点的带宽设置。

## <span id="ddk_ksproperty_bda_rf_tuner_bandwidth_ks"></span><span id="DDK_KSPROPERTY_BDA_RF_TUNER_BANDWIDTH_KS"></span>


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

属性值指定要设置的带宽。 带宽是用于传输信号或相关信号组的频率范围。 换句话说，可以一次传输的信息量。

\_ \_ 用以下内容指定 KSPROPERTY BDA RF \_ 调谐器 \_ 带宽属性：

-   \_ \_ 未设置 BDA 更改带宽 \_ \_ (− 1) 指示未设置带宽。

-   \_ \_ 未定义 BDA 更改带宽 \_ \_ (0) 指示未定义带宽。

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

## <a name="see-also"></a>请参阅


[**KSP \_ 节点**](/windows-hardware/drivers/ddi/ks/ns-ks-ksp_node)

 

