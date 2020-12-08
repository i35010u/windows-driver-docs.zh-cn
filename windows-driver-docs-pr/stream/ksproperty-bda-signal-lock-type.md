---
title: KSPROPERTY \_ BDA \_ 信号 \_ 锁定 \_ 类型
description: 客户端使用 KSPROPERTY \_ BDA \_ 信号 \_ 锁 \_ 类型来确定信号的当前锁类型。
keywords:
- KSPROPERTY_BDA_SIGNAL_LOCK_TYPE 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_SIGNAL_LOCK_TYPE
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 785601db3dd141ec493296dbbc4536e3bb12c42b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96834887"
---
# <a name="ksproperty_bda_signal_lock_type"></a>KSPROPERTY \_ BDA \_ 信号 \_ 锁定 \_ 类型


客户端使用 KSPROPERTY \_ BDA \_ 信号 \_ 锁 \_ 类型来确定信号的当前锁类型。

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
<td><p><a href="/windows-hardware/drivers/ddi/bdamedia/ne-bdamedia-_bdalocktype" data-raw-source="[&lt;strong&gt;BDA_LockType&lt;/strong&gt;](/windows-hardware/drivers/ddi/bdamedia/ne-bdamedia-_bdalocktype)"><strong>BDA_LockType</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

KSP **NodeId** \_ 节点的节点1指定了控制节点的标识符，或设置为−1以指定 pin。

返回的 [**BDA \_ LockType**](/windows-hardware/drivers/ddi/bdamedia/ne-bdamedia-_bdalocktype)类型值标识当前锁类型。

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

## <a name="see-also"></a>请参阅


[**BDA \_ LockType**](/windows-hardware/drivers/ddi/bdamedia/ne-bdamedia-_bdalocktype)

[**KSP \_ 节点**](/windows-hardware/drivers/ddi/ks/ns-ks-ksp_node)

[**KSPROPERTY \_ BDA \_ 信号 \_ 锁 \_ 帽**](ksproperty-bda-signal-lock-caps.md)

