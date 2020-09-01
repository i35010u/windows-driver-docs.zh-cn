---
title: KSPROPERTY \_ BDA \_ 信号 \_ 锁 \_ 帽
description: 客户端使用 KSPROPERTY \_ BDA \_ 信号 \_ 锁定 \_ cap 来确定驱动程序可以支持的信号的锁定类型。
ms.assetid: 753f1a3c-5308-49a6-96ee-f7d0090f021a
keywords:
- KSPROPERTY_BDA_SIGNAL_LOCK_CAPS 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_SIGNAL_LOCK_CAPS
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 20c500309d33096ea994bbbe8a8424f2ed4a81bf
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89190151"
---
# <a name="ksproperty_bda_signal_lock_caps"></a>KSPROPERTY \_ BDA \_ 信号 \_ 锁 \_ 帽


客户端使用 KSPROPERTY \_ BDA \_ 信号 \_ 锁定 \_ cap 来确定驱动程序可以支持的信号的锁定类型。

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
<td><p>否</p></td>
<td><p>固定或筛选</p></td>
<td><p>KSP_NODE</p></td>
<td><p>一个32位值，它包含 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/bdamedia/ne-bdamedia-_bdalocktype" data-raw-source="[&lt;strong&gt;BDA_LockType&lt;/strong&gt;](/windows-hardware/drivers/ddi/bdamedia/ne-bdamedia-_bdalocktype)"><strong>BDA_LockType</strong></a>类型化值的按位 "或"</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

KSP **NodeId** \_ 节点的节点1指定了控制节点的标识符，或设置为−1以指定 pin。

返回的32位值是 [**BDA \_ LockType**](/windows-hardware/drivers/ddi/bdamedia/ne-bdamedia-_bdalocktype)类型的值的按位 "或"，用于指示驱动程序支持的锁类型。

RF 调谐器节点应提供此指示。

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


[**BDA \_ LockType**](/windows-hardware/drivers/ddi/bdamedia/ne-bdamedia-_bdalocktype)

[**KSP \_ 节点**](/windows-hardware/drivers/ddi/ks/ns-ks-ksp_node)

[**KSPROPERTY \_ BDA \_ 信号 \_ 锁定 \_ 类型**](ksproperty-bda-signal-lock-type.md)

 

