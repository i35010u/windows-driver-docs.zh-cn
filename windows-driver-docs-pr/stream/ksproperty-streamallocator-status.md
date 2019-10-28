---
title: KSPROPERTY\_STREAMALLOCATOR\_状态
description: KSPROPERTY\_STREAMALLOCATOR\_STATUS 属性检索指定分配器的当前状态。
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
ms.openlocfilehash: e0b448619923a9f09c3c3a603dca1432cc269916
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837934"
---
# <a name="ksproperty_streamallocator_status"></a>KSPROPERTY\_STREAMALLOCATOR\_状态


KSPROPERTY\_STREAMALLOCATOR\_STATUS 属性检索指定分配器的当前状态。

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksstreamallocator_status" data-raw-source="[&lt;strong&gt;KSSTREAMALLOCATOR_STATUS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksstreamallocator_status)"><strong>KSSTREAMALLOCATOR_STATUS</strong></a></p></td>
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
<td>Ks （包含 Ks）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**KSSTREAMALLOCATOR\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksstreamallocator_status)

 

 






