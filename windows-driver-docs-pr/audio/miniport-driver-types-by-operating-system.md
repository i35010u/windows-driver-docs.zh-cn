---
title: 按操作系统划分的微型端口驱动程序类型
description: 按操作系统划分的微型端口驱动程序类型
ms.assetid: 6ab0e4e4-5118-4df5-ba4e-7da66ce5880d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 20895e85c14ba771131e098bb1e1e6eb98c17377
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89211369"
---
# <a name="miniport-driver-types-by-operating-system"></a>按操作系统划分的微型端口驱动程序类型


开发自己的音频驱动程序时，必须确定驱动程序是否将与 PortCls 系统驱动程序一起使用 ( # A0) 或 AVStream 类系统驱动程序。 如果视频流不是必需的，则可能需要使用适用于 PortCls 系统驱动程序的驱动程序。 有关这两种类型的系统驱动程序的详细信息，请参阅 [Port Class 简介](introduction-to-port-class.md) 和 [AVStream 概述](../stream/avstream-overview.md) 主题。

PortCls 系统驱动程序 ( # A0) 提供多个内置的端口驱动程序来支持呈现和捕获 wave 和 MIDI 流的音频设备。 通常，端口驱动程序为每类音频 subdevice 提供大多数功能。

每个端口驱动程序与微型端口驱动程序一起工作。 微型端口驱动程序管理波形呈现设备或 wave 捕获设备的硬件相关功能。 换句话说，微型端口驱动程序为特定于第三方音频设备硬件的功能提供支持。

你开发的微型端口驱动程序的类型取决于你的目标 Windows 操作系统和音频设备提供的功能。 下表显示了不同类型的微型端口驱动程序以及支持它们的 Windows 操作系统。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">微型端口驱动程序</th>
<th align="left">Windows XP</th>
<th align="left">Windows Vista</th>
<th align="left">Windows 7</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="wavecyclic-miniport-driver.md" data-raw-source="[WaveCyclic](wavecyclic-miniport-driver.md)">WaveCyclic</a></p></td>
<td align="left"><p>x</p></td>
<td align="left"><p>x</p></td>
<td align="left"><p>x</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wavepci-miniport-driver.md" data-raw-source="[WavePci](wavepci-miniport-driver.md)">WavePci</a></p></td>
<td align="left"><p>x</p></td>
<td align="left"><p>x</p></td>
<td align="left"><p>x</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wavert-miniport-driver.md" data-raw-source="[WaveRT](wavert-miniport-driver.md)">WaveRT</a></p></td>
<td align="left"></td>
<td align="left"><p>x</p></td>
<td align="left"><p>x</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="topology-miniport-driver.md" data-raw-source="[Topology](topology-miniport-driver.md)">拓扑</a></p></td>
<td align="left"><p>x</p></td>
<td align="left"><p>x</p></td>
<td align="left"><p>x</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="midi-miniport-driver.md" data-raw-source="[MIDI](midi-miniport-driver.md)">MIDI</a></p></td>
<td align="left"><p>x</p></td>
<td align="left"><p>x</p></td>
<td align="left"><p>x</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="dmus-miniport-driver.md" data-raw-source="[DMus](dmus-miniport-driver.md)">Dmu</a></p></td>
<td align="left"><p>x</p></td>
<td align="left"><p>x</p></td>
<td align="left"><p>x</p></td>
</tr>
</tbody>
</table>

 

每个端口驱动程序都实现一个接口，该接口提供给微型端口驱动程序。 若要与端口驱动程序通信，微型端口驱动程序还必须实现接口。 有关微型端口驱动程序实现的接口的详细信息，请参阅 [微型端口接口](miniport-interfaces.md)。

**注意**   为 Windows Vista 和更高版本的操作系统开发音频驱动程序时，请注意以下事项：
-   不能为 WaveCyclic 或基于 WavePci 的音频驱动程序获得徽标资格。

-   不支持 Dmu 的内核模式软件合成程序。 但是，提供对硬件 MIDI i/o 的支持。

 

 

