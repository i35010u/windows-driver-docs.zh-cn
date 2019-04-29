---
title: KSPROPERTY\_调谐器\_频率
description: KSPROPERTY\_调谐器\_FREQUENCY 属性设置或获取当前的频率或调谐器的通道。 必须实现此属性。
ms.assetid: ba6caf67-63c1-4a31-b93f-3b06b61244bf
keywords:
- KSPROPERTY_TUNER_FREQUENCY 流式处理媒体设备
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
ms.openlocfilehash: 86a9aba51b7f336db151b86c682abd6a41c4ff97
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63355834"
---
# <a name="kspropertytunerfrequency"></a>KSPROPERTY\_调谐器\_频率


KSPROPERTY\_调谐器\_FREQUENCY 属性设置或获取当前的频率或调谐器的通道。 必须实现此属性。

## <span id="ddk_ksproperty_tuner_frequency_ks"></span><span id="DDK_KSPROPERTY_TUNER_FREQUENCY_KS"></span>


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
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>Pin</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565839" data-raw-source="[&lt;strong&gt;KSPROPERTY_TUNER_FREQUENCY_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565839)"><strong>KSPROPERTY_TUNER_FREQUENCY_S</strong></a></p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 为 ULONG，指定当前调谐器的频率。 赫兹 (Hz) 中指定此值。

<a name="remarks"></a>备注
-------

**频率**KSPROPERTY 成员\_调谐器\_频率\_S 结构指定的当前调谐器频率。

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

[**KSPROPERTY\_调谐器\_频率\_S**](https://msdn.microsoft.com/library/windows/hardware/ff565839)

 

 






