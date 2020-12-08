---
title: KSPROPERTY \_ 调谐器 \_ 频率
description: KSPROPERTY \_ 调谐器 \_ frequency 属性设置或获取调谐器的当前频率或通道。 必须实现此属性。
keywords:
- KSPROPERTY_TUNER_FREQUENCY 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_TUNER_FREQUENCY
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7a7a9aab413bdfd44d7a9adef6bcc8d61554c5aa
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840529"
---
# <a name="ksproperty_tuner_frequency"></a>KSPROPERTY \_ 调谐器 \_ 频率


KSPROPERTY \_ 调谐器 \_ frequency 属性设置或获取调谐器的当前频率或通道。 必须实现此属性。

## <span id="ddk_ksproperty_tuner_frequency_ks"></span><span id="DDK_KSPROPERTY_TUNER_FREQUENCY_KS"></span>


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
<td><p>是</p></td>
<td><p>Pin</p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_frequency_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_TUNER_FREQUENCY_S&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_frequency_s)"><strong>KSPROPERTY_TUNER_FREQUENCY_S</strong></a></p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

 (操作数据) 的属性值是一个 ULONG，用于指定调谐器的当前频率。 此值以赫兹 (Hz) 指定。

<a name="remarks"></a>备注
-------

KSPROPERTY **Frequency** \_ 调谐器 Frequency 结构的 Frequency 成员 \_ \_ 指定当前的调谐器频率。

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

[**KSPROPERTY \_ 调谐器 \_ 频率 \_ S**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_frequency_s)

