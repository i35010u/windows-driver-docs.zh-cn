---
title: 音乐技术 GUID
description: 音乐技术 GUID
ms.assetid: 3b7c2907-e67f-458e-809d-080dcc30be1a
keywords:
- WDM 音频扩展 WDK，音乐技术 Guid
- 音乐技术 Guid WDK 音频
- KSDATARANGE_MUSIC 结构
- 合成 WDK 音频，技术 Guid
- MIDI 流数据格式 WDK 音频
- DirectMusic WDK 音频，流数据格式
- Dmu 流数据格式 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6db15b4a05ebe5e55030b3e2dc144be852626aaa
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89210559"
---
# <a name="music-technology-guids"></a>音乐技术 GUID


## <span id="music_technology_guids"></span><span id="MUSIC_TECHNOLOGY_GUIDS"></span>


MIDI 或 Dmu 微型端口驱动程序必须指定其每个插针都能够处理的流格式范围。 如 [Pin 工厂](pin-factories.md)中所述，驱动程序将此信息指定为一个或多个数据范围描述符的数组，其中每个描述符都是 [**KSDATARANGE \_ 音乐**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksdatarange_music)类型的结构。 此结构的 **技术** 成员指示 MIDI 或 DirectMusic 设备使用哪种类型的合成器技术。 微型端口驱动程序可以将 **技术** 成员设置为下表中所示的某个 GUID 值 (左栏) 。

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
<td align="left"><p>设备是 MPU-401 设备。</p></td>
</tr>
<tr class="even">
<td align="left"><p>KSMUSIC_TECHNOLOGY_SYNTH</p></td>
<td align="left"><p>MOD_SYNTH</p></td>
<td align="left"><p>设备是合成器。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>KSMUSIC_TECHNOLOGY_SQSYNTH</p></td>
<td align="left"><p>MOD_SQSYNTH</p></td>
<td align="left"><p>设备是一个平方英寸合成器。</p></td>
</tr>
<tr class="even">
<td align="left"><p>KSMUSIC_TECHNOLOGY_FMSYNTH</p></td>
<td align="left"><p>MOD_FMSYNTH</p></td>
<td align="left"><p>设备是 FM 合成器。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>KSMUSIC_TECHNOLOGY_MAPPER</p></td>
<td align="left"><p>MOD_MAPPER</p></td>
<td align="left"><p>设备是 Microsoft MIDI 映射器。</p></td>
</tr>
<tr class="even">
<td align="left"><p>KSMUSIC_TECHNOLOGY_WAVETABLE</p></td>
<td align="left"><p>MOD_WAVETABLE</p></td>
<td align="left"><p>设备是硬件 wavetable 合成器。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>KSMUSIC_TECHNOLOGY_SWSYNTH</p></td>
<td align="left"><p>MOD_SWSYNTH</p></td>
<td align="left"><p>设备是软件合成器。</p></td>
</tr>
</tbody>
</table>

 

**MidiOutGetDevCaps**函数将它从驱动程序接收的技术 GUID 转换为其将其输出到调用方的 MIDIOUTCAPS 结构的**wTechnology**成员写入的索引。 上表显示与每个技术 GUID 相对应 (居中列) 的 **wTechnology** 值。 有关 **midiOutGetDevCaps** 和 MIDIOUTCAPS 的详细信息，请参阅 Microsoft Windows SDK 文档。

枚举设备时，使用 Windows 多媒体 midiOut 或 midiIn API 的 MIDI 应用程序可以看到 MIDI pin，而不是 DirectMusic pin。 DirectMusic 应用程序可以看到 MIDI 和 DirectMusic pin。 MIDI 或 Dmu 微型端口驱动程序通过将 pin 的数据范围内的子类型 GUID 设置为 KSDATAFORMAT 子类型 midi 来识别 MIDI pin \_ \_ 。 Dmu 微型端口驱动程序通过将子类型 GUID 设置为 KSDATAFORMAT 子类型 DirectMusic 来识别 DirectMusic pin \_ \_ 。 有关 MIDI 和 DirectMusic pin 的数据范围示例，请参阅 [Midi Stream 数据范围](midi-stream-data-range.md) 和 [DirectMusic 流数据范围](directmusic-stream-data-range.md)。

如 [MIDI 和 DirectMusic 筛选器](midi-and-directmusic-filters.md)中所述，适配器驱动程序调用 [**PcNewMiniport**](/windows-hardware/drivers/ddi/portcls/nf-portcls-pcnewminiport) 函数在 Portcls.sys 中创建一个系统提供的微端口驱动程序的实例。 调用方指定下表中的一个驱动程序 Guid 来指定要实例化的小型端口驱动程序。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">驱动程序 GUID</th>
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

 

上表的右列指出了相应微型端口驱动程序在其 pin 的数据范围内指定的技术 GUID。 例如，FmSynth 微型端口驱动程序将技术 GUID KSMUSIC \_ 技术 \_ FmSynth 分配到其 pin。

某些 wavetable 合成器设备会将其自身公开给应用程序，如 MPU-401 设备 (技术 GUID KSMUSIC \_ 技术 \_ 端口) 。 在没有外部合成器的情况下，它们可以通过 wavetable 合成器播放原始 MIDI 字节流。

但是，在 \_ \_ 选择默认 () 首选的 "MIDI 播放" 设备时，midiOut API 首选 wavetable 合成器设备 (与技术 GUID KSMUSIC 技术 wavetable) 。 它显式避免将 MPU-401 设备选为默认设备。

若要使自身成为默认设备的资格，可以播放 raw MIDI 的 wavetable 设备应公开为 wavetable 设备，而不是 MPU-401 设备。 但是，如果适配器驱动程序使用系统提供的 MPU-401 微型端口驱动程序 DMusUART 来管理其 wavetable 合成器设备，则该小型端口驱动程序会将技术 GUID KSMUSIC \_ 技术端口静态分配 \_ 给其 pin。

通过调用 [**IMusicTechnology：： SetTechnology**](/windows-hardware/drivers/ddi/portcls/nf-portcls-imusictechnology-settechnology) 方法，适配器驱动程序可以覆盖微型端口驱动程序的数据范围内的技术 guid。 在下面的代码示例中，适配器驱动程序将 DMusUART 微型端口驱动程序的数据范围中的技术 GUID 从其默认值 KSMUSIC \_ 技术 \_ 端口更改为值 KSMUSIC \_ 技术 \_ WAVETABLE。 使用此新设置，MPU 的 wavetable 设备可由 midiOut API 作为默认的 MIDI 设备进行选择。

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

如前面的代码示例的注释中所示，适配器驱动程序应在调用端口驱动程序的方法之前调用 [**SetTechnology**](/windows-hardware/drivers/ddi/portcls/nf-portcls-imusictechnology-settechnology) ， `Init` (后者进而调用微型端口驱动程序的 `Init` 方法) 。 系统提供的 DMusUART 和 UART 微型端口驱动程序都支持 [IMusicTechnology](/windows-hardware/drivers/ddi/portcls/nn-portcls-imusictechnology) 接口。 对于其他微型端口驱动程序，支持 IMusicTechnology 是可选的。 有关详细信息，请参阅 Microsoft Windows 驱动程序工具包 (WDK) 中的 DMusUART 示例音频驱动程序中的 **SetTechnology** 方法的实现。

 

