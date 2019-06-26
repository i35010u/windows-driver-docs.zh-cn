---
title: KSPROPERTY\_AUDIO\_MIC\_SNR
description: KSPROPERTY\_音频\_MIC\_SNR 属性指定信噪比 (SNR) 以数据库单位的麦克风信号。
ms.assetid: 1DF088D0-7C0D-42B6-B7FA-2E714C70DAA4
keywords:
- KSPROPERTY_AUDIO_MIC_SNR Audio Devices
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_MIC_SNR
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c19ed1872f7f0f2315fe41dfb7264130c4a7a232
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360619"
---
# <a name="kspropertyaudiomicsnr"></a>KSPROPERTY\_AUDIO\_MIC\_SNR


KSPROPERTY\_音频\_MIC\_SNR 属性指定信噪比 (SNR) 以数据库单位的麦克风信号。

### <a name="span-idusagesummarytablespanspan-idusagesummarytablespanspan-idusagesummarytablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用率摘要表

使用率摘要表

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Get</p></td>
<td align="left"><p>设置</p></td>
<td align="left"><p>目标</p></td>
<td align="left"><p>属性描述符类型</p></td>
<td align="left"><p>属性值类型</p></td>
</tr>
<tr class="even">
<td align="left"><p>是</p></td>
<td align="left"><p>否</p></td>
<td align="left"><p>Pin 实例</p></td>
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksp_pin" data-raw-source="[&lt;strong&gt;KSP_PIN&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksp_pin)"><strong>KSP_PIN</strong></a></td>
<td align="left">长</td>
</tr>
</tbody>
</table>

 

（操作数据） 的属性值属于类型 long 类型的值，包含数据库单位中的 SNR 信息。 值使用定点十进制表示形式。 数据存储为 16.16 固定的点值。 较高的 16 位用于值的整数，低 16 位适用值的小数部分。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_音频\_MIC\_SNR 属性请求返回状态\_请求的成功完成后成功。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

音频驱动程序可以获取有关每个麦克风的麦克风 SNR。 此属性允许从驱动程序检索此信息。

Windows 10 语音识别体验，例如 Cortana 可以准确地检测并使用不同麦克风分析各种设备上的用户的声音，操作系统需要知道输入信号的某些特征。 根据该信息，操作系统可以计算有效敏感度并应用相应的提升来增强输入的信号。 有关详细信息，请参阅[语音激活](https://docs.microsoft.com/windows-hardware/drivers/audio/voice-activation)。

KSPROPERTY\_音频\_MIC\_SNR 是 Windows 10，版本 1607年开始可用。

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

 

 





