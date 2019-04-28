---
title: KSPROPERTY\_调谐器\_标准\_模式
description: KSPROPERTY\_调谐器\_标准\_模式属性检索指示驱动程序是否可以设置优化设备能够自动检测从本身的信号的调谐器标准的 BOOL 值。 可以根据需要实现此属性。
ms.assetid: 9c374778-20fd-427a-864f-f57ec14add07
keywords:
- KSPROPERTY_TUNER_STANDARD_MODE 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_TUNER_STANDARD_MODE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 03e7026b3925f727a914552abafbaf1412ee02c1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342129"
---
# <a name="kspropertytunerstandardmode"></a>KSPROPERTY\_调谐器\_标准\_模式


KSPROPERTY\_调谐器\_标准\_模式属性检索指示驱动程序是否可以设置优化设备能够自动检测从本身的信号的调谐器标准的 BOOL 值。 可以根据需要实现此属性。

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
<td><p>否</p></td>
<td><p>Pin</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565913" data-raw-source="[&lt;strong&gt;KSPROPERTY_TUNER_STANDARD_MODE_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565913)"><strong>KSPROPERTY_TUNER_STANDARD_MODE_S</strong></a></p></td>
<td><p>BOOL</p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 是一个布尔值，该值指示是否优化设备可以自动检测到从本身的信号的调谐器标准。

<a name="remarks"></a>备注
-------

详细了解如何为 KSPROPERTY\_调谐器\_标准\_使用模式属性，请参阅[检测调谐器标准](https://msdn.microsoft.com/library/windows/hardware/ff558691)。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Version</p></td>
<td><p>在 Windows Vista 和更高版本的操作系统中可用。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ksmedia.h （包括 Ksmedia.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**KSPROPERTY\_调谐器\_标准**](ksproperty-tuner-standard.md)

[**KSPROPERTY\_调谐器\_标准\_模式\_S**](https://msdn.microsoft.com/library/windows/hardware/ff565913)

 

 






