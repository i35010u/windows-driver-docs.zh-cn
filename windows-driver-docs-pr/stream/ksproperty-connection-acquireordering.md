---
title: KSPROPERTY\_连接\_ACQUIREORDERING
description: KSPROPERTY\_连接\_ACQUIREORDERING 属性是可选属性，当状态更改顺序很重要时应实现在插针上。
ms.assetid: b0d27615-bece-49b1-8497-f3c389ea37fc
keywords:
- KSPROPERTY_CONNECTION_ACQUIREORDERING 流式处理媒体设备
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
ms.openlocfilehash: efe4be575e6a2b8ece4d5223a44bfc6b0be5d7cc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562863"
---
# <a name="kspropertyconnectionacquireordering"></a>KSPROPERTY\_连接\_ACQUIREORDERING


KSPROPERTY\_连接\_ACQUIREORDERING 属性是可选属性，当状态更改顺序很重要时应实现在插针上。 例如，该属性应实现在通信接收器针如果接收器需要连接到其通信源插针，以设置为 Acquire 状态之前设置接收器 pin 的 pin。

## <span id="ddk_ksproperty_connection_acquireordering_ks"></span><span id="DDK_KSPROPERTY_CONNECTION_ACQUIREORDERING_KS"></span>


### <a name="usage-summary-table"></a>使用率摘要表

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
<th>Get</th>
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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p>BOOL</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

此属性返回 **，则返回 TRUE**如果状态更改顺序非常重要。 如果**FALSE**要返回，不需要实现属性。

此只读属性用于确定是否为此通信接收器 pin 有效获取停止状态更改。 该属性未实现，排序不重要。 对于基于 IRP 的数据流中，这将实现通过 pin 时它将转发流式处理 Irp 而不是创建新 Irp 的请求，并因此需要通过以指示连接的源 pin 到正确的堆栈深度。 如果 pin 未转发 Irp，则重新计算的堆栈深度不应重要的是，就会是静态筛选器的堆栈深度。

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
<td>Ks.h （包括 Ks.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[KSPROPSETID\_连接](kspropsetid-connection.md)

 

 






