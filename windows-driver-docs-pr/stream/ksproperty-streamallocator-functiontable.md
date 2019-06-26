---
title: KSPROPERTY\_STREAMALLOCATOR\_FUNCTIONTABLE
description: KSPROPERTY\_STREAMALLOCATOR\_FUNCTIONTABLE 属性检索给定的分配器函数表。
ms.assetid: 5a55c808-2960-41c7-b242-69d1e10d0015
keywords:
- KSPROPERTY_STREAMALLOCATOR_FUNCTIONTABLE 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_STREAMALLOCATOR_FUNCTIONTABLE
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 99617df4a7971c3a3a4b728ee272586d0c795ba4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368834"
---
# <a name="kspropertystreamallocatorfunctiontable"></a>KSPROPERTY\_STREAMALLOCATOR\_FUNCTIONTABLE


KSPROPERTY\_STREAMALLOCATOR\_FUNCTIONTABLE 属性检索给定的分配器函数表。

## <span id="ddk_ksproperty_streamallocator_functiontable_ks"></span><span id="DDK_KSPROPERTY_STREAMALLOCATOR_FUNCTIONTABLE_KS"></span>


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
<td><p>分配器</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksstreamallocator_functiontable" data-raw-source="[&lt;strong&gt;KSSTREAMALLOCATOR_FUNCTIONTABLE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksstreamallocator_functiontable)"><strong>KSSTREAMALLOCATOR_FUNCTIONTABLE</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

KSPROPERTY\_STREAMALLOCATOR\_FUNCTIONTABLE 仅由分配器支持在调度\_LEVEL 函数接口。 支持此属性的分配器必须能够分配和释放帧的调度 IRQL\_级别和更低。 可仅从内核模式下访问此属性。

因为调度\_级别接口是密切相关基于 IRP 的界面后，获取函数表是可能会导致创建一个内部通知事件，以允许挂起的 I/O 完成时返回的帧到空闲列表中。 当关闭句柄分配器时，函数表指针无效，关联的事件将被自动禁用。

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


[**KSSTREAMALLOCATOR\_FUNCTIONTABLE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksstreamallocator_functiontable)

 

 






