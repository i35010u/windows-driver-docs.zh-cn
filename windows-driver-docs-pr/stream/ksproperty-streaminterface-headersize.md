---
title: KSPROPERTY\_STREAMINTERFACE\_HEADERSIZE
description: KSPROPERTY\_STREAMINTERFACE\_HEADERSIZE 属性在 pin 中查询此 pin 所使用的流标头的大小。
ms.assetid: 45c2e10a-c223-4d96-9055-cf012dc50e7a
keywords:
- KSPROPERTY_STREAMINTERFACE_HEADERSIZE 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_STREAMINTERFACE_HEADERSIZE
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3f0b9e161e145af1b85b91fa61d13023f04788d7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837932"
---
# <a name="ksproperty_streaminterface_headersize"></a>KSPROPERTY\_STREAMINTERFACE\_HEADERSIZE


KSPROPERTY\_STREAMINTERFACE\_HEADERSIZE 属性在 pin 中查询此 pin 所使用的流标头的大小。

## <span id="ddk_ksproperty_streaminterface_headersize_ks"></span><span id="DDK_KSPROPERTY_STREAMINTERFACE_HEADERSIZE_KS"></span>


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
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

有关详细信息，请参阅[**KSPIN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_kspin)的**StreamHeaderSize**成员。

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


[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

[**KSPIN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_kspin)

 

 






