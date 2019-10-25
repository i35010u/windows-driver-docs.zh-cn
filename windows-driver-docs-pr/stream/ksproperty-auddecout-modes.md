---
title: KSPROPERTY\_AUDDECOUT\_模式
description: KSPROPERTY\_AUDDECOUT\_模式属性返回音频解码器的可用输出模式。此属性是只读的。
ms.assetid: 5ae62fae-7f13-480f-ba36-3fa72ff547bc
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
ms.openlocfilehash: fcd8409e13d1c2558bcbf523d94f2a62a41460b8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842163"
---
# <a name="ksproperty_auddecout_modes"></a>KSPROPERTY\_AUDDECOUT\_模式


KSPROPERTY\_AUDDECOUT\_模式属性返回音频解码器的可用输出模式。

此属性为只读。

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
<td><p>无</p></td>
<td><p>大头针</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p>DWORD</p></td>
</tr>
</tbody>
</table>

 

属性值（操作数据）是一个 DWORD，表示音频解码器支持的音频输出模式的位掩码。

<a name="remarks"></a>备注
-------

属性值可以包含在*Ksmedia*头文件中定义的以下常量的按位 "或"：

<span id="KSAUDDECOUTMODE_STEREO_ANALOG"></span><span id="ksauddecoutmode_stereo_analog"></span>**KSAUDDECOUTMODE\_立体声\_模拟**  
指示输出为模拟立体声。

<span id="KSAUDDECOUTMODE_PCM_51"></span><span id="ksauddecoutmode_pcm_51"></span>**KSAUDDECOUTMODE\_PCM\_51**  
指示输出处于 PCM 5.1 信道数字中。

<span id="KSAUDDECOUTMODE_SPDIFF"></span><span id="ksauddecoutmode_spdiff"></span>**KSAUDDECOUTMODE\_SPDIFF**  
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
<td>Ksmedia （包括 Ksmedia）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**KSPROPERTY\_AUDDECOUT\_当前\_模式**](ksproperty-auddecout-cur-mode.md)

 

 






