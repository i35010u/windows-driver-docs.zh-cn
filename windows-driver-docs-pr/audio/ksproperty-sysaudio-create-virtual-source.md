---
title: KSPROPERTY\_SYSAUDIO\_创建\_虚拟\_源
description: KSPROPERTY\_SYSAUDIO\_创建\_虚拟\_SOURCE 属性创建新的虚拟源。
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
ms.openlocfilehash: 272c9f1d3ca5f97e090a7576f44b71b90539c2cf
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832729"
---
# <a name="ksproperty_sysaudio_create_virtual_source"></a>KSPROPERTY\_SYSAUDIO\_创建\_虚拟\_源


KSPROPERTY\_SYSAUDIO\_创建\_虚拟\_SOURCE 属性创建新的虚拟源。

## <span id="ddk_ksproperty_sysaudio_create_virtual_source_ks"></span><span id="DDK_KSPROPERTY_SYSAUDIO_CREATE_VIRTUAL_SOURCE_KS"></span>


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
<td align="left"><p>无</p></td>
<td align="left"><p>Filter</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-sysaudio_create_virtual_source" data-raw-source="[&lt;strong&gt;SYSAUDIO_CREATE_VIRTUAL_SOURCE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-sysaudio_create_virtual_source)"><strong>SYSAUDIO_CREATE_VIRTUAL_SOURCE</strong></a></p></td>
<td align="left"><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

属性说明符（实例数据）是 SYSAUDIO 类型的结构\_创建\_虚拟\_源，用于指定虚拟源的 pin 类别和端口名称 Guid。

属性值（操作数据）是包含虚拟源索引的 ULONG 变量。 SysAudio 生成此索引以标识新的虚拟源。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_SYSAUDIO\_创建\_虚拟\_源属性请求返回状态\_SUCCESS 以指示已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

此属性用于创建混音器线虚拟源，例如音量或静音控制。

如果 SysAudio 已使用相同的 pin 类别和端口名称 Guid 创建了虚拟源，则 KSPROPERTY\_SYSAUDIO\_CREATE\_VIRTUAL\_源 get 属性请求检索现有虚拟源的索引。 否则，请求将生成新的虚拟源索引并输出该值。

在 SysAudio 为虚拟源分配索引后， [**KSPROPERTY\_SysAudio\_附加\_虚拟\_源**](ksproperty-sysaudio-attach-virtual-source.md)集-属性请求可用于将该虚拟源附加到虚拟音频设备上的 pin 实例。

用户通过 SndVol32 应用程序控制各种音频源的音量级别。 这些源包括波形输出设备、MIDI 合成器、CD 播放器和线路输入插孔。 SndVol32 使用 Windows 多媒体**waveOut**_Xxx_、 **midiOut**_xxx_和**aux**_Xxx_函数来控制这些源的卷级别。 有关 Windows 多媒体功能的详细信息，请参阅 Microsoft Windows SDK 文档。

SysAudio 截获对这些设备进行的卷更改，并将这些更改应用到其虚拟源。 例如，如果将 MIDI 文件转换为波形数据的软件 MIDI 合成器连接到某个虚拟音频设备的波形渲染插针，则 SysAudio 会*将 midiOut*卷更改）。 同样，如果将数字音频从 CD 播放机转换为波形数据的[Redbook 系统驱动程序](https://docs.microsoft.com/windows-hardware/drivers/audio/kernel-mode-wdm-audio-components#redbook-system-driver)已连接到某个虚拟音频设备的波形渲染插针，则 SysAudio 会应用 AUXCAPS\_CDAUDIO 对该 pin 进行的卷更改。 有关 AUXCAPS\_CDAUDIO 结构的详细信息，请参阅 Windows SDK 文档。

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


[**SYSAUDIO\_创建\_虚拟\_源**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-sysaudio_create_virtual_source)

[**KSPROPERTY\_SYSAUDIO\_附加\_虚拟\_源**](ksproperty-sysaudio-attach-virtual-source.md)

 

 






