---
title: KSPROPERTY \_ AUDIOMODULE \_ 描述符
description: KSPROPERTY \_ AUDIOMODULE \_ 描述符用于检索终结点波形筛选器上的每个音频模块的静态数据描述符。
keywords:
- KSPROPERTY_AUDIOMODULE_DESCRIPTORS 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIOMODULE_DESCRIPTORS
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b71b97e8c8b8dc2dc4bbabb9c120e108295b4261
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96798923"
---
# <a name="ksproperty_audiomodule_descriptors"></a>KSPROPERTY \_ AUDIOMODULE \_ 描述符


**KSPROPERTY \_AUDIOMODULE \_ 描述符** 用于为 endpoint wave 筛选器上的每个音频模块检索静态数据描述符。

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
<td align="left"><p>筛选器或固定</p></td>
<td align="left"><p><strong>KSPROPERTY</strong></p></td>
<td align="left"><p>对于筛选器目标，KSMULTIPLE_ITEM 后跟描述模板模块的 KSAUDIOMODULE_DESCRIPTOR 的数组。</p>
<p>对于 pin 目标，KSMULTIPLE_ITEM 后跟该流路径中实例化模块的 KSAUDIOMODULE_DESCRIPTOR 数组。</p></td>
</tr>
</tbody>
</table>

 

属性值为结构，后跟零 (0) 或多个 [**KSAUDIOMODULE \_ 说明符**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ksaudiomodule_descriptor) 结构。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

**KSPROPERTY \_AUDIOMODULE \_ 描述符** 返回这些描述符的数组，以响应此请求。

如果驱动程序支持此属性，但它没有任何音频模块，则它将返回一个 \_ 包含零个元素计数的 ksmultiple 项。

有关音频模块的详细信息，请参阅 [实现音频模块发现](./implementing-audio-module-communication.md)。

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
<td align="left"><p>无受支持的版本</p></td>
</tr>
<tr class="odd">
<td align="left"><p>版本</p></td>
<td align="left"><p>Windows 10 版本 1703</p></td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**KSAUDIOMODULE \_ 描述符**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ksaudiomodule_descriptor)

[KSPROPSETID \_ AudioModule](kspropsetid-audiomodule.md)

 

