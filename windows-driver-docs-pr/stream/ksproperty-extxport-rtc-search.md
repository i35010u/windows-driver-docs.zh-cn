---
title: KSPROPERTY\_EXTXPORT\_RTC\_SEARCH
description: KSPROPERTY\_EXTXPORT\_RTC\_搜索属性搜索到磁带上的相对时间计数器 (RTC)。
ms.assetid: 4a5b76fc-46f3-44f7-8548-34125df777f5
keywords:
- KSPROPERTY_EXTXPORT_RTC_SEARCH 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_EXTXPORT_RTC_SEARCH
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 62e7ed5da283a0c5495d296a1bd11f049a20d76a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524205"
---
# <a name="kspropertyextxportrtcsearch"></a>KSPROPERTY\_EXTXPORT\_RTC\_SEARCH


KSPROPERTY\_EXTXPORT\_RTC\_搜索属性搜索到磁带上的相对时间计数器 (RTC)。

## <span id="ddk_ksproperty_extxport_rtc_search_ks"></span><span id="DDK_KSPROPERTY_EXTXPORT_RTC_SEARCH_KS"></span>


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
<td><p>DWORD</p></td>
</tr>
</tbody>
</table>

 

（操作数据） 的属性值为 dword 值，指定时间码，小时： 分钟： 秒： 在框架中，若要搜索到磁带上。

<a name="remarks"></a>备注
-------

**DwTimecode** KSPROPERTY 成员\_EXTXPORT\_S 结构指定要搜索的相对时间计数器设置。

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
<td><p>标头</p></td>
<td>Ksmedia.h （包括 Ksmedia.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)

[**KSPROPERTY\_EXTXPORT\_S**](https://msdn.microsoft.com/library/windows/hardware/ff565167)

 

 






