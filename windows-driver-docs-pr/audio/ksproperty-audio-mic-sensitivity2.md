---
title: KSPROPERTY\_音频\_MIC\_SENSITIVITY2
description: KSPROPERTY_AUDIO_MIC_SENSITIVITY 属性以分贝相对于完全比例（dBFS）单位指定麦克风灵敏度，包括任何硬件增益。
keywords:
- KSPROPERTY_AUDIO_MIC_SENSITIVITY2 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_MIC_SENSITIVITY2
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 05/10/2018
ms.localizationpriority: medium
ms.openlocfilehash: 0bd5321612badb5977a6e286ba3853d4acfe2689
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832982"
---
# <a name="ksproperty_audio_mic_sensitivity2"></a>KSPROPERTY\_音频\_MIC\_SENSITIVITY2

KSPROPERTY\_音频\_MIC\_SENSITIVITY2 属性指定麦克风相对于完全比例（dBFS）单位（包括任何硬件增益）的以分贝为单位的灵敏度。 在任何软件增益之前，此值包括任何影响 mic 敏感度的硬件集成。  KSPROPERTY\_音频\_MIC\_SENSITIVITY2 属性不包括从音频堆栈应用的任何软件增益。

### <a name="span-idusage_summary_tablespanspan-idusage_summary_tablespanspan-idusage_summary_tablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用情况摘要表

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

属性值（操作数据）的类型为 LONG，并以分贝相对于 dBFS 单位包含敏感度信息。 敏感度值使用以下刻度。 该值使用固定点十进制表示形式。 数据存储为16.16 固定点值。 较高的16位用于值的整数，较低的16位用于值的小数部分。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_音频\_MIC\_SENSITIVITY2 属性请求在请求成功完成后返回状态\_成功。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

音频驱动程序可以获得每个麦克风的麦克风灵敏度。 此属性允许从驱动程序检索此信息。

对于 Windows 10 语音识别体验（例如 Cortana），若要在具有不同麦克风的各种设备上准确检测和分析用户的声音，操作系统需要知道输入信号的某些特征。 根据该信息，操作系统可以计算出有效的灵敏度，并应用相应的增益来增强输入信号。 有关详细信息，请参阅[语音激活](https://docs.microsoft.com/windows-hardware/drivers/audio/voice-activation)。

KSPROPERTY\_音频\_MIC\_SENSITIVITY2 从 Windows 10 版本1803开始提供，并取代[KSPROPERTY\_音频\_](ksproperty-audio-mic-sensitivity.md)的麦克风。


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

<a name="see-also"></a>另请参阅
---------

[KSPROPERTY_AUDIO_MIC_SENSITIVITY](ksproperty-audio-mic-sensitivity.md)





