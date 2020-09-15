---
title: KSPROPERTY \_ AUDIOENGINE \_ DEVICEFORMAT
description: KSPROPERTY \_ AUDIOENGINE \_ DEVICEFORMAT 属性请求检索或更改音频引擎节点的状态，有关其设备格式设置。
ms.assetid: 07821ACC-F561-4A40-9E2C-CB30B25521CB
keywords:
- KSPROPERTY_AUDIOENGINE_DEVICEFORMAT 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIOENGINE_DEVICEFORMAT
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3425bf4a7f47a35731f0bba008abd6d9196f2876
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90102012"
---
# <a name="ksproperty_audioengine_deviceformat"></a>KSPROPERTY \_ AUDIOENGINE \_ DEVICEFORMAT


**KSPROPERTY \_ AUDIOENGINE \_ DEVICEFORMAT**属性请求检索或更改音频引擎节点的状态，有关其设备格式设置。

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
<td align="left"><p>是</p></td>
<td align="left"><p>节点 via 筛选器</p></td>
<td align="left"><p>KSP_NODE</p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/ks/ns-ks-ksdataformat" data-raw-source="[&lt;strong&gt;KSDATAFORMAT&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/ns-ks-ksdataformat)"><strong>KSDATAFORMAT</strong></a></p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

**KSPROPERTY \_ AUDIOENGINE \_ DEVICEFORMAT**属性请求返回**状态 \_ SUCCESS**以指示已成功完成。 否则，请求将返回相应的错误状态代码。

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


[**KSDATAFORMAT**](/windows-hardware/drivers/ddi/ks/ns-ks-ksdataformat)

[**KSPROPERTY \_ AUDIOENGINE**](ksproperty-audioengine.md)

