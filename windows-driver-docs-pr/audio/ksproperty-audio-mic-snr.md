---
title: KSPROPERTY\_音频\_MIC\_SNR
description: KSPROPERTY\_音频\_MIC\_SNR 属性指定以 dB 单位度量的麦克风信号与信噪比（SNR）。
ms.assetid: 1DF088D0-7C0D-42B6-B7FA-2E714C70DAA4
keywords:
- KSPROPERTY_AUDIO_MIC_SNR 音频设备
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
ms.openlocfilehash: 07205df06e192a4f92b583097986aa0df7dd97e1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831033"
---
# <a name="ksproperty_audio_mic_snr"></a>KSPROPERTY\_音频\_MIC\_SNR


KSPROPERTY\_音频\_MIC\_SNR 属性指定以 dB 单位度量的麦克风信号与信噪比（SNR）。

### <a name="span-idusage_summary_tablespanspan-idusage_summary_tablespanspan-idusage_summary_tablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用情况摘要表

使用情况摘要表

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
<td align="left"><p>“获取”</p></td>
<td align="left"><p>设置</p></td>
<td align="left"><p>目标</p></td>
<td align="left"><p>属性描述符类型</p></td>
<td align="left"><p>属性值类型</p></td>
</tr>
<tr class="even">
<td align="left"><p>“是”</p></td>
<td align="left"><p>无</p></td>
<td align="left"><p>固定实例</p></td>
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin" data-raw-source="[&lt;strong&gt;KSP_PIN&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin)"><strong>KSP_PIN</strong></a></td>
<td align="left">漫长</td>
</tr>
</tbody>
</table>

 

属性值（操作数据）的类型为 LONG，其中包含以 dB 单位表示的 SNR 信息。 该值使用固定点十进制表示形式。 数据存储为16.16 固定点值。 较高的16位用于值的整数，较低的16位用于值的小数部分。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_音频\_MIC\_SNR 属性请求在请求成功完成后返回状态\_成功。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

音频驱动程序可以为每个麦克风获取麦克风 SNR。 此属性允许从驱动程序检索此信息。

若要让 Windows 10 语音识别体验（例如 Cortana）在具有不同麦克风的各种设备上准确检测和分析用户的声音，操作系统需要知道输入信号的某些特征。 根据该信息，操作系统可以计算出有效的灵敏度，并应用相应的增益来增强输入信号。 有关详细信息，请参阅[语音激活](https://docs.microsoft.com/windows-hardware/drivers/audio/voice-activation)。

从 Windows 10 1607 版开始提供 KSPROPERTY\_音频\_MIC\_SNR。

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

 

 





