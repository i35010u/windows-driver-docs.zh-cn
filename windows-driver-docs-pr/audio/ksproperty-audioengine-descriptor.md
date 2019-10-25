---
title: KSPROPERTY\_AUDIOENGINE\_描述符
description: 适用于卸载的硬件解决方案的音频驱动程序使用 KSPROPERTY\_AUDIOENGINE\_描述符来提供有关表示硬件音频引擎的节点的信息。
ms.assetid: 1D912155-6DB2-4AFF-949F-47C19E47678C
keywords:
- KSPROPERTY_AUDIOENGINE_DESCRIPTOR 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIOENGINE_DESCRIPTOR
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: dda089f57de17500d99f01f6234ba3879edca45b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832880"
---
# <a name="ksproperty_audioengine_descriptor"></a>KSPROPERTY\_AUDIOENGINE\_描述符


适用于卸载的硬件解决方案的音频驱动程序使用**KSPROPERTY\_AUDIOENGINE\_描述符**来提供有关表示硬件音频引擎的节点的信息。

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
<td align="left"><p>“是”</p></td>
<td align="left"><p>无</p></td>
<td align="left"><p>节点 via 筛选器</p></td>
<td align="left"><p>KSP_NODE</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_tagksaudioengine_descriptor" data-raw-source="[&lt;strong&gt;KSAUDIOENGINE_DESCRIPTOR&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_tagksaudioengine_descriptor)"><strong>KSAUDIOENGINE_DESCRIPTOR</strong></a></p></td>
</tr>
</tbody>
</table>

 

属性值的类型为**KSAUDIOENGINE\_描述符**，它指示音频引擎节点的静态属性。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

**KSPROPERTY\_AUDIOENGINE\_描述符**属性请求返回**状态\_SUCCESS** ，以指示已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>版本</p></td>
<td align="left"><p>Windows 8</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Ksmedia.h</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**KSAUDIOENGINE\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_tagksaudioengine_descriptor)

[**KSPROPERTY\_AUDIOENGINE**](ksproperty-audioengine.md)

 

 






