---
title: KSPROPERTY\_VIDEODECODER\_VCR\_计时
description: KSPROPERTY\_VIDEODECODER\_VCR\_计时属性控制是否应为 VCR 视频从盿源或广播的源。 此属性为可选项。
ms.assetid: 66d194e4-df9e-4f8a-9767-414311c205da
keywords:
- KSPROPERTY_VIDEODECODER_VCR_TIMING 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_VIDEODECODER_VCR_TIMING
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 311467778422992f90a46820c37d54227babce8a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381970"
---
# <a name="kspropertyvideodecodervcrtiming"></a>KSPROPERTY\_VIDEODECODER\_VCR\_计时


KSPROPERTY\_VIDEODECODER\_VCR\_计时属性控制是否应为 VCR 视频从盿源或广播的源。 此属性为可选项。

## <span id="ddk_ksproperty_videodecoder_vcr_timing_ks"></span><span id="DDK_KSPROPERTY_VIDEODECODER_VCR_TIMING_KS"></span>


### <a name="usage-summary-table"></a>使用率摘要表

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
<th>Get</th>
<th>设置</th>
<th>目标</th>
<th>属性描述符类型</th>
<th>属性值类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>Pin</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_videodecoder_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEODECODER_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_videodecoder_s)"><strong>KSPROPERTY_VIDEODECODER_S</strong></a></p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 为 ULONG，用于指定是否应使用 VCR 计时或广播计时。 值为零表示广播的源。 一个非零值指示磁带源。

<a name="remarks"></a>备注
-------

**值**KSPROPERTY 成员\_VIDEODECODER\_S 结构指示是否应使用 VCR 计时或广播计时。

磁带源同步波的计时准确性通常不是同样准确广播源一样。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Ksmedia.h （包括 Ksmedia.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)

[**KSPROPERTY\_VIDEODECODER\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_videodecoder_s)

 

 






