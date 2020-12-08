---
title: KSPROPERTY \_ 音频 \_ 线性 \_ 缓冲区 \_ 位置
description: KSPROPERTY \_ AUDIO \_ 线性 \_ 缓冲 \_ 位置属性请求检索一个数字，该数字表示自流开始以来 DMA 从音频缓冲区中提取的字节数。
keywords:
- KSPROPERTY_AUDIO_LINEAR_BUFFER_POSITION 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_LINEAR_BUFFER_POSITION
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 21551822c92a602271f91681098e13a95bf63fc9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96799035"
---
# <a name="ksproperty_audio_linear_buffer_position"></a>KSPROPERTY \_ 音频 \_ 线性 \_ 缓冲区 \_ 位置


KSPROPERTY \_ AUDIO \_ 线性 \_ 缓冲 \_ 位置属性请求检索一个数字，该数字表示自流开始以来 DMA 从音频缓冲区中提取的字节数。

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
<td align="left"><p>节点 via 引脚实例</p></td>
<td align="left"><p>KSP_NODE</p></td>
<td align="left"><p>ULONGULONG</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY \_ AUDIO \_ 线性 \_ 缓冲区 \_ 位置属性请求返回状态 " \_ 成功" 以指示已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

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

 

 





