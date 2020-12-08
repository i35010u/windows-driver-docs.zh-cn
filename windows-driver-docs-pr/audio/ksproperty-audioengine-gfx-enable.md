---
title: KSPROPERTY \_ AUDIOENGINE \_ GFXENABLE
description: KSPROPERTY \_ AUDIOENGINE \_ GFXENABLE 属性请求允许音频驱动程序检索或更改音频引擎节点的状态，这与它的全局效果处理能力相关。
keywords:
- KSPROPERTY_AUDIOENGINE_GFXENABLE 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIOENGINE_GFXENABLE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 038caf7e3419a4cd6331efa291fcc6b1686ef29f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96798955"
---
# <a name="ksproperty_audioengine_gfxenable"></a>KSPROPERTY \_ AUDIOENGINE \_ GFXENABLE


**KSPROPERTY \_ AUDIOENGINE \_ GFXENABLE** 属性请求允许音频驱动程序检索或更改音频引擎节点的状态，这与它的全局效果处理能力相关。

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
<td align="left"><p>BOOL</p></td>
</tr>
</tbody>
</table>

 

属性值的类型为 **BOOL** ，指示是否启用音频引擎节点中的全局效果处理。 如果值为 **TRUE，则** 表示已启用处理。 **FALSE** 指示它处于禁用状态。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

**KSPROPERTY \_ AUDIOENGINE \_ GFXENABLE** 属性请求返回 **状态 \_ SUCCESS** 以指示已成功完成。 否则，请求将返回相应的错误状态代码。

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


[**KSPROPERTY \_ AUDIOENGINE**](ksproperty-audioengine.md)

[**KSPROPERTY \_ AUDIOENGINE \_ LFXENABLE**](ksproperty-audioengine-lfx-enable.md)

 

 






