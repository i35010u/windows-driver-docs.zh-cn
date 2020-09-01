---
title: KSPROPERTY \_ AUDIOENGINE \_ 缓冲区 \_ 大小 \_ 范围
description: KSPROPERTY \_ AUDIOENGINE \_ BUFFER \_ size \_ RANGE 属性指示在调用时，硬件音频引擎可为给定数据格式支持的缓冲区的最小大小和最大大小。 指定缓冲区大小（以字节为单位）。
ms.assetid: 6A5DF24C-A328-4814-A410-2B1E13402A2B
keywords:
- KSPROPERTY_AUDIOENGINE_BUFFER_SIZE_RANGE 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIOENGINE_BUFFER_SIZE_RANGE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ee8c9bbc8489e3bbf92090a62a1933c7195d94ca
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89206919"
---
# <a name="ksproperty_audioengine_buffer_size_range"></a>KSPROPERTY \_ AUDIOENGINE \_ 缓冲区 \_ 大小 \_ 范围


**KSPROPERTY \_ AUDIOENGINE \_ BUFFER \_ size \_ RANGE**属性指示在调用时，硬件音频引擎可为给定数据格式支持的缓冲区的最小大小和最大大小。 指定缓冲区大小（以字节为单位）。

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_tagksaudioengine_buffer_size_range" data-raw-source="[&lt;strong&gt;KSAUDIOENGINE_BUFFER_SIZE_RANGE&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_tagksaudioengine_buffer_size_range)"><strong>KSAUDIOENGINE_BUFFER_SIZE_RANGE</strong></a></p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

**KSPROPERTY \_ AUDIOENGINE \_ 缓冲区 \_ 大小 \_ 范围**属性请求返回状态 " ** \_ 成功**" 以指示它已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

请务必注意，在调用方调用 **KSPROPERTY \_ AUDIOENGINE \_ BUFFER \_ SIZE \_ 范围** 属性之前，调用方将填充 [**KSDATAFORMAT \_ WAVEFORMATEX**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksdataformat_waveformatex) 结构的字段。 因此，当调用 **KSPROPERTY \_ AUDIOENGINE \_ 缓冲区 \_ 大小 \_ 范围** 时，音频驱动程序将接收一个 KSP \_ 节点，后跟来自调用方的已填充 **KSDATAFORMAT \_ WAVEFORMATEX** 结构。 驱动程序使用此结构中的数据格式信息来确定最小和最大缓冲区大小以适应指定的数据格式。 成功调用此属性后，内核流式处理 (KS) 筛选器将填充[**KSAUDIOENGINE \_ 缓冲区 \_ 大小 \_ 范围**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_tagksaudioengine_buffer_size_range)结构的**MinBufferBytes**和**MaxBufferBytes**字段。

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


[**KSAUDIOENGINE \_ 缓冲区 \_ 大小 \_ 范围**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_tagksaudioengine_buffer_size_range)

[**KSDATAFORMAT \_ WAVEFORMATEX**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksdataformat_waveformatex)

[**KSPROPERTY \_ AUDIOENGINE**](ksproperty-audioengine.md)

 

