---
title: KSPROPERTY\_音频\_首选\_状态
description: KSPROPERTY\_音频\_首选\_状态属性告知设备是系统的首选音频设备。
ms.assetid: a0e89143-ead1-4e0d-a550-398ec1abf9e9
keywords:
- KSPROPERTY_AUDIO_PREFERRED_STATUS 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_PREFERRED_STATUS
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 13ab53cee6091120320c1282aeb7df32c7147e9b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830942"
---
# <a name="ksproperty_audio_preferred_status"></a>KSPROPERTY\_音频\_首选\_状态


KSPROPERTY\_音频\_首选\_状态属性告知设备是系统的首选音频设备。

## <span id="ddk_ksproperty_audio_preferred_status_ks"></span><span id="DDK_KSPROPERTY_AUDIO_PREFERRED_STATUS_KS"></span>


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
<td align="left"><p>无</p></td>
<td align="left"><p>“是”</p></td>
<td align="left"><p>Filter</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/ff564262(v=vs.85)" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))"><strong>KSPROPERTY</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_preferred_status" data-raw-source="[&lt;strong&gt;KSAUDIO_PREFERRED_STATUS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_preferred_status)"><strong>KSAUDIO_PREFERRED_STATUS</strong></a></p></td>
</tr>
</tbody>
</table>

 

属性值（操作数据）是 KSAUDIO 类型的结构，\_首选设备类型的首选\_状态，以及设备是选择还是取消选择为该设备类型的首选设备。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_音频\_首选\_状态属性请求返回状态\_"成功" 以指示已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

[SysAudio 系统驱动程序](https://docs.microsoft.com/windows-hardware/drivers/audio/kernel-mode-wdm-audio-components#sysaudio-system-driver)使用此属性来通知波形播放、波形记录、MIDI 或混音器设备被选择为新的首选设备，或取消选择以前选择的首选设备时。

有关首选设备的信息，请参阅[**SetupPreferredAudioDevices**](setuppreferredaudiodevices.md)。

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


[**KSPROPERTY**](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))

[**KSAUDIO\_首选\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_preferred_status)

[**SetupPreferredAudioDevices**](setuppreferredaudiodevices.md)

 

 






