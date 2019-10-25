---
title: KSPROPERTY\_MEDIASEEKING\_位置
description: KSPROPERTY\_MEDIASEEKING\_位置属性设置筛选器上的媒体时间和/或停止时间。
ms.assetid: 20f0e97a-37bb-4c01-8012-b73bb765f4b9
keywords:
- KSPROPERTY_MEDIASEEKING_POSITIONS 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_MEDIASEEKING_POSITIONS
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ad5d8d2f57f3b670670e0b93b31b042f43030d03
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842299"
---
# <a name="ksproperty_mediaseeking_positions"></a>KSPROPERTY\_MEDIASEEKING\_位置


KSPROPERTY\_MEDIASEEKING\_位置属性设置筛选器上的媒体时间和/或停止时间。

## <span id="ddk_ksproperty_mediaseeking_positions_ks"></span><span id="DDK_KSPROPERTY_MEDIASEEKING_POSITIONS_KS"></span>


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
<td><p>无</p></td>
<td><p>“是”</p></td>
<td><p>Filter</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksproperty_positions" data-raw-source="[&lt;strong&gt;KSPROPERTY_POSITIONS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksproperty_positions)"><strong>KSPROPERTY_POSITIONS</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

KSPROPERTY\_位置结构指定相对于流的总持续时间的当前位置和停止位置。

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


[**KSPROPERTY\_位置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksproperty_positions)

 

 






