---
title: KSPROPERTY \_ 连接 \_ ACQUIREORDERING
description: KSPROPERTY \_ CONNECTION \_ ACQUIREORDERING 属性是一个可选属性，当状态更改顺序很重要时，应在 pin 上实现该属性。
keywords:
- KSPROPERTY_CONNECTION_ACQUIREORDERING 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_CONNECTION_ACQUIREORDERING
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4b75d5b1b57d0df0410c09ba65cb1054e03e9fd5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96830837"
---
# <a name="ksproperty_connection_acquireordering"></a>KSPROPERTY \_ 连接 \_ ACQUIREORDERING


KSPROPERTY \_ CONNECTION \_ ACQUIREORDERING 属性是一个可选属性，当状态更改顺序很重要时，应在 pin 上实现该属性。 例如，如果接收器要求在设置接收器 pin 之前将连接到其通信源 pin 的 pin 设置为 "获取" 状态，则应在通信接收器 pin 上实现属性。

## <span id="ddk_ksproperty_connection_acquireordering_ks"></span><span id="DDK_KSPROPERTY_CONNECTION_ACQUIREORDERING_KS"></span>


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
<td><p>Pin</p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p>BOOL</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

如果状态更改排序非常重要，则此属性返回 **TRUE** 。 如果返回 **FALSE** ，则不需要实现属性。

此只读属性用于确定停止-获取状态更改对于此通信接收器 pin 是否有意义。 如果未实现该属性，则假设顺序并不重要。 对于基于 IRP 的数据流，这会在转发流式处理 Irp 时通过 pin 来实现，而不是为请求创建新的 Irp，因此需要向连接的源 pin 指示正确的堆栈深度。 如果该 pin 未转发 Irp，则会重新计算堆栈深度，这并不重要，因为筛选器的堆栈深度为静态。

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
<td>Ks (包含 Ks .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[KSPROPSETID \_ 连接](kspropsetid-connection.md)

