---
title: KSPROPERTY\_STREAMALLOCATOR\_FUNCTIONTABLE
description: KSPROPERTY\_STREAMALLOCATOR\_FUNCTIONTABLE 属性检索给定分配器的函数表。
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
ms.openlocfilehash: 9f99eb9b155abd0e597f38485ed675a565574863
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837936"
---
# <a name="ksproperty_streamallocator_functiontable"></a>KSPROPERTY\_STREAMALLOCATOR\_FUNCTIONTABLE


KSPROPERTY\_STREAMALLOCATOR\_FUNCTIONTABLE 属性检索给定分配器的函数表。

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
<td><p>分配器</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksstreamallocator_functiontable" data-raw-source="[&lt;strong&gt;KSSTREAMALLOCATOR_FUNCTIONTABLE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksstreamallocator_functiontable)"><strong>KSSTREAMALLOCATOR_FUNCTIONTABLE</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

KSPROPERTY\_STREAMALLOCATOR\_FUNCTIONTABLE 只由支持调度\_级别函数接口的分配器使用。 支持此属性的分配器必须能够为调度\_级别和更低级别的 IRQL 分配和自由帧。 此属性只能从内核模式进行访问。

由于调度\_级别接口与基于 IRP 的接口紧密关联，因此获取函数表可能会导致创建内部通知事件，以允许在将帧返回到时挂起的 i/o 完成免费列表。 当关闭分配器的句柄时，函数表指针将无效，并且将自动禁用相关事件。

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


[**KSSTREAMALLOCATOR\_FUNCTIONTABLE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksstreamallocator_functiontable)

 

 






