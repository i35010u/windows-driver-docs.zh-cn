---
title: KSPROPERTY \_ E-ac3 \_ DOWNMIX
description: KSPROPERTY \_ E-ac3 \_ DOWNMIX 属性指定是否需要为 AC 3 编码流中的程序通道 downmixed，以适应扬声器配置。
ms.assetid: 1d47f890-f7da-423f-adef-72b06a0f79d8
keywords:
- KSPROPERTY_AC3_DOWNMIX 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_AC3_DOWNMIX
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ef17bb55631ebd6ee5d5cee79a17d3278d406b27
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90102344"
---
# <a name="ksproperty_ac3_downmix"></a>KSPROPERTY \_ E-ac3 \_ DOWNMIX


KSPROPERTY \_ E-ac3 \_ DOWNMIX 属性指定是否需要为 AC 3 编码流中的程序通道 downmixed，以适应扬声器配置。

## <span id="ddk_ksproperty_ac3_downmix_ks"></span><span id="DDK_KSPROPERTY_AC3_DOWNMIX_KS"></span>


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
<td align="left"><p><a href="/previous-versions/ff564262(v=vs.85)" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](/previous-versions/ff564262(v=vs.85))"><strong>KSPROPERTY</strong></a></p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksac3_downmix" data-raw-source="[&lt;strong&gt;KSAC3_DOWNMIX&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksac3_downmix)"><strong>KSAC3_DOWNMIX</strong></a></p></td>
</tr>
</tbody>
</table>

 

 (操作数据) 的属性值是一个 KSAC3 \_ DOWNMIX 结构，该结构指定程序通道是否应 downmixed。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY \_ E-ac3 \_ DOWNMIX 属性请求返回状态 \_ SUCCESS 以指示该请求已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

如果解码器输出的通道数小于在 AC 3 流中编码的通道数，则需要 Downmixing。

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


[**KSPROPERTY**](/previous-versions/ff564262(v=vs.85))

[**KSAC3 \_ DOWNMIX**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksac3_downmix)

