---
title: KSPROPERTY\_音频\_算法\_实例
description: KSPROPERTY\_音频\_算法\_实例属性指定用于实现节点将应用于的音频数据的流的第三方效果的数字信号处理 (DSP) 算法。
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
ms.openlocfilehash: 413093847ebcb1aedaad59eb3b45efbf68eba4ae
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358968"
---
# <a name="kspropertyaudioalgorithminstance"></a>KSPROPERTY\_音频\_算法\_实例


KSPROPERTY\_音频\_算法\_实例属性指定用于实现节点将应用于的音频数据的流的第三方效果的数字信号处理 (DSP) 算法。 为此属性定义的影响包括回声和干扰禁止显示。

## <span id="ddk_ksproperty_audio_algorithm_instance_ks"></span><span id="DDK_KSPROPERTY_AUDIO_ALGORITHM_INSTANCE_KS"></span>


### <a name="span-idusagesummarytablespanspan-idusagesummarytablespanspan-idusagesummarytablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用率摘要表

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
<th align="left">Get</th>
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
<td align="left"><p>Filter</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p>GUID</p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 是一个 GUID，标识 pin 适用于其数据流的效果。 此值可以是以下 Guid 从标头文件 Ksmedia.h 之一：

<span id="KSALGORITHMINSTANCE_SYSTEM_AGC"></span><span id="ksalgorithminstance_system_agc"></span>KSALGORITHMINSTANCE\_SYSTEM\_AGC  
保留供将来使用

<span id="KSALGORITHMINSTANCE_SYSTEM_ACOUSTIC_ECHO_CANCEL"></span><span id="ksalgorithminstance_system_acoustic_echo_cancel"></span>KSALGORITHMINSTANCE\_系统\_声学\_ECHO\_取消  
系统默认回声取消算法

<span id="KSALGORITHMINSTANCE_SYSTEM_MICROPHONE_ARRAY_PROCESSOR"></span><span id="ksalgorithminstance_system_microphone_array_processor"></span>KSALGORITHMINSTANCE\_系统\_麦克风\_数组\_处理器  
保留供将来使用

<span id="KSALGORITHMINSTANCE_SYSTEM_NOISE_SUPPRESS"></span><span id="ksalgorithminstance_system_noise_suppress"></span>KSALGORITHMINSTANCE\_系统\_干扰\_禁止  
系统默认干扰抑制算法

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_音频\_算法\_实例属性请求将返回状态\_成功以指示已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

此属性用于控制由 AEC 节点执行的 DSP 算法 ([**KSNODETYPE\_声学\_ECHO\_取消**](ksnodetype-acoustic-echo-cancel.md)) 或干扰禁止显示节点 （[ **KSNODETYPE\_干扰\_禁止**](ksnodetype-noise-suppress.md))。

算法实例 GUID 与的值匹配**guidDSCFXInstance** DSCEFFECTDESC 结构的调用方传递到成员**IDirectSoundCapture::CreateCaptureBuffer**方法或**DirectSoundFullDuplexCreate**函数。 有关详细信息，请参阅 Microsoft Windows SDK 文档。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h （包括 Ksmedia.h）</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**KSNODEPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksnodeproperty)

[**KSNODETYPE\_ACOUSTIC\_ECHO\_CANCEL**](ksnodetype-acoustic-echo-cancel.md)

[**KSNODETYPE\_干扰\_禁止**](ksnodetype-noise-suppress.md)

 

 






