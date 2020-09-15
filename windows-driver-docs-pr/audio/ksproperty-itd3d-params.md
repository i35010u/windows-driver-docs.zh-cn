---
title: KSPROPERTY \_ ITD3D \_ 参数
description: KSPROPERTY \_ ITD3D \_ PARAMS 属性用于设置3d 节点的 ITD 算法使用的参数。
ms.assetid: c6f87087-3c91-46a4-b40e-078d0a015c4c
keywords:
- KSPROPERTY_ITD3D_PARAMS 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_ITD3D_PARAMS
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: f0d4a4a5f76ed1d19849945f55574b660bc21a35
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90102000"
---
# <a name="ksproperty_itd3d_params"></a>KSPROPERTY \_ ITD3D \_ 参数


KSPROPERTY \_ ITD3D \_ PARAMS 属性用于设置3d 节点的 ITD 算法使用的参数。

## <span id="ddk_ksproperty_itd3d_params_ks"></span><span id="DDK_KSPROPERTY_ITD3D_PARAMS_KS"></span>


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
<td align="left"><p>Pin</p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksds3d_itd_params_msg" data-raw-source="[&lt;strong&gt;KSDS3D_ITD_PARAMS_MSG&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksds3d_itd_params_msg)"><strong>KSDS3D_ITD_PARAMS_MSG</strong></a></p></td>
</tr>
</tbody>
</table>

 

) 操作数据 (的属性值是 KSDS3D \_ itd PARAMS MSG 类型的 \_ 结构 \_ ，它指定了 itd 算法的参数。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY \_ ITD3D \_ PARAMS 属性请求返回状态 " \_ 成功" 以指示它已成功完成。 否则，请求将返回相应的错误状态代码。

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

[**KSDS3D \_ ITD \_ 参数 \_ 消息**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksds3d_itd_params_msg)

