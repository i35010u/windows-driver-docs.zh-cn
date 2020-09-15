---
title: KSPROPERTY \_ 音频 \_ 算法 \_ 实例
description: KSPROPERTY \_ 音频 \_ 算法 \_ 实例属性指定 (DSP) 算法的数字信号处理，该算法用于实现节点应用于音频数据流的第三方效果。
ms.assetid: 8c27f856-de46-42a2-9f1f-e0cef1ee0f6e
keywords:
- KSPROPERTY_AUDIO_ALGORITHM_INSTANCE 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_ALGORITHM_INSTANCE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e70dbc9205cfc7dc775a15b64ac82bb8f4fc4c20
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90102152"
---
# <a name="ksproperty_audio_algorithm_instance"></a>KSPROPERTY \_ 音频 \_ 算法 \_ 实例


KSPROPERTY \_ 音频 \_ 算法 \_ 实例属性指定 (DSP) 算法的数字信号处理，该算法用于实现节点应用于音频数据流的第三方效果。 为此属性定义的效果包括声音回声取消和干扰抑制。

## <span id="ddk_ksproperty_audio_algorithm_instance_ks"></span><span id="DDK_KSPROPERTY_AUDIO_ALGORITHM_INSTANCE_KS"></span>


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
<td align="left"><p>筛选器</p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p>GUID</p></td>
</tr>
</tbody>
</table>

 

 (操作数据) 的属性值是一个 GUID，用于标识 pin 应用到其数据流的效果。 此值可以是头文件 Ksmedia 中的以下 Guid 之一：

<span id="KSALGORITHMINSTANCE_SYSTEM_AGC"></span><span id="ksalgorithminstance_system_agc"></span>KSALGORITHMINSTANCE \_ 系统 \_ AGC  
保留以供将来使用

<span id="KSALGORITHMINSTANCE_SYSTEM_ACOUSTIC_ECHO_CANCEL"></span><span id="ksalgorithminstance_system_acoustic_echo_cancel"></span>KSALGORITHMINSTANCE \_ 系统 \_ 声音 \_ 回声 \_ 取消  
系统默认的声音回声取消算法

<span id="KSALGORITHMINSTANCE_SYSTEM_MICROPHONE_ARRAY_PROCESSOR"></span><span id="ksalgorithminstance_system_microphone_array_processor"></span>KSALGORITHMINSTANCE \_ 系统 \_ 麦克风 \_ 阵列 \_ 处理器  
保留以供将来使用

<span id="KSALGORITHMINSTANCE_SYSTEM_NOISE_SUPPRESS"></span><span id="ksalgorithminstance_system_noise_suppress"></span>KSALGORITHMINSTANCE \_ 系统 \_ 干扰 \_  
系统默认噪音禁止显示算法

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY \_ 音频 \_ 算法 \_ 实例属性请求返回状态 " \_ 成功" 以指示已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

此属性用于控制由 AEC 节点执行的 DSP 算法 (KSNODETYPE 的 "回声" [** \_ \_ \_ 取消**](ksnodetype-acoustic-echo-cancel.md)) 或 "噪音禁止显示" 节点 ([**KSNODETYPE \_ 噪声 \_ 禁止显示**](ksnodetype-noise-suppress.md)) 。

算法实例 GUID 与调用方传递给**IDirectSoundCapture：： CreateCaptureBuffer**方法或**DIRECTSOUNDFULLDUPLEXCREATE**函数的 DSCEFFECTDESC 结构的**guidDSCFXInstance**成员中的值相匹配。 有关详细信息，请参阅 Microsoft Windows SDK 文档。

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

[**KSNODETYPE \_ 干扰 \_**](ksnodetype-noise-suppress.md)

