---
title: KSPROPERTY\_音频\_MIC\_敏感度
description: KSPROPERTY\_音频\_MIC\_敏感度属性以分贝相对于完全比例（dBFS）单位指定麦克风灵敏度。
ms.assetid: FE62AAA5-E022-459F-817B-3661535FA9BD
keywords:
- KSPROPERTY_AUDIO_MIC_SENSITIVITY 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_MIC_SENSITIVITY
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 05/10/2018
ms.localizationpriority: medium
ms.openlocfilehash: 7a5755667478ea9c06c001335dd0d48cf5d83f8e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831035"
---
# <a name="ksproperty_audio_mic_sensitivity"></a>KSPROPERTY\_音频\_MIC\_敏感度

KSPROPERTY\_音频\_MIC\_敏感度属性以分贝相对于完全比例（dBFS）单位指定麦克风灵敏度。

> [!NOTE]
> KSPROPERTY\_音频\_MIC\_敏感度从 Windows 10 版本1803开始已弃用。 改为使用[KSPROPERTY\_音频\_MIC\_SENSITIVITY2](ksproperty-audio-mic-sensitivity2.md) 。

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

KSPROPERTY\_音频\_MIC\_敏感度属性请求在请求成功完成后返回状态\_成功。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

音频驱动程序可以获得每个麦克风的麦克风灵敏度。 此属性允许从驱动程序检索此信息。

若要让 Windows 10 语音识别体验（例如 Cortana）在具有不同麦克风的各种设备上准确检测和分析用户的声音，操作系统需要知道输入信号的某些特征。 根据该信息，操作系统可以计算出有效的灵敏度，并应用相应的增益来增强输入信号。 有关详细信息，请参阅[语音激活](https://docs.microsoft.com/windows-hardware/drivers/audio/voice-activation)。

从 Windows 10 1607 版开始，KSPROPERTY\_音频\_MIC\_灵敏度。

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

 

 





