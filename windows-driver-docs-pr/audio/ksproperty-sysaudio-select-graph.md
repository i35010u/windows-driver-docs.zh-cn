---
title: KSPROPERTY \_ SYSAUDIO \_ 选择 \_ 图
description: KSPROPERTY \_ SYSAUDIO \_ SELECT \_ GRAPH 属性用于在图形中显式包含一个可选节点，该节点 SYSAUDIO 为虚拟音频设备上的 pin 实例生成。
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
ms.openlocfilehash: 2a92201cea898c242423311d18cfdc51a46aad0e
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89208907"
---
# <a name="ksproperty_sysaudio_select_graph"></a>KSPROPERTY \_ SYSAUDIO \_ 选择 \_ 图


KSPROPERTY \_ SYSAUDIO \_ SELECT \_ GRAPH 属性用于在图形中显式包含一个可选节点，该节点 SYSAUDIO 为虚拟音频设备上的 pin 实例生成。

## <span id="ddk_ksproperty_sysaudio_select_graph_ks"></span><span id="DDK_KSPROPERTY_SYSAUDIO_SELECT_GRAPH_KS"></span>


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
<td align="left"><p>否</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>筛选器</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-sysaudio_select_graph" data-raw-source="[&lt;strong&gt;SYSAUDIO_SELECT_GRAPH&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-sysaudio_select_graph)"><strong>SYSAUDIO_SELECT_GRAPH</strong></a></p></td>
<td align="left"><p>无</p></td>
</tr>
</tbody>
</table>

 

 (实例数据) 的属性描述符是 SYSAUDIO 选择图形的类型为的结构 \_ \_ ，它指定属性、pin id 和节点 ID。 属性由 [**KSPROPERTY**](/previous-versions/ff564262(v=vs.85))类型的嵌入结构指定。 Pin ID 是一个索引，用于标识用于包装虚拟音频设备的 KS 筛选器中的 pin 工厂。 节点 ID 是标识指定 pin 的数据路径中的可选节点的索引。 有关更多信息，请参见下面的“备注”部分。

没有为此属性定义 (操作数据) 的属性值。 将属性值的缓冲区指针指定为 **NULL** ，并将其大小指定为零。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY \_ SYSAUDIO \_ SELECT \_ GRAPH 属性请求返回状态 \_ SUCCESS 以指示已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

此属性通常用于将 AEC 节点强制转换为插针实例的关系图。

在虚拟音频设备的筛选器上实例化呈现插针时，SysAudio 从该位置开始，并在默认情况下，通过筛选器选择表示最简单路径的关系图。 此图不包括任何可选节点，如 AEC 控件。

您可以重写 SysAudio 的默认行为，方法是：首先发送 SysAudio KSPROPERTY \_ SysAudio \_ 选择 \_ 图形集属性请求，指定要包含在图形中的可选节点。 当 SysAudio 随后创建 pin 实例时，该 pin 的图形将包含请求中指定的可选节点。

KSPROPERTY \_ SYSAUDIO \_ 选择 \_ 图形集-属性请求仅影响在请求后创建的 pin 实例。 该请求对任何以前实例化的 pin 不起作用。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>标头</p></td>
<td align="left">Ksmedia (包含 Ksmedia) </td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**SYSAUDIO \_ 选择 \_ 图形**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-sysaudio_select_graph)

[**KSPROPERTY**](/previous-versions/ff564262(v=vs.85))

 

