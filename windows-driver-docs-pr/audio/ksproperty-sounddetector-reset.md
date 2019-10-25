---
title: KSPROPERTY\_SOUNDDETECTOR\_RESET
description: KSPROPERTY\_SOUNDDETECTOR\_RESET 属性将检测程序重置为不带模式集的 unarmed 状态。
ms.assetid: 3B9B43C0-31EE-4490-AD29-98DA81D1664D
keywords:
- KSPROPERTY_SOUNDDETECTOR_RESET 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_SOUNDDETECTOR_RESET
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 09/25/2019
ms.localizationpriority: medium
ms.openlocfilehash: 2890f4d2d12fc44c17f3dc1991af486af0d3d328
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830578"
---
# <a name="ksproperty_sounddetector_reset"></a>KSPROPERTY\_SOUNDDETECTOR\_RESET

**KSPROPERTY\_SOUNDDETECTOR\_RESET**属性将检测程序重置为不带模式集的 unarmed 状态。

### <a name="span-idusage_summary_tablespanspan-idusage_summary_tablespanspan-idusage_summary_tablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用情况摘要表

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
<th align="left">“获取”</th>
<th align="left">设置</th>
<th align="left">目标</th>
<th align="left">属性描述符类型</th>
<th align="left">属性值类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>无</p></td>
<td align="left"><p>“是”</p></td>
<td align="left"><p>Filter</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-kssounddetectorproperty" data-raw-source="[&lt;strong&gt;KSSOUNDDETECTORPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-kssounddetectorproperty"><strong>KSSOUNDDETECTORPROPERTY</strong></a></p></td>
<td align="left"><p>型</p></td>
</tr>
</tbody>
</table>

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

属性值为布尔值。 True 表示重置，忽略 false。

<a name="remarks"></a>备注
-------

当操作系统要执行以下操作时，会调用 reset，并将值设置为 true：

- Unarm 关键字检测器。
- 清除已设置的任何[**KSPROPERTY\_SOUNDDETECTOR\_模式**](ksproperty-sounddetector-patterns.md)。

如果未设置关键字模式（[**KSPROPERTY\_SOUNDDETECTOR\_模式**](ksproperty-sounddetector-patterns.md)为空），则设置此值不起作用。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>最低受支持的客户端</p></td>
<td align="left"><p>Windows 10 版本1903</p></td>
</tr>
<tr class="odd">
<td align="left"><p>标头</p></td>
<td align="left">Ksmedia.h</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅

[**KSPROPERTY\_SOUNDDETECTOR\_模式**](ksproperty-sounddetector-patterns.md)

[**KSSOUNDDETECTORPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/)
