---
title: 音乐技术 GUID
description: 音乐技术 GUID
ms.assetid: 3b7c2907-e67f-458e-809d-080dcc30be1a
keywords:
- WDM 音频扩展 WDK，音乐技术 Guid
- 音乐技术 Guid WDK 音频
- KSDATARANGE_MUSIC 结构
- 合成器 WDK 音频，技术 Guid
- MIDI 数据格式 WDK 音频进行流式处理
- DirectMusic WDK 音频流数据格式
- Dmu 流式传输的数据格式 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8620aca8fe141af1adb0e9a02b73b167e2ca857b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563091"
---
# <a name="music-technology-guids"></a>音乐技术 GUID


## <span id="music_technology_guids"></span><span id="MUSIC_TECHNOLOGY_GUIDS"></span>


MIDI 或 Dmu 微型端口驱动程序必须指定每个其插针，都是能够处理的流格式的范围。 如中所述[Pin 工厂](pin-factories.md)，驱动程序的一个或多个数据范围说明符，其中每个是一种结构类型的数组的形式指定此信息[ **KSDATARANGE\_音乐**](https://msdn.microsoft.com/library/windows/hardware/ff537097). 此结构**技术**成员指示哪种类型的合成器技术的 MIDI 或 DirectMusic 设备使用。 微型端口驱动程序可以设置**技术**成员添加到表 （左列） 所示的 GUID 值之一。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">KSDATARANGE_MUSIC 技术 GUID</th>
<th align="left">MIDIOUTCAPS wTechnology 值</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>KSMUSIC_TECHNOLOGY_PORT</p></td>
<td align="left"><p>MOD_MIDIPORT</p></td>
<td align="left"><p>设备是 MPU 401 设备。</p></td>
</tr>
<tr class="even">
<td align="left"><p>KSMUSIC_TECHNOLOGY_SYNTH</p></td>
<td align="left"><p>MOD_SYNTH</p></td>
<td align="left"><p>设备是合成器。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>KSMUSIC_TECHNOLOGY_SQSYNTH</p></td>
<td align="left"><p>MOD_SQSYNTH</p></td>
<td align="left"><p>设备是正方形批合成器。</p></td>
</tr>
<tr class="even">
<td align="left"><p>KSMUSIC_TECHNOLOGY_FMSYNTH</p></td>
<td align="left"><p>MOD_FMSYNTH</p></td>
<td align="left"><p>设备是 FM 合成器。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>KSMUSIC_TECHNOLOGY_MAPPER</p></td>
<td align="left"><p>MOD_MAPPER</p></td>
<td align="left"><p>设备是 Microsoft MIDI 映射程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p>KSMUSIC_TECHNOLOGY_WAVETABLE</p></td>
<td align="left"><p>MOD_WAVETABLE</p></td>
<td align="left"><p>设备是硬件波表合成器。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>KSMUSIC_TECHNOLOGY_SWSYNTH</p></td>
<td align="left"><p>MOD_SWSYNTH</p></td>
<td align="left"><p>设备是软件合成器。</p></td>
</tr>
</tbody>
</table>

 

**MidiOutGetDevCaps**函数转换技术驱动程序从接收到的索引，它将写入到的 GUID **wTechnology**输出到 MIDIOUTCAPS 结构中的成员调用方。 以上表所示**wTechnology**对应于每种技术的 GUID 值 （中心列）。 有关详细信息**midiOutGetDevCaps**和 MIDIOUTCAPS，请参阅 Microsoft Windows SDK 文档。

枚举设备时，使用 Windows 多媒体 midiOut 或 midiIn API 的 MIDI 应用程序可以看到 MIDI pin，但不是 DirectMusic pin。 DirectMusic 应用程序可以看到 MIDI 和 DirectMusic 插针。 MIDI 或 Dmu 微型端口驱动程序通过 pin 的数据范围指向 KSDATAFORMAT 中设置的子类型 GUID 标识 MIDI pin\_子类型\_MIDI。 Dmu 微型端口驱动程序通过将 GUID 的子类型设置为 KSDATAFORMAT 标识 DirectMusic pin\_子类型\_DIRECTMUSIC。 有关 MIDI 和 DirectMusic 插针的数据范围的示例，请参阅[MIDI Stream 数据范围](midi-stream-data-range.md)并[DirectMusic Stream 数据范围](directmusic-stream-data-range.md)。

中所述[MIDI 和 DirectMusic 筛选器](midi-and-directmusic-filters.md)，适配器驱动程序调用[ **PcNewMiniport** ](https://msdn.microsoft.com/library/windows/hardware/ff537714)函数来创建一个系统提供微型端口的实例在 Portcls.sys 驱动程序。 调用方指定一个驱动程序的 Guid 在下表来指定要实例化的微型端口驱动程序。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">驱动程序的 GUID</th>
<th align="left">技术 GUID</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>CLSID_MiniportDriverDMusUART</strong></p></td>
<td align="left"><p>KSMUSIC_TECHNOLOGY_PORT</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>CLSID_MiniportDriverDMusUARTCapture</strong></p></td>
<td align="left"><p>KSMUSIC_TECHNOLOGY_PORT</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>CLSID_MiniportDriverFmSynth</strong></p></td>
<td align="left"><p>KSMUSIC_TECHNOLOGY_FMSYNTH</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>CLSID_MiniportDriverFmSynthWithVol</strong></p></td>
<td align="left"><p>KSMUSIC_TECHNOLOGY_FMSYNTH</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>CLSID_MiniportDriverUart</strong></p></td>
<td align="left"><p>KSMUSIC_TECHNOLOGY_PORT</p></td>
</tr>
</tbody>
</table>

 

上表的右侧列指示技术相应的微型端口驱动程序在其 pin 的数据范围内指定的 GUID。 例如，FmSynth 微型端口驱动程序将技术 GUID KSMUSIC\_技术\_FMSYNTH 到其插针。

某些波表合成器设备将自身公开给 MPU 401 设备的应用程序 (使用技术 GUID KSMUSIC\_技术\_端口)。 在没有外部合成器的情况下，它们是通过波表合成器播放的原始 MIDI 字节流。

但是，midiOut API 首选波表合成器设备 (使用技术 GUID KSMUSIC\_技术\_波表) 选择 （首选） 的默认 MIDI 播放设备时。 显式可避免选择为默认设备的 MPU 401 设备。

若要使自身可作为默认设备，可以播放原始 MIDI 波表设备应公开本身为波表设备，而不是 MPU 401 设备。 但是，如果适配器驱动程序使用系统提供 MPU 401 微型端口驱动程序，DMusUART，来管理其波表合成器设备，该微型端口驱动程序以静态方式分配技术 GUID KSMUSIC\_技术\_端口连接到其pin。

通过调用[ **IMusicTechnology::SetTechnology** ](https://msdn.microsoft.com/library/windows/hardware/ff536780)方法中，适配器驱动程序可以覆盖微型端口驱动程序的数据区域中的技术的 Guid。 在下面的代码示例中，适配器驱动程序技术 GUID DMusUART 微型端口驱动程序的数据范围中从其默认值更改，KSMUSIC\_技术\_端口的值 KSMUSIC\_技术\_波表。 使用此新设置，类似于 MPU 的波表设备都有资格 midiOut API 作为默认 MIDI 设备被选中。

```cpp
  // Create the miniport object.
  PUNKNOWN miniport;

  ntStatus = PcNewMiniport((PMINIPORT*)&miniport, CLSID_MiniportDriverDMusUART);

  // Query the miniport driver for the IMusicTechnology interface.
  IMusicTechnology* pMusicTechnology;

  if (NT_SUCCESS(ntStatus))
  {
      ntStatus = miniport->QueryInterface(IID_IMusicTechnology, (PVOID*)&pMusicTechnology);
  }

  // Set the Technology members in the DirectMusic data-range entries
  // for all the pins that are exposed by this miniport.
  // SetTechnology should be called before initializing the miniport.
  if (NT_SUCCESS(ntStatus))
  {
      ntStatus = pMusicTechnology->SetTechnology(&KSMUSIC_TECHNOLOGY_WAVETABLE);
  }
```

在前面的代码示例中的注释中所示，适配器驱动程序应调用[ **SetTechnology** ](https://msdn.microsoft.com/library/windows/hardware/ff536780)调用端口驱动程序之前`Init`方法 （后者，反过来，将调用微型端口驱动程序的`Init`方法)。 系统提供 DMusUART 和 UART 微型端口驱动程序同时支持[IMusicTechnology](https://msdn.microsoft.com/library/windows/hardware/ff536778)接口。 有关其他微型端口驱动程序，支持 IMusicTechnology 是可选的。 有关详细信息，请参阅的实现**SetTechnology** DMusUART 示例音频驱动程序中 Microsoft Windows Driver Kit (WDK) 中的方法。

 

 




