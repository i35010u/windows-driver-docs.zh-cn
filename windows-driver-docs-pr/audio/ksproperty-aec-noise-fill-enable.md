---
title: KSPROPERTY\_AEC\_干扰\_填充\_启用
description: KSPROPERTY\_AEC\_杂色\_FILL\_ENABLE 属性用于启用和禁用背景杂色填充。 这是 AEC 节点的一个可选属性（KSNODETYPE\_声音\_回音\_"取消"）。
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
ms.openlocfilehash: 5123a84d26766142f9dbb90afe5b602921fe08c1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831135"
---
# <a name="ksproperty_aec_noise_fill_enable"></a>KSPROPERTY\_AEC\_干扰\_填充\_启用


KSPROPERTY\_AEC\_杂色\_FILL\_ENABLE 属性用于启用和禁用背景杂色填充。 这是 AEC 节点的一个可选属性（[**KSNODETYPE\_声音\_回音\_"取消**](ksnodetype-acoustic-echo-cancel.md)"）。

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
<td align="left"><p>大头针</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p>型</p></td>
</tr>
</tbody>
</table>

 

属性值（操作数据）的类型为 BOOL。 将此值设置为**TRUE**可启用背景杂色填充。 启用后，节点会将背景噪音插入捕获流中。 将此值设置为**FALSE**可禁用背景杂色填充。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_AEC\_噪声\_FILL\_ENABLE 属性请求返回状态\_SUCCESS 以指示已成功完成。 否则，请求将返回相应的错误状态代码。

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
<td align="left">Ksmedia （包括 Ksmedia）</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**KSNODEPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)

[**KSNODETYPE\_声音\_回音\_取消**](ksnodetype-acoustic-echo-cancel.md)

 

 






