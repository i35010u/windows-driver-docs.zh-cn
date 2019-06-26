---
title: 微型端口接口
description: 微型端口接口
ms.assetid: 50b92adc-a63c-4242-9ec9-4d97151f0f91
keywords:
- 音频的微型端口驱动程序 WDK，接口
- 微型端口驱动程序 WDK 音频，接口
- 微型端口接口 WDK 音频
- 端口类驱动程序 WDK 音频
- PortCls WDK 音频，接口
- 接口 WDK 音频
- 内置端口驱动程序 WDK 音频
- WDK 音频进行流式处理接口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c05a51cab5a86d874bc172190782434e6a20aa86
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363211"
---
# <a name="miniport-interfaces"></a>微型端口接口


## <span id="miniport_interfaces"></span><span id="MINIPORT_INTERFACES"></span>


如中所述[支持设备](supporting-a-device.md)，PortCls 系统驱动程序提供了一组内置端口驱动程序管理批和 MIDI 设备。 若要使用这些端口驱动程序之一来管理特定类型的音频设备，适配器驱动程序必须提供相应的微型端口驱动程序的补充端口驱动程序通过管理设备的所有依赖于硬件的函数。

本部分介绍以下微型端口驱动程序类型：

[WaveRT 微型端口驱动程序](wavert-miniport-driver.md)

通过管理的音频数据使用循环缓冲区的批呈现或捕获设备依赖于硬件的函数补充 WaveRT 端口驱动程序。

[拓扑微型端口驱动程序](topology-miniport-driver.md)

在音频适配器 mixer 电路中通过管理各种硬件控件 （例如，卷级别） 来补充拓扑端口驱动程序。

[MIDI 微型端口驱动程序](midi-miniport-driver.md)

通过管理简单 MIDI 设备依赖于硬件的函数补充 MIDI 端口驱动程序。

[Dmu 微型端口驱动程序](dmus-miniport-driver.md)

补充 Dmu 端口驱动程序通过管理高级 MIDI 设备的硬件相关的函数。

每个端口驱动程序实现**IPortXxx**接口，它提供给微型端口驱动程序。 反过来，微型端口驱动程序必须实现**IMiniportXxx**端口驱动程序使用与微型端口驱动程序进行通信的接口。 下表显示**IPortXxx**接口和相应**IMiniportXxx**每种设备类型的接口。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">设备类型</th>
<th align="left">端口驱动程序接口</th>
<th align="left">微型端口驱动程序接口</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>WaveCyclic</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iportwavecyclic" data-raw-source="[IPortWaveCyclic](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iportwavecyclic)">IPortWaveCyclic</a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iminiportwavecyclic" data-raw-source="[IMiniportWaveCyclic](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iminiportwavecyclic)">IMiniportWaveCyclic</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>WavePci</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff536905(v=vs.85)" data-raw-source="[IPortWavePci](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff536905(v=vs.85))">IPortWavePci</a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iminiportwavepci" data-raw-source="[IMiniportWavePci](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iminiportwavepci)">IMiniportWavePci</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>WaveRT</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iportwavert" data-raw-source="[IPortWaveRT](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iportwavert)">IPortWaveRT</a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iminiportwavert" data-raw-source="[IMiniportWaveRT](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iminiportwavert)">IMiniportWaveRT</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>拓扑</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iporttopology" data-raw-source="[IPortTopology](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iporttopology)">IPortTopology</a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iminiporttopology" data-raw-source="[IMiniportTopology](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iminiporttopology)">IMiniportTopology</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>MIDI</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iportmidi" data-raw-source="[IPortMidi](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iportmidi)">IPortMidi</a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iminiportmidi" data-raw-source="[IMiniportMidi](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iminiportmidi)">IMiniportMidi</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>DirectMusic</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nn-dmusicks-iportdmus" data-raw-source="[IPortDMus](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nn-dmusicks-iportdmus)">IPortDMus</a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nn-dmusicks-iminiportdmus" data-raw-source="[IMiniportDMus](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nn-dmusicks-iminiportdmus)">IMiniportDMus</a></p></td>
</tr>
</tbody>
</table>

 

在上表中，所有**IPortXxx**接口派生自基接口[IPort](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iport)，和全部**IMiniportXxx**接口派生自[IMiniport](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iminiport)。

 

 




