---
title: KSPROPERTY \_ BDA \_ ECM \_ 映射 \_ 状态
description: 客户端使用 KSPROPERTY \_ BDA \_ ECM \_ 映射 \_ 状态来确定 ECM 映射节点上的状态。
ms.assetid: 8f46e179-8070-4a1b-921d-41d99aaff446
keywords:
- KSPROPERTY_BDA_ECM_MAP_STATUS 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_ECM_MAP_STATUS
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7dd1dd317b8bacd37a9c883c8de05e417300f01c
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89188143"
---
# <a name="ksproperty_bda_ecm_map_status"></a>KSPROPERTY \_ BDA \_ ECM \_ 映射 \_ 状态


客户端使用 KSPROPERTY \_ BDA \_ ECM \_ 映射 \_ 状态来确定 ECM 映射节点上的状态。

## <span id="ddk_ksproperty_bda_ecm_map_status_ks"></span><span id="DDK_KSPROPERTY_BDA_ECM_MAP_STATUS_KS"></span>


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

返回的值指定 ECM 映射节点状态。

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


[**KSEVENT \_ BDA \_ 程序 \_ 流 \_ 状态 \_ 已更改**](ksevent-bda-program-flow-status-changed.md)

[**KSP \_ 节点**](/windows-hardware/drivers/ddi/ks/ns-ks-ksp_node)

 

