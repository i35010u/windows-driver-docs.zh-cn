---
title: KSPROPERTY\_AUDIO\_MIC\_SENSITIVITY
description: KSPROPERTY \_ 音频 \_ MIC \_ 敏感度属性以分贝为单位指定麦克风敏感度，相对于完全比例 (dBFS) 单位。
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
ms.openlocfilehash: dbfa5579f07f0d9d6ae27baaae5efe0bfa3ba33d
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90102620"
---
# <a name="ksproperty_audio_mic_sensitivity"></a>KSPROPERTY\_AUDIO\_MIC\_SENSITIVITY

KSPROPERTY \_ 音频 \_ MIC \_ 敏感度属性以分贝为单位指定麦克风敏感度，相对于完全比例 (dBFS) 单位。

> [!NOTE]
> \_ \_ \_ 从 Windows 10 版本1803开始，已弃用 KSPROPERTY 音频 MIC 敏感度。 改为使用 [KSPROPERTY \_ AUDIO \_ MIC \_ SENSITIVITY2](ksproperty-audio-mic-sensitivity2.md) 。

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
<td align="left"><p>获取</p></td>
<td align="left"><p>设置</p></td>
<td align="left"><p>目标</p></td>
<td align="left"><p>属性描述符类型</p></td>
<td align="left"><p>属性值类型</p></td>
</tr>
<tr class="even">
<td align="left"><p>是</p></td>
<td align="left"><p>否</p></td>
<td align="left"><p>固定实例</p></td>
<td align="left"><a href="/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin" data-raw-source="[&lt;strong&gt;KSP_PIN&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin)"><strong>KSP_PIN</strong></a></td>
<td align="left">LONG</td>
</tr>
</tbody>
</table>

 

 (操作数据) 的属性值的类型为 LONG，其中包含相对于 dBFS 单位的以分贝表示的敏感信息。 敏感度值使用以下刻度。 该值使用固定点十进制表示形式。 数据存储为16.16 固定点值。 较高的16位用于值的整数，较低的16位用于值的小数部分。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

\_ \_ \_ 成功完成请求后，KSPROPERTY 音频 MIC 敏感度属性请求返回状态 \_ 成功。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

音频驱动程序可以获得每个麦克风的麦克风灵敏度。 此属性允许从驱动程序检索此信息。

若要让 Windows 10 语音识别体验（例如 Cortana）在具有不同麦克风的各种设备上准确检测和分析用户的声音，操作系统需要知道输入信号的某些特征。 根据该信息，操作系统可以计算出有效的灵敏度，并应用相应的增益来增强输入信号。 有关详细信息，请参阅 [语音激活](./voice-activation.md)。

\_ \_ \_ 从 Windows 10 版本1607开始，可以使用 KSPROPERTY 音频 MIC 敏感度。

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

