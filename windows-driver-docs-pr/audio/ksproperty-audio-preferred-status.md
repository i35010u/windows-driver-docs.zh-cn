---
title: KSPROPERTY\_音频\_首选\_状态
description: KSPROPERTY\_音频\_首选\_状态属性会通知设备它是系统的首选音频设备。
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
ms.openlocfilehash: b2bcbcf8f0facc1830f7d3309fcc2c482237086a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332948"
---
# <a name="kspropertyaudiopreferredstatus"></a>KSPROPERTY\_音频\_首选\_状态


KSPROPERTY\_音频\_首选\_状态属性会通知设备它是系统的首选音频设备。

## <span id="ddk_ksproperty_audio_preferred_status_ks"></span><span id="DDK_KSPROPERTY_AUDIO_PREFERRED_STATUS_KS"></span>


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
<td align="left"><p>否</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>Filter</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564262" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564262)"><strong>KSPROPERTY</strong></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff537093" data-raw-source="[&lt;strong&gt;KSAUDIO_PREFERRED_STATUS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537093)"><strong>KSAUDIO_PREFERRED_STATUS</strong></a></p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 是一种结构的类型 KSAUDIO\_首选\_首选的设备和设备是否选中或取消选择的类型指定为适用于该设备类型的首选设备的状态。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_音频\_PREFERRED\_状态属性请求返回状态\_成功以指示已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

[SysAudio 系统驱动程序](https://msdn.microsoft.com/library/windows/hardware/ff537039#sysaudio-system-driver)使用此属性以通知批播放波形记录、 MIDI 或 mixer 设备选择为新的首选设备时或当之前选择首选设备处于取消选中状态。

有关首选的设备的信息，请参阅[ **SetupPreferredAudioDevices**](setuppreferredaudiodevices.md)。

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


[**KSPROPERTY**](https://msdn.microsoft.com/library/windows/hardware/ff564262)

[**KSAUDIO\_PREFERRED\_STATUS**](https://msdn.microsoft.com/library/windows/hardware/ff537093)

[**SetupPreferredAudioDevices**](setuppreferredaudiodevices.md)

 

 






