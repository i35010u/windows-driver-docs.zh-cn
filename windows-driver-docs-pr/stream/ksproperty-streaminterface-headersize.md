---
title: KSPROPERTY \_ STREAMINTERFACE \_ HEADERSIZE
description: KSPROPERTY \_ STREAMINTERFACE \_ HEADERSIZE 属性在 pin 中查询此 pin 所使用的流标头的大小。
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
ms.openlocfilehash: 5c7134c9d5fb00704c1e5825233758e5eceeebe0
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90106968"
---
# <a name="ksproperty_streaminterface_headersize"></a>KSPROPERTY \_ STREAMINTERFACE \_ HEADERSIZE


KSPROPERTY \_ STREAMINTERFACE \_ HEADERSIZE 属性在 pin 中查询此 pin 所使用的流标头的大小。

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
<td><p>Pin</p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注解
-------

有关详细信息，请参阅[**KSPIN**](/windows-hardware/drivers/ddi/ks/ns-ks-_kspin)的**StreamHeaderSize**成员。

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


[**KSPROPERTY**](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

[**KSPIN**](/windows-hardware/drivers/ddi/ks/ns-ks-_kspin)

