---
title: KSPROPERTY\_音频\_算法\_实例
description: KSPROPERTY\_音频\_算法\_实例属性指定数字信号处理（DSP）算法，该算法用于实现节点应用于音频数据流的第三方效果。
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
ms.openlocfilehash: 362d6e8627474b4fa1a7518ed6a294648e5cbaff
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831125"
---
# <a name="ksproperty_audio_algorithm_instance"></a>KSPROPERTY\_音频\_算法\_实例


KSPROPERTY\_音频\_算法\_实例属性指定数字信号处理（DSP）算法，该算法用于实现节点应用于音频数据流的第三方效果。 为此属性定义的效果包括声音回声取消和干扰抑制。

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
<td align="left"><p>Filter</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p>GUID</p></td>
</tr>
</tbody>
</table>

 

属性值（操作数据）是一个 GUID，用于标识 pin 应用到其数据流的效果。 此值可以是头文件 Ksmedia 中的以下 Guid 之一：

<span id="KSALGORITHMINSTANCE_SYSTEM_AGC"></span><span id="ksalgorithminstance_system_agc"></span>KSALGORITHMINSTANCE\_SYSTEM\_AGC  
保留以供将来使用

<span id="KSALGORITHMINSTANCE_SYSTEM_ACOUSTIC_ECHO_CANCEL"></span><span id="ksalgorithminstance_system_acoustic_echo_cancel"></span>KSALGORITHMINSTANCE\_系统\_声音\_回音\_取消  
系统默认的声音回声取消算法

<span id="KSALGORITHMINSTANCE_SYSTEM_MICROPHONE_ARRAY_PROCESSOR"></span><span id="ksalgorithminstance_system_microphone_array_processor"></span>KSALGORITHMINSTANCE\_系统\_麦克风\_阵列\_处理器  
保留以供将来使用

<span id="KSALGORITHMINSTANCE_SYSTEM_NOISE_SUPPRESS"></span><span id="ksalgorithminstance_system_noise_suppress"></span>KSALGORITHMINSTANCE\_系统\_噪音\_禁止显示  
系统默认噪音禁止显示算法

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

\_实例属性请求的 KSPROPERTY\_音频\_算法返回状态\_"成功" 以指示已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

此属性用于控制 AEC 节点所执行的 DSP 算法（[**KSNODETYPE\_声音\_回音\_取消**](ksnodetype-acoustic-echo-cancel.md)）或干扰禁止显示节点（[**KSNODETYPE\_干扰点\_抑制**](ksnodetype-noise-suppress.md)）。

算法实例 GUID 与调用方传递给**IDirectSoundCapture：： CreateCaptureBuffer**方法或**DIRECTSOUNDFULLDUPLEXCREATE**函数的 DSCEFFECTDESC 结构的**guidDSCFXInstance**成员中的值匹配. 有关详细信息，请参阅 Microsoft Windows SDK 文档。

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

[**KSNODETYPE\_\_禁止显示**](ksnodetype-noise-suppress.md)

 

 






