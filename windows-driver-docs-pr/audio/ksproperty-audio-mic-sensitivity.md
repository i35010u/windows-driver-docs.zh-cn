---
title: KSPROPERTY\_音频\_MIC\_敏感度
description: KSPROPERTY\_音频\_MIC\_敏感度属性指定相对于完整扩展 (dBFS) 单元分贝麦克风敏感度。
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
ms.openlocfilehash: 9c82f8d5231c6ae66c690c33cd7772a6080358d6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333005"
---
# <a name="kspropertyaudiomicsensitivity"></a>KSPROPERTY\_音频\_MIC\_敏感度

KSPROPERTY\_音频\_MIC\_敏感度属性指定相对于完整扩展 (dBFS) 单元分贝麦克风敏感度。

> [!NOTE]
> KSPROPERTY\_音频\_MIC\_从 Windows 10 版本 1803年开始弃用的敏感度。 使用[KSPROPERTY\_音频\_MIC\_SENSITIVITY2](ksproperty-audio-mic-sensitivity2.md)相反。

### <a name="span-idusagesummarytablespanspan-idusagesummarytablespanspan-idusagesummarytablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用率摘要表



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
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff566722" data-raw-source="[&lt;strong&gt;KSP_PIN&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566722)"><strong>KSP_PIN</strong></a></td>
<td align="left">长</td>
</tr>
</tbody>
</table>

 

（操作数据） 的属性值属于类型 long 类型的值，包含相对于 dBFS 单位分贝敏感度信息。 敏感度值使用以下等级。 值使用定点十进制表示形式。 数据存储为 16.16 固定的点值。 较高的 16 位用于值的整数，低 16 位适用值的小数部分。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_音频\_MIC\_敏感度属性请求返回状态\_请求的成功完成后成功。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

音频驱动程序可以获取每个麦克风的麦克风敏感度。 此属性允许从驱动程序检索此信息。

Windows 10 语音识别体验，例如 Cortana 可以准确地检测并使用不同麦克风分析各种设备上的用户的声音，操作系统需要知道输入信号的某些特征。 根据该信息，操作系统可以计算有效敏感度并应用相应的提升来增强输入的信号。 有关详细信息，请参阅[语音激活](https://msdn.microsoft.com/library/windows/hardware/mt593238)。

KSPROPERTY\_音频\_MIC\_敏感度是 Windows 10，版本 1607年开始可用。

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

 

 





