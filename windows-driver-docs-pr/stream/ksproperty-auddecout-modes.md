---
title: KSPROPERTY \_ AUDDECOUT \_ 模式
description: KSPROPERTY \_ AUDDECOUT \_ 模式属性返回音频解码器的可用输出模式。此属性是只读的。
keywords:
- KSPROPERTY_AUDDECOUT_MODES 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDDECOUT_MODES
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 99bc09d01cdf042585ed90dd9fb190ee8a50a2d8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96819955"
---
# <a name="ksproperty_auddecout_modes"></a>KSPROPERTY \_ AUDDECOUT \_ 模式


KSPROPERTY \_ AUDDECOUT \_ 模式属性返回音频解码器的可用输出模式。

此属性是只读的。

## <span id="ddk_ksproperty_auddecout_modes_ks"></span><span id="DDK_KSPROPERTY_AUDDECOUT_MODES_KS"></span>


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
<th>获取</th>
<th>设置</th>
<th>目标</th>
<th>属性描述符类型</th>
<th>属性值类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>是</p></td>
<td><p>否</p></td>
<td><p>Pin</p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p>DWORD</p></td>
</tr>
</tbody>
</table>

 

) 操作数据 (的属性值是一个 DWORD 值，它表示音频解码器支持的音频输出模式的位掩码。

<a name="remarks"></a>备注
-------

属性值可以包含在 *Ksmedia* 头文件中定义的以下常量的按位 "或"：

<span id="KSAUDDECOUTMODE_STEREO_ANALOG"></span><span id="ksauddecoutmode_stereo_analog"></span>**KSAUDDECOUTMODE \_ 立体声 \_ 模拟**  
指示输出为模拟立体声。

<span id="KSAUDDECOUTMODE_PCM_51"></span><span id="ksauddecoutmode_pcm_51"></span>**KSAUDDECOUTMODE \_ PCM \_ 51**  
指示输出处于 PCM 5.1 信道数字中。

<span id="KSAUDDECOUTMODE_SPDIFF"></span><span id="ksauddecoutmode_spdiff"></span>**KSAUDDECOUTMODE \_ SPDIFF**  
指示输出的格式为 SPDIFF E-AC3 数码。

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
<td>Ksmedia (包含 Ksmedia) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**KSPROPERTY \_ AUDDECOUT \_ 当前 \_ 模式**](ksproperty-auddecout-cur-mode.md)

