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
ms.openlocfilehash: b66c0cef0e2ca0e50e8f95f7fd6a8ed307ff69cf
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548046"
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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff536899" data-raw-source="[IPortWaveCyclic](https://msdn.microsoft.com/library/windows/hardware/ff536899)">IPortWaveCyclic</a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff536714" data-raw-source="[IMiniportWaveCyclic](https://msdn.microsoft.com/library/windows/hardware/ff536714)">IMiniportWaveCyclic</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>WavePci</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff536905" data-raw-source="[IPortWavePci](https://msdn.microsoft.com/library/windows/hardware/ff536905)">IPortWavePci</a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff536724" data-raw-source="[IMiniportWavePci](https://msdn.microsoft.com/library/windows/hardware/ff536724)">IMiniportWavePci</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>WaveRT</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff536920" data-raw-source="[IPortWaveRT](https://msdn.microsoft.com/library/windows/hardware/ff536920)">IPortWaveRT</a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff536737" data-raw-source="[IMiniportWaveRT](https://msdn.microsoft.com/library/windows/hardware/ff536737)">IMiniportWaveRT</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>拓扑</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff536896" data-raw-source="[IPortTopology](https://msdn.microsoft.com/library/windows/hardware/ff536896)">IPortTopology</a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff536712" data-raw-source="[IMiniportTopology](https://msdn.microsoft.com/library/windows/hardware/ff536712)">IMiniportTopology</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>MIDI</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff536891" data-raw-source="[IPortMidi](https://msdn.microsoft.com/library/windows/hardware/ff536891)">IPortMidi</a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff536703" data-raw-source="[IMiniportMidi](https://msdn.microsoft.com/library/windows/hardware/ff536703)">IMiniportMidi</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>DirectMusic</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff536879" data-raw-source="[IPortDMus](https://msdn.microsoft.com/library/windows/hardware/ff536879)">IPortDMus</a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff536699" data-raw-source="[IMiniportDMus](https://msdn.microsoft.com/library/windows/hardware/ff536699)">IMiniportDMus</a></p></td>
</tr>
</tbody>
</table>

 

在上表中，所有**IPortXxx**接口派生自基接口[IPort](https://msdn.microsoft.com/library/windows/hardware/ff536842)，和全部**IMiniportXxx**接口派生自[IMiniport](https://msdn.microsoft.com/library/windows/hardware/ff536698)。

 

 




