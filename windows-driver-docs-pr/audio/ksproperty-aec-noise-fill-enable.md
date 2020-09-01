---
title: KSPROPERTY \_ AEC \_ 干扰 \_ 填充 \_ 启用
description: KSPROPERTY \_ AEC \_ 干扰 " \_ 启用" \_ 属性用于启用和禁用背景杂色填充。 这是 AEC 节点的一个可选属性， (KSNODETYPE \_ \_ 的声音回声 \_ 取消) 。
ms.assetid: 7c0ed4ba-d25e-42b5-b213-fbe74040a453
keywords:
- KSPROPERTY_AEC_NOISE_FILL_ENABLE 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_AEC_NOISE_FILL_ENABLE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 88001888e72233cfb70c235b2c05bcbbdbedda88
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89208999"
---
# <a name="ksproperty_aec_noise_fill_enable"></a>KSPROPERTY \_ AEC \_ 干扰 \_ 填充 \_ 启用


KSPROPERTY \_ AEC \_ 干扰 " \_ 启用" \_ 属性用于启用和禁用背景杂色填充。 这是 AEC 节点的一个可选属性， ([**KSNODETYPE 的 \_ 声音 \_ 回声 \_ 取消**](ksnodetype-acoustic-echo-cancel.md)) 。

## <span id="ddk_ksproperty_aec_noise_fill_enable_ks"></span><span id="DDK_KSPROPERTY_AEC_NOISE_FILL_ENABLE_KS"></span>


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
<td align="left"><p>Pin</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p>BOOL</p></td>
</tr>
</tbody>
</table>

 

操作数据) 的属性值 (为 BOOL 类型。 将此值设置为 **TRUE** 可启用背景杂色填充。 启用后，节点会将背景噪音插入捕获流中。 将此值设置为 **FALSE** 可禁用背景杂色填充。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY \_ AEC \_ 干扰 \_ \_ 启用属性请求返回状态 " \_ 成功" 以指示已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

AEC 节点会在捕获流中插入背景舒适的噪音，以避免在完全回显取消后将捕获的数据流设置为零时发生的非自然无声。

当包含 AEC 节点的筛选器已创建或节点被重置时，默认情况下禁用后台杂色填充。

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

 

