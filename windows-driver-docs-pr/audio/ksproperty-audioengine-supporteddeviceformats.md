---
title: KSPROPERTY \_ AUDIOENGINE \_ SUPPORTEDDEVICEFORMATS
description: KSPROPERTY \_ AUDIOENGINE \_ SUPPORTEDDEVICEFORMATS 属性请求检索硬件音频引擎支持的设备格式。
keywords:
- KSPROPERTY_AUDIOENGINE_SUPPORTEDDEVICEFORMATS 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIOENGINE_SUPPORTEDDEVICEFORMATS
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: baf5a5d1b197522c41d13bb803896e84e809c19f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96798949"
---
# <a name="ksproperty_audioengine_supporteddeviceformats"></a>KSPROPERTY \_ AUDIOENGINE \_ SUPPORTEDDEVICEFORMATS


**KSPROPERTY \_ AUDIOENGINE \_ SUPPORTEDDEVICEFORMATS** 属性请求检索硬件音频引擎支持的设备格式。

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
<td align="left"><p><a href="/windows-hardware/drivers/ddi/ks/ns-ks-ksmultiple_item" data-raw-source="[&lt;strong&gt;KSMULTIPLE_ITEM&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/ns-ks-ksmultiple_item)"><strong>KSMULTIPLE_ITEM</strong></a>结构，后跟一系列<a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksdataformat_waveformatex" data-raw-source="[&lt;strong&gt;KSDATAFORMAT_WAVEFORMATEX&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksdataformat_waveformatex)"><strong>KSDATAFORMAT_WAVEFORMATEX</strong></a>结构</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

**KSPROPERTY \_ AUDIOENGINE \_ SUPPORTEDDEVICEFORMATS** 属性请求返回 **状态 \_ SUCCESS** 以指示已成功完成。 否则，请求将返回相应的错误状态代码。

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

[**KSMULTIPLE \_ 项**](/windows-hardware/drivers/ddi/ks/ns-ks-ksmultiple_item)

[**KSPROPERTY \_ AUDIOENGINE**](ksproperty-audioengine.md)

[**KSPROPERTY \_ AUDIOENGINE \_ VOLUMELEVEL**](ksproperty-audioengine-volumelevel.md)

