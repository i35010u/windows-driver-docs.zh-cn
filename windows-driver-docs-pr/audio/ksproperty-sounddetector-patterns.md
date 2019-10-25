---
title: KSPROPERTY\_SOUNDDETECTOR\_模式
description: 操作系统将 KSPROPERTY\_SOUNDDETECTOR\_模式属性设置为配置要检测的关键字。
ms.assetid: 7A6AF4F6-5F5F-4A3D-AF61-B3E4374B33AD
keywords:
- KSPROPERTY_SOUNDDETECTOR_PATTERNS 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_SOUNDDETECTOR_PATTERNS
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 09/25/2019
ms.localizationpriority: medium
ms.openlocfilehash: 35ef2ecc1fde4511ef186746c35fc0c744a5a0fd
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830579"
---
# <a name="ksproperty_sounddetector_patterns"></a>KSPROPERTY\_SOUNDDETECTOR\_模式

操作系统将**KSPROPERTY\_SOUNDDETECTOR\_模式**属性设置为配置要检测的关键字。

OS 设置关键字模式，或者可能将此值设置为空值。

当 OS 设置此属性时，驱动程序会自动 disarms 检测程序。

如果由于资源不足而导致驱动程序无法满足 "set" 请求，则驱动程序将失败请求，**状态\_\_资源不足**。

### <a name="span-idusage_summary_tablespanspan-idusage_summary_tablespanspan-idusage_summary_tablespanusage-summary-table---kspropsetid_sounddetector"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用情况摘要表-KSPROPSETID_SoundDetector

此使用情况表汇总了使用[KSPROPSETID_SoundDetector](kspropsetid-sounddetector.md)调用 KSPROPERTY\_SOUNDDETECTOR\_时的情况

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
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/ff564262(v=vs.85)" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))"><strong>KSPROPERTY</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksmultiple_item" data-raw-source="[&lt;strong&gt;KSMULTIPLE_ITEM&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksmultiple_item)"><strong>KSMULTIPLE_ITEM</strong></a></p></td>
</tr>
</tbody>
</table>


### <a name="span-idusage_summary_tablespanspan-idusage_summary_tablespanspan-idusage_summary_tablespanusage-summary-table---kspropsetid_sounddetector2"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用情况摘要表-KSPROPSETID_SoundDetector2

此使用情况表汇总了使用[KSPROPSETID_SoundDetector2](kspropsetid-sounddetector2.md)调用 KSPROPERTY\_SOUNDDETECTOR\_时的情况

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksmultiple_item" data-raw-source="[&lt;strong&gt;KSMULTIPLE_ITEM&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksmultiple_item)"><strong>KSMULTIPLE_ITEM</strong></a></p></td>
</tr>
</tbody>
</table>


### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

属性值是[**KSMULTIPLE\_项**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksmultiple_item)结构，后跟64位对齐检测模式的序列。 每个模式都以[**SOUNDDETECTOR\_PATTERNHEADER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-sounddetector_patternheader)开始，后跟模式负载。

<a name="remarks"></a>备注
-------

在以下时间之前，驱动程序不应完成 "set" 请求：

-   在[**KSPROPERTY\_SOUNDDETECTOR**](ksproperty-sounddetector-armed.md)上，检测到已卸下和后续的 "get" 请求\_会返回 false。
-   对[**KSPROPERTY\_SOUNDDETECTOR\_MATCHRESULT**](ksproperty-sounddetector-matchresult.md)的后续 "get" 请求不返回任何数据。
-   新的关键字模式已建立，并且关键字检测器正在对新模式进行操作。

驱动程序可能会使请求处于挂起状态，直到满足上述条件。 此外，如果设备需要可度量的初始化时间，驱动程序可能会使此请求处于挂起状态，直到设备准备就绪并且可以处理请求。

OS 需要此行为，以避免检测到的关键字和更新关键字模式之间出现争用情况（例如，如果检测到关键字并且 KSEVENT\_SOUNDDETECTOR 在 OS 更新关键字之前生成了即时）。

要完成此请求，OS 至少要等待2秒。

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
<td align="left"><p>Windows 10</p></td>
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


[**SOUNDDETECTOR\_PATTERNHEADER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-sounddetector_patternheader)

[**SOUNDDETECTOR\_模式**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/dn932155(v=vs.85))

[**KSPROPERTY\_SOUNDDETECTOR\_** ](ksproperty-sounddetector-armed.md)

[**KSPROPERTY\_SOUNDDETECTOR\_MATCHRESULT**](ksproperty-sounddetector-matchresult.md)

[**KSPROPERTY**](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))

[**KSMULTIPLE\_项**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksmultiple_item)

 

 






