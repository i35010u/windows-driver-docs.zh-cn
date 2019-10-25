---
title: KSPROPERTY\_EXTXPORT\_时间码\_搜索
description: KSPROPERTY\_EXTXPORT\_时间码\_搜索属性搜索特定时间码。
ms.assetid: 34252fce-426b-4f75-b57f-fa86654ffc5f
keywords:
- KSPROPERTY_EXTXPORT_TIMECODE_SEARCH 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_EXTXPORT_TIMECODE_SEARCH
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5c660bf134de6f8140dbdb96f19eaffa2e7293a1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827007"
---
# <a name="ksproperty_extxport_timecode_search"></a>KSPROPERTY\_EXTXPORT\_时间码\_搜索


KSPROPERTY\_EXTXPORT\_时间码\_搜索属性搜索特定时间码。

## <span id="ddk_ksproperty_extxport_timecode_search_ks"></span><span id="DDK_KSPROPERTY_EXTXPORT_TIMECODE_SEARCH_KS"></span>


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
<td><p>嵌入时间<strong>码</strong>结构</p></td>
</tr>
</tbody>
</table>

 

属性值（操作数据）是 KSPROPERTY\_EXTXPORT\_S 结构的嵌入时间**码**结构成员，用于描述要搜索的特定时间码，包括帧、秒、分钟和小时。

<a name="remarks"></a>备注
-------

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

 

 






