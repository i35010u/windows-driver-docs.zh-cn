---
title: KSPROPERTY\_连接\_ACQUIREORDERING
description: KSPROPERTY\_连接\_ACQUIREORDERING 属性是一个可选属性，如果状态更改顺序非常重要，则应在 pin 上实现该属性。
ms.assetid: b0d27615-bece-49b1-8497-f3c389ea37fc
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
ms.openlocfilehash: e0a989d17655c03a8402c6f2c2fff079fa52790a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826853"
---
# <a name="ksproperty_connection_acquireordering"></a>KSPROPERTY\_连接\_ACQUIREORDERING


KSPROPERTY\_连接\_ACQUIREORDERING 属性是一个可选属性，如果状态更改顺序非常重要，则应在 pin 上实现该属性。 例如，如果接收器要求在设置接收器 pin 之前将连接到其通信源 pin 的 pin 设置为 "获取" 状态，则应在通信接收器 pin 上实现属性。

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
<th>“获取”</th>
<th>设置</th>
<th>目标</th>
<th>属性描述符类型</th>
<th>属性值类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>“是”</p></td>
<td><p>无</p></td>
<td><p>大头针</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p>型</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

如果状态更改排序非常重要，则此属性返回**TRUE** 。 如果返回**FALSE** ，则不需要实现属性。

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
<td>Ks （包含 Ks）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[KSPROPSETID\_连接](kspropsetid-connection.md)

 

 






