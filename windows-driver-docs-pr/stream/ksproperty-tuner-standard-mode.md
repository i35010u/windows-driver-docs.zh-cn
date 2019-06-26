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
ms.openlocfilehash: 7441092ad15848aa48f16cfc30e805f2552a88a9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355968"
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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_tuner_standard_mode_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_TUNER_STANDARD_MODE_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_tuner_standard_mode_s)"><strong>KSPROPERTY_TUNER_STANDARD_MODE_S</strong></a></p></td>
<td><p>BOOL</p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 是一个布尔值，该值指示是否优化设备可以自动检测到从本身的信号的调谐器标准。

<a name="remarks"></a>备注
-------

详细了解如何为 KSPROPERTY\_调谐器\_标准\_使用模式属性，请参阅[检测调谐器标准](https://docs.microsoft.com/windows-hardware/drivers/stream/detecting-tuner-standards)。

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

[**KSPROPERTY\_调谐器\_标准\_模式\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_tuner_standard_mode_s)

 

 






