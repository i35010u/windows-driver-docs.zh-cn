---
title: KSPROPERTY \_ EXTXPORT \_ ATN \_ 搜索
description: "\"KSPROPERTY \\_ EXTXPORT \\_ ATN \\_ 搜索\" 属性搜索磁带上 (ATN) 的特定绝对磁道号。"
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
ms.openlocfilehash: c1850a8cca09b9fc029280c994579a87590769c6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96830835"
---
# <a name="ksproperty_extxport_atn_search"></a>KSPROPERTY \_ EXTXPORT \_ ATN \_ 搜索


"KSPROPERTY \_ EXTXPORT \_ ATN \_ 搜索" 属性搜索磁带上 (ATN) 的特定绝对磁道号。

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
<th>获取</th>
<th>设置</th>
<th>目标</th>
<th>属性描述符类型</th>
<th>属性值类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>否</p></td>
<td><p>是</p></td>
<td><p>设备</p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_extxport_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTXPORT_S&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_extxport_s)"><strong>KSPROPERTY_EXTXPORT_S</strong></a></p></td>
<td><p>DWORD</p></td>
</tr>
</tbody>
</table>

 

) 操作数据 (的属性值是一个 DWORD，用于指定绝对磁道号。

<a name="remarks"></a>备注
-------

KSPROPERTY **dwAbsTrackNumber** \_ EXTXPORT S 结构的 dwAbsTrackNumber 成员 \_ 指定要搜索的绝对磁道号。

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
<td>Ksmedia (包含 Ksmedia) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**KSPROPERTY**](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

[**KSPROPERTY \_ EXTXPORT \_ S**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_extxport_s)

