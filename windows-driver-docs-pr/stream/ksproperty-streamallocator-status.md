---
title: KSPROPERTY\_STREAMALLOCATOR\_状态
description: KSPROPERTY\_STREAMALLOCATOR\_状态属性检索指定的分配器的当前状态。
ms.assetid: af88253b-e72d-4ea9-855d-0a91e6e35d0f
keywords:
- KSPROPERTY_STREAMALLOCATOR_STATUS 流式处理媒体设备
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
ms.openlocfilehash: a53be25a2df4434fd4cd97a3c5ad2a1d0df1f53d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384014"
---
# <a name="kspropertystreamallocatorstatus"></a>KSPROPERTY\_STREAMALLOCATOR\_状态


KSPROPERTY\_STREAMALLOCATOR\_状态属性检索指定的分配器的当前状态。

## <span id="ddk_ksproperty_streamallocator_status_ks"></span><span id="DDK_KSPROPERTY_STREAMALLOCATOR_STATUS_KS"></span>


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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksstreamallocator_status" data-raw-source="[&lt;strong&gt;KSSTREAMALLOCATOR_STATUS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksstreamallocator_status)"><strong>KSSTREAMALLOCATOR_STATUS</strong></a></p></td>
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
<td><p>Header</p></td>
<td>Ks.h （包括 Ks.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**KSSTREAMALLOCATOR\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksstreamallocator_status)

 

 






