---
title: 微型端口接口
description: 微型端口接口
ms.assetid: 50b92adc-a63c-4242-9ec9-4d97151f0f91
keywords:
- 音频微型端口驱动程序 WDK，接口
- 微型端口驱动程序 WDK 音频，接口
- 微型端口接口 WDK 音频
- 端口类驱动程序 WDK 音频
- PortCls WDK 音频，接口
- 接口 WDK 音频
- 内置端口驱动程序 WDK 音频
- 流接口 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 51e8e9a36ff094d360d1f654afe34780c70ce2c0
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90101800"
---
# <a name="miniport-interfaces"></a>微型端口接口


## <span id="miniport_interfaces"></span><span id="MINIPORT_INTERFACES"></span>


如 [支持设备](supporting-a-device.md)中所述，PortCls 系统驱动程序提供了一套内置的端口驱动程序，用于管理 WAVE 和 MIDI 设备。 若要使用其中一个端口驱动程序来管理特定类型的音频设备，适配器驱动程序必须提供相应的微型端口驱动程序，以便通过管理设备的所有硬件相关功能来补充端口驱动程序。

本部分介绍以下微型端口驱动程序类型：

[WaveRT 微型端口驱动程序](wavert-miniport-driver.md)

对 WaveRT 端口驱动程序进行了补充，方法是管理波形呈现的硬件相关功能，或捕获使用循环缓冲区的音频数据的设备。

[拓扑微型端口驱动程序](topology-miniport-driver.md)

通过管理各种硬件控制来补充拓扑端口驱动程序 (例如，音频适配器混音器电路中的音量级别) 。

[MIDI 微型端口驱动程序](midi-miniport-driver.md)

通过管理简单 MIDI 设备的硬件相关功能来补充 MIDI 端口驱动程序。

[DMus 微型端口驱动程序](dmus-miniport-driver.md)

通过管理高级 MIDI 设备的硬件相关功能来补充 Dmu 端口驱动程序。

每个端口驱动程序都实现一个 **IPortXxx** 接口，该接口将呈现给微型端口驱动程序。 同时，微型端口驱动程序必须实现 **IMiniportXxx** 接口，端口驱动程序使用该接口与微型端口驱动程序通信。 下表显示了每种设备类型的 **IPortXxx** 接口和对应的 **IMiniportXxx** 接口。

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
<td align="left"><p><a href="/windows-hardware/drivers/ddi/portcls/nn-portcls-iportwavecyclic" data-raw-source="[IPortWaveCyclic](/windows-hardware/drivers/ddi/portcls/nn-portcls-iportwavecyclic)">IPortWaveCyclic</a></p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavecyclic" data-raw-source="[IMiniportWaveCyclic](/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavecyclic)">IMiniportWaveCyclic</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>WavePci</p></td>
<td align="left"><p><a href="/previous-versions/windows/hardware/drivers/ff536905(v=vs.85)" data-raw-source="[IPortWavePci](/previous-versions/windows/hardware/drivers/ff536905(v=vs.85))">IPortWavePci</a></p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavepci" data-raw-source="[IMiniportWavePci](/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavepci)">IMiniportWavePci</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>WaveRT</p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/portcls/nn-portcls-iportwavert" data-raw-source="[IPortWaveRT](/windows-hardware/drivers/ddi/portcls/nn-portcls-iportwavert)">IPortWaveRT</a></p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavert" data-raw-source="[IMiniportWaveRT](/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavert)">IMiniportWaveRT</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>拓扑</p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/portcls/nn-portcls-iporttopology" data-raw-source="[IPortTopology](/windows-hardware/drivers/ddi/portcls/nn-portcls-iporttopology)">IPortTopology</a></p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiporttopology" data-raw-source="[IMiniportTopology](/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiporttopology)">IMiniportTopology</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>MIDI</p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/portcls/nn-portcls-iportmidi" data-raw-source="[IPortMidi](/windows-hardware/drivers/ddi/portcls/nn-portcls-iportmidi)">IPortMidi</a></p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportmidi" data-raw-source="[IMiniportMidi](/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportmidi)">IMiniportMidi</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>DirectMusic</p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-iportdmus" data-raw-source="[IPortDMus](/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-iportdmus)">IPortDMus</a></p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-iminiportdmus" data-raw-source="[IMiniportDMus](/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-iminiportdmus)">IMiniportDMus</a></p></td>
</tr>
</tbody>
</table>

 

在上表中，所有 **IPortXxx** 接口派生自基接口 [IPort](/windows-hardware/drivers/ddi/portcls/nn-portcls-iport)，所有 **IMiniportXxx** 接口派生自 [IMiniport](/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiport)。

