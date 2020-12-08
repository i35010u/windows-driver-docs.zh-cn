---
title: KSPROPERTY \_ BDA \_ CA \_ 智能 \_ 卡 \_ 状态
description: 客户端使用 KSPROPERTY \_ BDA \_ CA \_ 智能 \_ 卡 \_ 状态来确定与 ECM 映射节点关联的智能卡读卡器的状态。
keywords:
- KSPROPERTY_BDA_CA_SMART_CARD_STATUS 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_CA_SMART_CARD_STATUS
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 28d4c75c19fbab6814f43b5410312670b44c6d43
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96801233"
---
# <a name="ksproperty_bda_ca_smart_card_status"></a>KSPROPERTY \_ BDA \_ CA \_ 智能 \_ 卡 \_ 状态


客户端使用 KSPROPERTY \_ BDA \_ CA \_ 智能 \_ 卡 \_ 状态来确定与 ECM 映射节点关联的智能卡读卡器的状态。

## <span id="ddk_ksproperty_bda_ca_smart_card_status_ks"></span><span id="DDK_KSPROPERTY_BDA_CA_SMART_CARD_STATUS_KS"></span>


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

返回的值指定智能卡读卡器状态。

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


[**KSEVENT \_ BDA \_ CA \_ 智能 \_ 卡 \_ 状态 \_ 已更改**](ksevent-bda-ca-smart-card-status-changed.md)

[**KSP \_ 节点**](/windows-hardware/drivers/ddi/ks/ns-ks-ksp_node)

 

