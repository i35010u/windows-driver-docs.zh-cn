---
title: KSPROPERTY \_ TOPOLOGYNODE \_ ENABLE
description: KSPROPERTY \_ TOPOLOGYNODE \_ ENABLE 属性用于在已生成的拓扑中打开或关闭拓扑节点。
ms.assetid: 6b9f7a92-97dc-476b-962a-40ccf1987154
keywords:
- KSPROPERTY_TOPOLOGYNODE_ENABLE 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_TOPOLOGYNODE_ENABLE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b9b336f11d4381eb78615eeb5abd9133f6aaa714
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90101820"
---
# <a name="ksproperty_topologynode_enable"></a>KSPROPERTY \_ TOPOLOGYNODE \_ ENABLE


KSPROPERTY \_ TOPOLOGYNODE \_ ENABLE 属性用于在已生成的拓扑中打开或关闭拓扑节点。

## <span id="ddk_ksproperty_topologynode_enable_ks"></span><span id="DDK_KSPROPERTY_TOPOLOGYNODE_ENABLE_KS"></span>


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
<td align="left"><p>筛选器</p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p>BOOL</p></td>
</tr>
</tbody>
</table>

 

操作数据) 的属性值 (为 BOOL 类型，并指定该节点是打开还是关闭。 如果值为 **TRUE** ，则表示该节点处于打开状态。 **FALSE** 指示节点处于关闭状态。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY \_ TOPOLOGYNODE \_ ENABLE 属性请求返回状态 \_ SUCCESS 以指示已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

启用已启用的节点或禁用已禁用的节点不起作用，但不应将其视为错误。

禁用节点会关闭该节点在通过该节点的流上执行的转换。 对于 AEC、AGC 或干扰关闭节点 ([**KSNODETYPE 声 \_ \_ 回声 \_ CANCEL**](ksnodetype-acoustic-echo-cancel.md)、 [**KSNODETYPE \_ AGC**](ksnodetype-agc.md)或 [**KSNODETYPE \_ 噪音 \_ **](ksnodetype-noise-suppress.md) 取消) ，例如，禁用的节点在传递模式下操作 (也就是说，它在流从节点的输入插针流动到其输出插针) 时不对该流执行任何操作。

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


[**KSNODEPROPERTY**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)

[**KSNODETYPE \_ 回声 \_ \_ 取消**](ksnodetype-acoustic-echo-cancel.md)

[**KSNODETYPE \_ AGC**](ksnodetype-agc.md)

[**KSNODETYPE \_ 干扰 \_**](ksnodetype-noise-suppress.md)

