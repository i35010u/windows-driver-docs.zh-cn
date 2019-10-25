---
title: KSPROPERTY\_TOPOLOGYNODE\_启用
description: KSPROPERTY\_TOPOLOGYNODE\_ENABLE 属性用于在已生成的拓扑中打开或关闭拓扑节点。
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
ms.openlocfilehash: 63edfc77bd25a68c2c6b7e4d3dacc15346ca7286
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830476"
---
# <a name="ksproperty_topologynode_enable"></a>KSPROPERTY\_TOPOLOGYNODE\_启用


KSPROPERTY\_TOPOLOGYNODE\_ENABLE 属性用于在已生成的拓扑中打开或关闭拓扑节点。

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
<td align="left"><p>“是”</p></td>
<td align="left"><p>Filter</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p>型</p></td>
</tr>
</tbody>
</table>

 

属性值（操作数据）的类型为 BOOL，并指定该节点是打开还是关闭。 如果值为**TRUE** ，则表示该节点处于打开状态。 **FALSE**指示节点处于关闭状态。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_TOPOLOGYNODE\_ENABLE 属性请求返回状态\_SUCCESS，以指示已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

启用已启用的节点或禁用已禁用的节点不起作用，但不应将其视为错误。

禁用节点会关闭该节点在通过该节点的流上执行的转换。 对于 AEC、AGC 或干扰关闭节点（[**KSNODETYPE\_声音\_回显\_"取消**](ksnodetype-acoustic-echo-cancel.md)"、" [**KSNODETYPE\_AGC**](ksnodetype-agc.md)" 或 " [**KSNODETYPE\_不显示干扰**](ksnodetype-noise-suppress.md)"，例如禁用的节点在直通模式下操作（即，它在流从节点的输入插针流到其输出插针时，不对其执行任何操作）。

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
<td align="left">Ksmedia （包括 Ksmedia）</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**KSNODEPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)

[**KSNODETYPE\_声音\_回音\_取消**](ksnodetype-acoustic-echo-cancel.md)

[**KSNODETYPE\_AGC**](ksnodetype-agc.md)

[**KSNODETYPE\_\_禁止显示**](ksnodetype-noise-suppress.md)

 

 






