---
title: KSPROPERTY \_ STREAMALLOCATOR \_ 状态
description: KSPROPERTY \_ STREAMALLOCATOR \_ STATUS 属性检索指定分配器的当前状态。
ms.assetid: af88253b-e72d-4ea9-855d-0a91e6e35d0f
keywords:
- KSPROPERTY_STREAMALLOCATOR_STATUS 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_STREAMALLOCATOR_STATUS
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6a6d6fd4ec6008163d03157bb62be5542a27fd80
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90106974"
---
# <a name="ksproperty_streamallocator_status"></a>KSPROPERTY \_ STREAMALLOCATOR \_ 状态


KSPROPERTY \_ STREAMALLOCATOR \_ STATUS 属性检索指定分配器的当前状态。

## <span id="ddk_ksproperty_streamallocator_status_ks"></span><span id="DDK_KSPROPERTY_STREAMALLOCATOR_STATUS_KS"></span>


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
<td><p><a href="/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ks/ns-ks-ksstreamallocator_status" data-raw-source="[&lt;strong&gt;KSSTREAMALLOCATOR_STATUS&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/ns-ks-ksstreamallocator_status)"><strong>KSSTREAMALLOCATOR_STATUS</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

分配器的状态指示组帧规范和当前分配的帧。

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


[**KSSTREAMALLOCATOR \_ 状态**](/windows-hardware/drivers/ddi/ks/ns-ks-ksstreamallocator_status)

