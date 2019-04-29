---
title: KSPROPERTY\_EXTXPORT\_TIMECODE\_SEARCH
description: KSPROPERTY\_EXTXPORT\_时间码\_搜索属性搜索到特定时间码。
ms.assetid: 34252fce-426b-4f75-b57f-fa86654ffc5f
keywords:
- KSPROPERTY_EXTXPORT_TIMECODE_SEARCH 流式处理媒体设备
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
ms.openlocfilehash: 5eb65288001e66b87e20f0caf906a7c2b7480ee4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63364005"
---
# <a name="kspropertyextxporttimecodesearch"></a>KSPROPERTY\_EXTXPORT\_TIMECODE\_SEARCH


KSPROPERTY\_EXTXPORT\_时间码\_搜索属性搜索到特定时间码。

## <span id="ddk_ksproperty_extxport_timecode_search_ks"></span><span id="DDK_KSPROPERTY_EXTXPORT_TIMECODE_SEARCH_KS"></span>


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
<td><p>否</p></td>
<td><p>是</p></td>
<td><p>设备</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565167" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTXPORT_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565167)"><strong>KSPROPERTY_EXTXPORT_S</strong></a></p></td>
<td><p>嵌入<strong>时间码</strong>结构</p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 是一个嵌入式**时间码**KSPROPERTY 的结构成员\_EXTXPORT\_S 结构，它描述特定时间码来进行搜索，第二，包括帧，分钟和小时。

<a name="remarks"></a>备注
-------

此方法是定义，但不是受支持。

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
<td>Ksmedia.h （包括 Ksmedia.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)

[**KSPROPERTY\_EXTXPORT\_S**](https://msdn.microsoft.com/library/windows/hardware/ff565167)

 

 






