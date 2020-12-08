---
title: KSPROPERTY \_ RTC \_ 读取器
description: KSPROPERTY \_ rtc \_ 读取器属性检索当前磁带位置 (RTC) 的相对时间计数器。
keywords:
- KSPROPERTY_RTC_READER 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_RTC_READER
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a25ca9857a75a53ba8d8e0cad5defb031aa4d17b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837843"
---
# <a name="ksproperty_rtc_reader"></a>KSPROPERTY \_ RTC \_ 读取器


KSPROPERTY \_ rtc \_ 读取器属性检索当前磁带位置 (RTC) 的相对时间计数器。

## <span id="ddk_ksproperty_rtc_reader_ks"></span><span id="DDK_KSPROPERTY_RTC_READER_KS"></span>


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
<td><p>设备</p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_timecode_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_TIMECODE_S&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_timecode_s)"><strong>KSPROPERTY_TIMECODE_S</strong></a></p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagtimecode_sample" data-raw-source="[&lt;strong&gt;TIMECODE_SAMPLE&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagtimecode_sample)"><strong>TIMECODE_SAMPLE</strong></a></p></td>
</tr>
</tbody>
</table>

 

 (操作数据) 的属性值是一个时间码 \_ 示例结构，该结构指定当前磁带位置的相对时间计数器。

<a name="remarks"></a>备注
-------

KSPROPERTY **TimecodeSamp** 时间 \_ 码 S 结构的 TimecodeSamp 成员描述了 \_ 当前磁带位置的相对时间计数器。

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

[**KSPROPERTY 时间 \_ 码 \_ S**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_timecode_s)

[**时间码 \_ 示例**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagtimecode_sample)

