---
title: KSPROPERTY\_SYSAUDIO\_CREATE\_VIRTUAL\_SOURCE
description: KSPROPERTY\_SYSAUDIO\_创建\_虚拟\_SOURCE 属性创建一个新的虚拟源。
ms.assetid: 771c4084-8007-4280-8451-946a26182740
keywords:
- KSPROPERTY_SYSAUDIO_CREATE_VIRTUAL_SOURCE 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_SYSAUDIO_CREATE_VIRTUAL_SOURCE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1be154fb762023e50902139712d9416ff233f9d2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358718"
---
# <a name="kspropertysysaudiocreatevirtualsource"></a>KSPROPERTY\_SYSAUDIO\_CREATE\_VIRTUAL\_SOURCE


KSPROPERTY\_SYSAUDIO\_创建\_虚拟\_SOURCE 属性创建一个新的虚拟源。

## <span id="ddk_ksproperty_sysaudio_create_virtual_source_ks"></span><span id="DDK_KSPROPERTY_SYSAUDIO_CREATE_VIRTUAL_SOURCE_KS"></span>


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
<td align="left"><p>否</p></td>
<td align="left"><p>Filter</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-sysaudio_create_virtual_source" data-raw-source="[&lt;strong&gt;SYSAUDIO_CREATE_VIRTUAL_SOURCE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-sysaudio_create_virtual_source)"><strong>SYSAUDIO_CREATE_VIRTUAL_SOURCE</strong></a></p></td>
<td align="left"><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

属性描述符 （实例数据） 是一种结构的类型 SYSAUDIO\_创建\_虚拟\_指定虚拟源的 pin 类别和 pin 名称 Guid 的源。

属性值 （操作数据） 是包含虚拟源索引的 ULONG 变量。 SysAudio 生成此索引来标识新的虚拟源。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_SYSAUDIO\_创建\_虚拟\_源属性请求将返回状态\_成功以指示已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

此属性用于创建 mixer 行虚拟源，例如卷或将调节到静音控件。

如果使用的同一个 pin 类别和 pin 名称 Guid，KSPROPERTY SysAudio 已经创建虚拟源\_SYSAUDIO\_创建\_虚拟\_源属性 get 请求检索现有的索引虚拟源。 否则为请求生成新的虚拟源索引，并输出该值。

SysAudio 已分配给虚拟源的索引后[ **KSPROPERTY\_SYSAUDIO\_附加\_虚拟\_源**](ksproperty-sysaudio-attach-virtual-source.md)设置属性请求可用于将该虚拟源附加到虚拟的音频设备上的 pin 实例。

用户控制通过 SndVol32 应用程序的各种音频源的卷级别。 这些源包括 wave 输出设备、 MIDI 合成器、 CD 播放机和线路输入插孔。 SndVol32 使用 Windows 多媒体 **waveOut * * * Xxx*，**midiOut * * * Xxx*，和 **aux * * * Xxx*函数，以控制这些源的卷级别。 有关 Windows 多媒体函数的详细信息，请参阅 Microsoft Windows SDK 文档。

SysAudio 截获卷对这些设备所做的更改，并将其应用到其虚拟源。 例如，如果将一个 MIDI 文件转换为批数据的软件 MIDI 合成器连接到虚拟音频设备的批呈现引脚之一，SysAudio 适用 midiOut*Xxx*卷更改为固定 (而不是 **waveOut * * * Xxx*批量更改)。 同样，如果[Redbook 系统驱动程序](https://docs.microsoft.com/windows-hardware/drivers/audio/kernel-mode-wdm-audio-components#redbook-system-driver)，它将数字音频 CD 播放机从转换波形数据，为连接到虚拟音频设备的批呈现引脚之一，SysAudio 适用 AUXCAPS\_CDAUDIO 卷对 pin 的更改。 详细了解 AUXCAPS\_CDAUDIO 结构，请参阅 Windows SDK 文档。

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


[**SYSAUDIO\_CREATE\_VIRTUAL\_SOURCE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-sysaudio_create_virtual_source)

[**KSPROPERTY\_SYSAUDIO\_附加\_虚拟\_源**](ksproperty-sysaudio-attach-virtual-source.md)

 

 






