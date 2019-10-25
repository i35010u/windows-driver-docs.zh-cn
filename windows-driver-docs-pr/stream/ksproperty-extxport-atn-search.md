---
title: KSPROPERTY\_EXTXPORT\_ATN\_搜索
description: KSPROPERTY\_EXTXPORT\_ATN\_搜索属性将搜索磁带上的特定绝对磁道号（ATN）。
ms.assetid: e5bc7552-64a8-4567-9dc3-3f2b50411cc6
keywords:
- KSPROPERTY_EXTXPORT_ATN_SEARCH 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_EXTXPORT_ATN_SEARCH
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1278058a93e04ef622068e1d25b729903135ce87
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827014"
---
# <a name="ksproperty_extxport_atn_search"></a>KSPROPERTY\_EXTXPORT\_ATN\_搜索


KSPROPERTY\_EXTXPORT\_ATN\_搜索属性将搜索磁带上的特定绝对磁道号（ATN）。

## <span id="ddk_ksproperty_extxport_atn_search_ks"></span><span id="DDK_KSPROPERTY_EXTXPORT_ATN_SEARCH_KS"></span>


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
<td><p>设备</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_extxport_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTXPORT_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_extxport_s)"><strong>KSPROPERTY_EXTXPORT_S</strong></a></p></td>
<td><p>DWORD</p></td>
</tr>
</tbody>
</table>

 

属性值（操作数据）是指定绝对磁道号的 DWORD 值。

<a name="remarks"></a>备注
-------

KSPROPERTY\_EXTXPORT\_S 结构的**dwAbsTrackNumber**成员指定要搜索的绝对磁道号。

定义了此方法，但不支持此方法。

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
<td>Ksmedia （包括 Ksmedia）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

[**KSPROPERTY\_EXTXPORT\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_extxport_s)

 

 






