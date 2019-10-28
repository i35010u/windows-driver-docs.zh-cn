---
title: KSPROPERTY\_RTC\_读取器
description: KSPROPERTY\_RTC\_读取器属性检索当前磁带位置的相对时间计数器（RTC）。
ms.assetid: 728a4504-de60-47c7-a381-3513f2d4745b
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
ms.openlocfilehash: ed71a1b0ab3d66e335374bd8b7441bc8316d6418
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838832"
---
# <a name="ksproperty_rtc_reader"></a>KSPROPERTY\_RTC\_读取器


KSPROPERTY\_RTC\_读取器属性检索当前磁带位置的相对时间计数器（RTC）。

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
<td><p>设备</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_timecode_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_TIMECODE_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_timecode_s)"><strong>KSPROPERTY_TIMECODE_S</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagtimecode_sample" data-raw-source="[&lt;strong&gt;TIMECODE_SAMPLE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagtimecode_sample)"><strong>TIMECODE_SAMPLE</strong></a></p></td>
</tr>
</tbody>
</table>

 

属性值（操作数据）是指定当前磁带位置的相对时间计数器的时间码\_示例结构。

<a name="remarks"></a>备注
-------

KSPROPERTY\_\_时间段的**TimecodeSamp**成员描述了当前磁带位置的相对时间计数器。

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

[**KSPROPERTY\_时间码\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_timecode_s)

[**时间码\_示例**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagtimecode_sample)

 

 






