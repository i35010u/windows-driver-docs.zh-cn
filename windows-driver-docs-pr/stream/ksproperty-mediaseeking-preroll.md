---
title: KSPROPERTY\_MEDIASEEKING\_预缓冲
description: KSPROPERTY\_MEDIASEEKING\_预计算属性检索筛选器上所需的以100毫微秒为单位的预缓冲量。
ms.assetid: 3b9a5458-b26a-452b-b7aa-7bbb30c3d631
keywords:
- KSPROPERTY_MEDIASEEKING_PREROLL 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_MEDIASEEKING_PREROLL
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 33f8f5faf0ec7c0307584089302fbb9fa50e775b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845637"
---
# <a name="ksproperty_mediaseeking_preroll"></a>KSPROPERTY\_MEDIASEEKING\_预缓冲


KSPROPERTY\_MEDIASEEKING\_预计算属性检索筛选器上所需的以100毫微秒为单位的预缓冲量。

## <span id="ddk_ksproperty_mediaseeking_preroll_ks"></span><span id="DDK_KSPROPERTY_MEDIASEEKING_PREROLL_KS"></span>


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
<td><p>Filter</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p>LONGLONG</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

此属性返回以 LONGLONG 类型的值形式表示的预缓冲的100毫微秒单位数。

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


[KSPROPSETID\_MediaSeeking](kspropsetid-mediaseeking.md)

 

 






