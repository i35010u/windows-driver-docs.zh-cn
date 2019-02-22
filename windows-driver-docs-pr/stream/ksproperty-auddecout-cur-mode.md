---
title: KSPROPERTY\_AUDDECOUT\_CUR\_模式
description: KSPROPERTY\_AUDDECOUT\_CUR\_模式属性指示当前的音频输出模式。
ms.assetid: 4ac6d181-f532-4ac6-b8fd-2975214a3618
keywords:
- KSPROPERTY_AUDDECOUT_CUR_MODE 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDDECOUT_CUR_MODE
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c6de09fbd9bbd31a4242a411f26ddd2c54728ffa
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520453"
---
# <a name="kspropertyauddecoutcurmode"></a>KSPROPERTY\_AUDDECOUT\_CUR\_模式


KSPROPERTY\_AUDDECOUT\_CUR\_模式属性指示当前的音频输出模式。

## <span id="ddk_ksproperty_auddecout_cur_mode_ks"></span><span id="DDK_KSPROPERTY_AUDDECOUT_CUR_MODE_KS"></span>


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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p>DWORD</p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 是一个 dword 值，表示音频解码器的当前输出模式。

<a name="remarks"></a>备注
-------

属性值可以是以下标头文件中定义的模式常量之一*ksmedia.h*:

<span id="KSAUDDECOUTMODE_STEREO_ANALOG"></span><span id="ksauddecoutmode_stereo_analog"></span>**KSAUDDECOUTMODE\_STEREO\_ANALOG**  
指示输出是在模拟立体声设备中。

<span id="KSAUDDECOUTMODE_PCM_51"></span><span id="ksauddecoutmode_pcm_51"></span>**KSAUDDECOUTMODE\_PCM\_51**  
指示输出为数字的 PCM 5.1 通道中。

<span id="KSAUDDECOUTMODE_SPDIFF"></span><span id="ksauddecoutmode_spdiff"></span>**KSAUDDECOUTMODE\_SPDIFF**  
指示输出为 SPDIFF 格式 AC3 数字。

音频的微型端口驱动程序 get 属性处理程序返回的当前模式解码器，而音频微型端口驱动程序集属性处理程序请求解码器到请求的模式切换输出音频格式。

我们建议你指定默认值为 KSPROPERTY\_AUDDECOUT\_CUR\_微型驱动程序中的模式属性的序列化的注册表中设置的属性。

有关详细信息，请参阅[音频微型端口驱动程序](https://msdn.microsoft.com/library/windows/hardware/ff536206)。

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
<td>Ksmedia.h （包括 Ksmedia.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**KSPROPERTY\_AUDDECOUT\_模式**](ksproperty-auddecout-modes.md)

 

 






