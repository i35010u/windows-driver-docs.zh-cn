---
title: KSPROPERTY\_VIDEODECODER\_VCR\_计时
description: KSPROPERTY\_VIDEODECODER\_VCR\_计时属性控制 VCR 是否需要来自磁带源或广播源的视频。 此属性为可选项。
ms.assetid: 66d194e4-df9e-4f8a-9767-414311c205da
keywords:
- KSPROPERTY_VIDEODECODER_VCR_TIMING 流媒体设备
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
ms.openlocfilehash: baaccbf82a1874fe3d47abdced2f206fb6e3114e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837863"
---
# <a name="ksproperty_videodecoder_vcr_timing"></a>KSPROPERTY\_VIDEODECODER\_VCR\_计时


KSPROPERTY\_VIDEODECODER\_VCR\_计时属性控制 VCR 是否需要来自磁带源或广播源的视频。 此属性为可选项。

## <span id="ddk_ksproperty_videodecoder_vcr_timing_ks"></span><span id="DDK_KSPROPERTY_VIDEODECODER_VCR_TIMING_KS"></span>


### <a name="usage-summary-table"></a>使用情况摘要表

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
<th>“获取”</th>
<th>设置</th>
<th>目标</th>
<th>属性描述符类型</th>
<th>属性值类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>“是”</p></td>
<td><p>“是”</p></td>
<td><p>大头针</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videodecoder_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEODECODER_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videodecoder_s)"><strong>KSPROPERTY_VIDEODECODER_S</strong></a></p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

属性值（操作数据）是一个 ULONG，用于指定是使用 VCR 计时还是使用广播计时。 如果值为零，则指示广播源。 非零值表示磁带源。

<a name="remarks"></a>备注
-------

KSPROPERTY\_VIDEODECODER\_S 结构的**值**成员指示是使用 VCR 计时还是使用广播计时。

磁带源上的同步脉冲的计时准确性通常与从广播源时的准确性并不准确。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>标头</p></td>
<td>Ksmedia （包括 Ksmedia）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

[**KSPROPERTY\_VIDEODECODER\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videodecoder_s)

 

 






