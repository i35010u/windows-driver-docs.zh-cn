---
title: KSPROPERTY \_ AUDIOENGINE \_ MIXFORMAT
description: KSPROPERTY \_ AUDIOENGINE \_ MIXFORMAT 属性请求检索硬件音频引擎中混音器的设置。
ms.assetid: 12353E72-1092-44B4-861A-90C198237670
keywords:
- KSPROPERTY_AUDIOENGINE_MIXFORMAT 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIOENGINE_MIXFORMAT
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: f18e653e19ceb6b5f483c560bd1a8a9c1abe1745
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89206915"
---
# <a name="ksproperty_audioengine_mixformat"></a>KSPROPERTY \_ AUDIOENGINE \_ MIXFORMAT


**KSPROPERTY \_ AUDIOENGINE \_ MIXFORMAT**属性请求检索硬件音频引擎中混音器的设置。

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
<td align="left"><p>否</p></td>
<td align="left"><p>节点 via 筛选器</p></td>
<td align="left"><p>KSP_NODE</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksdataformat_waveformatex" data-raw-source="[&lt;strong&gt;KSDATAFORMAT_WAVEFORMATEX&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksdataformat_waveformatex)"><strong>KSDATAFORMAT_WAVEFORMATEX</strong></a></p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

**KSPROPERTY \_ AUDIOENGINE \_ MIXFORMAT**属性请求返回**状态 \_ SUCCESS**以指示已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

在任何时间点，在音频引擎节点上设置的组合格式也必须受卸载 pin 工厂支持。

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


[**KSDATAFORMAT \_ WAVEFORMATEX**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksdataformat_waveformatex)

[**KSPROPERTY \_ AUDIOENGINE**](ksproperty-audioengine.md)

 

