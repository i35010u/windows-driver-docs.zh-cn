---
title: KSPROPERTY \_ SOUNDDETECTOR \_
description: SOUNDDETECTOR 的 \_ KSPROPERTY \_ 属性是探测器的当前武装状态。
ms.assetid: 3B9B43C0-31EE-4490-AD29-98DA81D1664F
keywords:
- KSPROPERTY_SOUNDDETECTOR_ARMED 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_SOUNDDETECTOR_ARMED
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 09/26/2019
ms.localizationpriority: medium
ms.openlocfilehash: 1fbe75ca6fc0e13cd8f4b8a1db1608ed7e33bfac
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90101928"
---
# <a name="ksproperty_sounddetector_armed"></a>KSPROPERTY \_ SOUNDDETECTOR \_


**SOUNDDETECTOR 的 \_ KSPROPERTY \_ **属性是探测器的当前武装状态。

### <a name="span-idusage_summary_tablespanspan-idusage_summary_tablespanspan-idusage_summary_tablespanusage-summary-table---kspropsetid_sounddetector"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用情况摘要表-KSPROPSETID_SoundDetector

此使用情况表汇总了 \_ \_ 使用[KSPROPSETID_SoundDetector](kspropsetid-sounddetector.md)调用 KSPROPERTY SOUNDDETECTOR 时的情况

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
<th align="left">获取</th>
<th align="left">设置</th>
<th align="left">目标</th>
<th align="left">属性描述符类型</th>
<th align="left">属性值类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>是</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>筛选器</p></td>
<td align="left"><p><a href="/previous-versions/ff564262(v=vs.85)" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](/previous-versions/ff564262(v=vs.85))"><strong>KSPROPERTY</strong></a></p></td>
<td align="left"><p>BOOL</p></td>
</tr>
</tbody>
</table>

当通过 [KSPROPSETID_SoundDetector](kspropsetid-sounddetector.md)调用时，驱动程序会在以下情况下将其重置为 false：

-   禁用筛选器接口。
-   设置 [**KSPROPERTY \_ SOUNDDETECTOR \_ 模式**](ksproperty-sounddetector-patterns.md) 属性。
-   检测到关键字。


### <a name="span-idusage_summary_tablespanspan-idusage_summary_tablespanspan-idusage_summary_tablespanusage-summary-table---kspropsetid_sounddetector2"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用情况摘要表-KSPROPSETID_SoundDetector2


此使用情况表汇总了 \_ \_ 使用[KSPROPSETID_SoundDetector2](kspropsetid-sounddetector2.md)调用 KSPROPERTY SOUNDDETECTOR 时的情况

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
<th align="left">获取</th>
<th align="left">设置</th>
<th align="left">目标</th>
<th align="left">属性描述符类型</th>
<th align="left">属性值类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>是</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>筛选器</p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-kssounddetectorproperty" data-raw-source="[&lt;strong&gt;KSSOUNDDETECTORPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-kssounddetectorproperty"><strong>KSSOUNDDETECTORPROPERTY</strong></a></p></td>
<td align="left"><p>BOOL</p></td>
</tr>
</tbody>
</table>

当使用 [KSPROPSETID_SoundDetector2](kspropsetid-sounddetector2.md) 调用时，在检测到关键字时不会重置 arm 状态。

当以下情况时，它将重置为 false：
- 禁用筛选器接口。
- 设置 [**KSPROPERTY \_ SOUNDDETECTOR \_ 模式**](ksproperty-sounddetector-patterns.md) 属性


### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

属性值为布尔值，指示检测到的武装状态。

<a name="remarks"></a>备注
-------

OS 将此值设置为与检测探测器。

如果未设置关键字模式，则设置为 true ([**KSPROPERTY \_ SOUNDDETECTOR \_ 模式**](ksproperty-sounddetector-patterns.md) 为空) 不起作用。

注意：如果此属性为 true，则将 [**KSPROPERTY \_ SOUNDDETECTOR \_ 模式**](ksproperty-sounddetector-patterns.md) 自动重置为 false （如上所述）。

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
<td align="left"><p>Windows 10</p></td>
</tr>
<tr class="even">
<td align="left"><p>最低受支持的服务器</p></td>
<td align="left"><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td align="left"><p>标头</p></td>
<td align="left">Ksmedia.h</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅

[**KSPROPERTY \_ SOUNDDETECTOR \_ 模式**](ksproperty-sounddetector-patterns.md)

[**KSPROPERTY**](/previous-versions/ff564262(v=vs.85))

[**KSSOUNDDETECTORPROPERTY**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-kssounddetectorproperty)