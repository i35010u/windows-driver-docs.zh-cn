---
title: KSPROPERTY \_ AUDDECOUT \_ 当前 \_ 模式
description: KSPROPERTY \_ AUDDECOUT \_ \_ current mode 属性指示当前音频输出模式。
ms.assetid: 4ac6d181-f532-4ac6-b8fd-2975214a3618
keywords:
- KSPROPERTY_AUDDECOUT_CUR_MODE 流媒体设备
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
ms.openlocfilehash: b823e525d9902e5c95ac46ad4f2fd55f49e590cb
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90105062"
---
# <a name="ksproperty_auddecout_cur_mode"></a>KSPROPERTY \_ AUDDECOUT \_ 当前 \_ 模式


KSPROPERTY \_ AUDDECOUT \_ \_ current mode 属性指示当前音频输出模式。

## <span id="ddk_ksproperty_auddecout_cur_mode_ks"></span><span id="DDK_KSPROPERTY_AUDDECOUT_CUR_MODE_KS"></span>


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
<td><p>是</p></td>
<td><p>Pin</p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p>DWORD</p></td>
</tr>
</tbody>
</table>

 

) 操作数据 (的属性值是表示音频解码器当前输出模式的 DWORD 值。

<a name="remarks"></a>备注
-------

属性值可以是头文件 *ksmedia*中定义的以下模式常量之一：

<span id="KSAUDDECOUTMODE_STEREO_ANALOG"></span><span id="ksauddecoutmode_stereo_analog"></span>**KSAUDDECOUTMODE \_ 立体声 \_ 模拟**  
指示输出为模拟立体声。

<span id="KSAUDDECOUTMODE_PCM_51"></span><span id="ksauddecoutmode_pcm_51"></span>**KSAUDDECOUTMODE \_ PCM \_ 51**  
指示输出处于 PCM 5.1 信道数字中。

<span id="KSAUDDECOUTMODE_SPDIFF"></span><span id="ksauddecoutmode_spdiff"></span>**KSAUDDECOUTMODE \_ SPDIFF**  
指示输出的格式为 SPDIFF E-AC3 数码。

音频微型端口驱动程序 get 属性处理程序返回解码器的当前模式，而音频微型端口驱动程序设置属性处理程序请求解码器将输出音频格式转换为请求的模式。

建议你在 \_ \_ 注册表中 \_ 设置微型驱动程序的序列化属性中的 KSPROPERTY AUDDECOUT 当前模式属性的默认值。

有关详细信息，请参阅 [音频微型端口驱动程序](../audio/audio-miniport-drivers.md)。

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

## <a name="see-also"></a>另请参阅


[**KSPROPERTY \_ AUDDECOUT \_ 模式**](ksproperty-auddecout-modes.md)

