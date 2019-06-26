---
title: 按操作系统划分的微型端口驱动程序类型
description: 按操作系统划分的微型端口驱动程序类型
ms.assetid: 6ab0e4e4-5118-4df5-ba4e-7da66ce5880d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bc014ba43a91072abf13884d64844e9255f2d96a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355353"
---
# <a name="miniport-driver-types-by-operating-system"></a>按操作系统划分的微型端口驱动程序类型


当开发音频驱动程序时，必须确定您的驱动程序将可结合使用 PortCls 系统驱动程序 (Portcls.sys) 或 AVStream 类系统驱动程序。 如果视频流不是必需的您可能需要的驱动程序，适用于 PortCls 系统驱动程序。 有关这两种类型的系统驱动程序的详细信息，请参阅[端口类简介](introduction-to-port-class.md)并[AVStream 概述](https://docs.microsoft.com/windows-hardware/drivers/stream/avstream-overview)主题。

PortCls 系统驱动程序 (Portcls.sys) 提供了几个内置端口驱动程序以支持的呈现和捕获批和 MIDI 流音频设备。 通常情况下，端口驱动程序提供了大多数的音频子每类功能。

每个端口驱动程序与协同工作的微型端口驱动程序。 微型端口驱动程序管理批呈现或批捕获设备的硬件相关的函数。 换而言之，微型端口驱动程序实现的特定于第三方音频设备的硬件的功能提供支持。

您开发的微型端口驱动程序的类型取决于目标 Windows 操作系统和音频设备提供的功能。 下表显示了不同类型的微型端口驱动程序和 Windows 操作系统支持它们。

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
<td align="left"><p><a href="dmus-miniport-driver.md" data-raw-source="[DMus](dmus-miniport-driver.md)">DMus</a></p></td>
<td align="left"><p>x</p></td>
<td align="left"><p>x</p></td>
<td align="left"><p>x</p></td>
</tr>
</tbody>
</table>

 

每个端口驱动程序实现的接口，它提供给微型端口驱动程序。 若要与端口驱动程序进行通信，微型端口驱动程序还必须实现一个接口。 有关接口的微型端口驱动程序实现的详细信息，请参阅[微型端口接口](miniport-interfaces.md)。

**请注意**  时适用于 Windows Vista 和更高版本的操作系统开发的音频驱动程序，请注意以下事项：
-   您不能获取 WaveCyclic-或 WavePci 徽标认证-基于音频驱动程序。

-   没有为 Dmu 为内核模式软件合成器支持。 但是，对于硬件 MIDI I/O 提供支持。

 

 

 




