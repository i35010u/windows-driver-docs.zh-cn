---
title: KSPROPERTY \_ 调谐器 \_ 标准 \_ 模式
description: KSPROPERTY \_ 调谐器 \_ 标准 \_ 模式属性检索一个布尔值，该值指示驱动程序是否可以将优化设备设置为自动检测信号本身的调谐器标准。 此属性可以选择实现。
ms.assetid: 9c374778-20fd-427a-864f-f57ec14add07
keywords:
- KSPROPERTY_TUNER_STANDARD_MODE 流媒体设备
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
ms.openlocfilehash: 5ebcd9a956f82414a1a77ad256f54875cc53c6b6
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90105980"
---
# <a name="ksproperty_tuner_standard_mode"></a>KSPROPERTY \_ 调谐器 \_ 标准 \_ 模式


KSPROPERTY \_ 调谐器 \_ 标准 \_ 模式属性检索一个布尔值，该值指示驱动程序是否可以将优化设备设置为自动检测信号本身的调谐器标准。 此属性可以选择实现。

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
<td><p>Pin</p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_standard_mode_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_TUNER_STANDARD_MODE_S&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_standard_mode_s)"><strong>KSPROPERTY_TUNER_STANDARD_MODE_S</strong></a></p></td>
<td><p>BOOL</p></td>
</tr>
</tbody>
</table>

 

 (操作数据) 的属性值是一个布尔值，该值指示优化设备是否可以自动检测信号本身的调谐器标准。

<a name="remarks"></a>备注
-------

有关如何 \_ 使用 KSPROPERTY 调谐器 \_ 标准模式属性的详细信息 \_ ，请参阅 [检测调谐器标准](./detecting-tuner-standards.md)。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>版本</p></td>
<td><p>在 Windows Vista 和更高版本的操作系统中可用。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ksmedia (包含 Ksmedia) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**KSPROPERTY \_ 调谐器 \_ 标准版**](ksproperty-tuner-standard.md)

[**KSPROPERTY \_ 调谐器 \_ 标准 \_ 模式 \_ S**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_standard_mode_s)

