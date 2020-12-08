---
title: KSPROPERTY \_ ATN \_ 读取器
description: KSPROPERTY \_ ATN \_ READER 属性检索当前磁带位置 (ATN) 的绝对轨迹号。
keywords:
- KSPROPERTY_ATN_READER 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_ATN_READER
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: aa1bbc09f06dac05bef4d6b6be67182f7924d70d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96834895"
---
# <a name="ksproperty_atn_reader"></a>KSPROPERTY \_ ATN \_ 读取器


KSPROPERTY \_ ATN \_ READER 属性检索当前磁带位置 (ATN) 的绝对轨迹号。

## <span id="ddk_ksproperty_atn_reader_ks"></span><span id="DDK_KSPROPERTY_ATN_READER_KS"></span>


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

 

 (操作数据) 的属性值是一个时间码 \_ 示例结构，该结构指定当前磁带位置的绝对跟踪号。

<a name="remarks"></a>备注
-------

KSPROPERTY **TimecodeSamp** 时间 \_ 码 S 结构的 TimecodeSamp 成员 \_ 描述当前磁带位置的绝对跟踪号。

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

