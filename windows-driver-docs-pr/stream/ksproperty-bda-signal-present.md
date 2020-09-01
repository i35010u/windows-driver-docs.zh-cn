---
title: '\_存在 KSPROPERTY BDA \_ 信号 \_'
description: 客户端使用 KSPROPERTY \_ BDA \_ 信号 \_ 来确定是否存在信号载波。
ms.assetid: d3dbe0f7-a308-48e2-9751-0131fa2b512d
keywords:
- KSPROPERTY_BDA_SIGNAL_PRESENT 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_SIGNAL_PRESENT
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e5f97ab88f480c9ccb8e276d0f6d9fd3b5c36df5
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89192155"
---
# <a name="ksproperty_bda_signal_present"></a>\_存在 KSPROPERTY BDA \_ 信号 \_


客户端使用 KSPROPERTY \_ BDA \_ 信号 \_ 来确定是否存在信号载波。

## <span id="ddk_ksproperty_bda_signal_present_ks"></span><span id="DDK_KSPROPERTY_BDA_SIGNAL_PRESENT_KS"></span>


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
<td><p>BOOL</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注解
-------

KSP **NodeId** \_ 节点的节点1指定了控制节点的标识符，或设置为−1以指定 pin。

返回的值指示是否存在信号载波。 如果有信号载波，则返回 **TRUE** ; 否则返回 **FALSE** 。 RF 调谐器节点应提供此指示。

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
<td>Bdamedia (包含 Bdamedia) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**KSP \_ 节点**](/windows-hardware/drivers/ddi/ks/ns-ks-ksp_node)

 

