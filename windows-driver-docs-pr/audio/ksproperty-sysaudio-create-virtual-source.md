---
title: KSPROPERTY \_ SYSAUDIO \_ 创建 \_ 虚拟 \_ 源
description: KSPROPERTY \_ SYSAUDIO \_ CREATE \_ virtual \_ source 属性创建新的虚拟源。
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
ms.openlocfilehash: 5b6efc934e13bad1ff3b969cdadf420cd2926d91
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96801159"
---
# <a name="ksproperty_sysaudio_create_virtual_source"></a>KSPROPERTY \_ SYSAUDIO \_ 创建 \_ 虚拟 \_ 源


KSPROPERTY \_ SYSAUDIO \_ CREATE \_ virtual \_ source 属性创建新的虚拟源。

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
<th align="left">获取</th>
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
<td align="left"><p>筛选器</p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-sysaudio_create_virtual_source" data-raw-source="[&lt;strong&gt;SYSAUDIO_CREATE_VIRTUAL_SOURCE&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-sysaudio_create_virtual_source)"><strong>SYSAUDIO_CREATE_VIRTUAL_SOURCE</strong></a></p></td>
<td align="left"><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

 (实例数据) 的属性描述符是 SYSAUDIO CREATE virtual source 类型的结构，用于 \_ \_ \_ 指定虚拟源的 pin 类别和端口名称 guid。

 (操作数据) 的属性值是包含虚拟源索引的 ULONG 变量。 SysAudio 生成此索引以标识新的虚拟源。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY \_ SYSAUDIO \_ CREATE \_ VIRTUAL \_ SOURCE property 请求返回状态 \_ SUCCESS 以指示该请求已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

此属性用于创建混音器线虚拟源，例如音量或静音控制。

如果 SysAudio 已使用相同的 pin 类别和 pin 名称 Guid 创建了一个虚拟源，则 KSPROPERTY \_ SysAudio \_ CREATE \_ virtual \_ source get property 请求会检索现有虚拟源的索引。 否则，请求将生成新的虚拟源索引并输出该值。

在 SysAudio 为虚拟源分配索引后，可以使用 [**KSPROPERTY \_ SysAudio \_ 附加 \_ 虚拟 \_ 源**](ksproperty-sysaudio-attach-virtual-source.md)集-属性请求将该虚拟源附加到虚拟音频设备上的 pin 实例。

用户通过 SndVol32 应用程序控制各种音频源的音量级别。 这些源包括波形输出设备、MIDI 合成器、CD 播放器和线路输入插孔。 SndVol32 使用 Windows 多媒体 **waveOut**_Xxx_、 **midiOut**_xxx_ 和 **aux**_Xxx_ 函数来控制这些源的卷级别。 有关 Windows 多媒体功能的详细信息，请参阅 Microsoft Windows SDK 文档。

SysAudio 截获对这些设备进行的卷更改，并将这些更改应用到其虚拟源。 例如，如果将 MIDI 文件转换为波形数据的软件 MIDI 合成器连接到某个虚拟音频设备的波形渲染插针，则 SysAudio 会将 midiOut *Xxx* 卷更改应用到 pin (而不是 **waveOut**_Xxx_ 的卷更改) 。 同样，如果将数字音频从 CD 播放机转换为波形数据的 [Redbook 系统驱动程序](./kernel-mode-wdm-audio-components.md#redbook-system-driver)已连接到某个虚拟音频设备的波形渲染插针，则 SysAudio 会将 AUXCAPS \_ CDAUDIO 批量更改应用到该 pin。 有关 AUXCAPS CDAUDIO 结构的详细信息 \_ ，请参阅 Windows SDK 文档。

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

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**SYSAUDIO \_ 创建 \_ 虚拟 \_ 源**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-sysaudio_create_virtual_source)

[**KSPROPERTY \_ SYSAUDIO \_ 附加 \_ 虚拟 \_ 源**](ksproperty-sysaudio-attach-virtual-source.md)

