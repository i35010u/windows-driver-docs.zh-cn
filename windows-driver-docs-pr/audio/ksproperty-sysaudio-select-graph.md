---
title: KSPROPERTY\_SYSAUDIO\_SELECT\_GRAPH
description: KSPROPERTY\_SYSAUDIO\_选择\_使用关系图属性来显式包括 SysAudio pin 实例为生成虚拟的音频设备的关系图中的可选节点。
ms.assetid: 1107e20e-9ba8-4fda-8457-c357426a9cda
keywords:
- KSPROPERTY_SYSAUDIO_SELECT_GRAPH 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_SYSAUDIO_SELECT_GRAPH
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 79eb872c3761d483363c0eafd960cd662982c1c1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332604"
---
# <a name="kspropertysysaudioselectgraph"></a>KSPROPERTY\_SYSAUDIO\_SELECT\_GRAPH


KSPROPERTY\_SYSAUDIO\_选择\_使用关系图属性来显式包括 SysAudio pin 实例为生成虚拟的音频设备的关系图中的可选节点。

## <span id="ddk_ksproperty_sysaudio_select_graph_ks"></span><span id="DDK_KSPROPERTY_SYSAUDIO_SELECT_GRAPH_KS"></span>


### <a name="span-idusagesummarytablespanspan-idusagesummarytablespanspan-idusagesummarytablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用率摘要表

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
<th align="left">Get</th>
<th align="left">设置</th>
<th align="left">目标</th>
<th align="left">属性描述符类型</th>
<th align="left">属性值类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>否</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>Filter</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff538500" data-raw-source="[&lt;strong&gt;SYSAUDIO_SELECT_GRAPH&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff538500)"><strong>SYSAUDIO_SELECT_GRAPH</strong></a></p></td>
<td align="left"><p>无</p></td>
</tr>
</tbody>
</table>

 

属性描述符 （实例数据） 是一种结构的类型 SYSAUDIO\_选择\_张图表，其中指定的属性、 pin ID 和节点 id。 类型的嵌入结构指定的属性[ **KSPROPERTY**](https://msdn.microsoft.com/library/windows/hardware/ff564262)。 Pin ID 是标识 KS 筛选器，用于包装虚拟音频设备中的 pin 工厂的索引。 节点 ID 是标识中指定的 pin 数据路径的可选节点的索引。 有关详细信息，请参阅以下备注部分。

为此属性定义没有属性值 （操作数据）。 指定属性值的缓冲区指针视为**NULL**和其大小为零。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_SYSAUDIO\_选择\_图形属性请求返回状态\_成功以指示已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

此属性通常用于强制 AEC 节点到 pin 实例的关系图。

实例化时为虚拟的音频设备筛选器上呈现 pin，SysAudio 开始 pin，默认情况下会选择关系图表示通过筛选器的最简单路径。 此关系图中不包括任何可选节点，例如 AEC 控件。

您可以重写 SysAudio 的默认行为的第一个发送 SysAudio KSPROPERTY\_SYSAUDIO\_选择\_图形组属性请求，指定要包含在关系图中的可选节点。 当 SysAudio 随后创建 pin 实例时，插针的关系图将包括在请求中指定的可选节点。

KSPROPERTY\_SYSAUDIO\_选择\_图形组属性请求会影响仅 pin 请求后创建的实例。 请求不起任何先前已实例化的插针上。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h （包括 Ksmedia.h）</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**SYSAUDIO\_SELECT\_GRAPH**](https://msdn.microsoft.com/library/windows/hardware/ff538500)

[**KSPROPERTY**](https://msdn.microsoft.com/library/windows/hardware/ff564262)

 

 






