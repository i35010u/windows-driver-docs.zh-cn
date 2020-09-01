---
title: KSPROPERTY \_ STREAMALLOCATOR \_ FUNCTIONTABLE
description: KSPROPERTY \_ STREAMALLOCATOR \_ FUNCTIONTABLE 属性检索给定分配器的函数表。
ms.assetid: 5a55c808-2960-41c7-b242-69d1e10d0015
keywords:
- KSPROPERTY_STREAMALLOCATOR_FUNCTIONTABLE 流媒体设备
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
ms.openlocfilehash: 46f5e08ec2ebbf53e6c7f567552b04cdbeae1c0a
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89189963"
---
# <a name="ksproperty_streamallocator_functiontable"></a>KSPROPERTY \_ STREAMALLOCATOR \_ FUNCTIONTABLE


KSPROPERTY \_ STREAMALLOCATOR \_ FUNCTIONTABLE 属性检索给定分配器的函数表。

## <span id="ddk_ksproperty_streamallocator_functiontable_ks"></span><span id="DDK_KSPROPERTY_STREAMALLOCATOR_FUNCTIONTABLE_KS"></span>


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
<td><p>分配器</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksstreamallocator_functiontable" data-raw-source="[&lt;strong&gt;KSSTREAMALLOCATOR_FUNCTIONTABLE&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/ns-ks-ksstreamallocator_functiontable)"><strong>KSSTREAMALLOCATOR_FUNCTIONTABLE</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

KSPROPERTY \_ STREAMALLOCATOR \_ FUNCTIONTABLE 只由支持调度 \_ 级别函数接口的分配器使用。 支持此属性的分配器必须能够为派单 \_ 级别和更低的 IRQL 分配和释放帧。 此属性只能从内核模式进行访问。

由于调度 \_ 级别接口与基于 IRP 的接口紧密关联，因此获取函数表可能会导致创建内部通知事件，以允许在将帧返回到可用列表时完成挂起的 i/o。 当关闭分配器的句柄时，函数表指针将无效，并且将自动禁用相关事件。

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

## <a name="see-also"></a>另请参阅


[**KSSTREAMALLOCATOR \_ FUNCTIONTABLE**](/windows-hardware/drivers/ddi/ks/ns-ks-ksstreamallocator_functiontable)

 

