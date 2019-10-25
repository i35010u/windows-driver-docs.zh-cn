---
title: KSPROPERTY\_AUDIOMODULE\_说明符
description: KSPROPERTY\_AUDIOMODULE\_说明符用于检索终结点波形筛选器上的每个音频模块的静态数据描述符。
ms.assetid: EAD613AA-005B-4751-B60E-212853CA40B4
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
ms.openlocfilehash: 10da8d7b34c6f92dc2d8743797075feeca9dbba1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830844"
---
# <a name="ksproperty_audiomodule_descriptors"></a>KSPROPERTY\_AUDIOMODULE\_说明符


**KSPROPERTY\_AUDIOMODULE\_说明符**用于检索终结点波形筛选器上的每个音频模块的静态数据描述符。

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
<td align="left"><p>筛选器或固定</p></td>
<td align="left"><p><strong>KSPROPERTY</strong></p></td>
<td align="left"><p>对于筛选器目标，KSMULTIPLE_ITEM 后跟一个描述模板模块的 KSAUDIOMODULE_DESCRIPTOR 数组。</p>
<p>对于 pin 目标，为该流路径中实例化模块的 KSAUDIOMODULE_DESCRIPTOR 的 KSMULTIPLE_ITEM。</p></td>
</tr>
</tbody>
</table>

 

属性值为结构，后跟零（0）或更多[**KSAUDIOMODULE\_说明符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ksaudiomodule_descriptor)结构。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

**KSPROPERTY\_AUDIOMODULE\_说明符**返回一个数组，这些说明符用于响应此请求。

如果驱动程序支持此属性，但它没有任何音频模块，则它会返回一个 ksmultiple\_项，其中包含零个元素计数。

有关音频模块的详细信息，请参阅[实现音频模块发现](https://docs.microsoft.com/windows-hardware/drivers/audio/implementing-audio-module-communication)。

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
<td align="left"><p>无受支持的版本</p></td>
</tr>
<tr class="odd">
<td align="left"><p>版本</p></td>
<td align="left"><p>Windows 10 版本1703</p></td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**KSAUDIOMODULE\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ksaudiomodule_descriptor)

[KSPROPSETID\_AudioModule](kspropsetid-audiomodule.md)

 

 






