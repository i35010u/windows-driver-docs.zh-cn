---
title: 等时侦听的 IEEE 1394 设备的选项
description: 等时侦听的 IEEE 1394 设备的选项
ms.assetid: a369b7f0-be85-49f0-bb09-d07cbd3d3558
keywords:
- 同步 I/O WDK IEEE 1394 总线，侦听选项
- 侦听选项 WDK IEEE 1394 总线
- 基于数据包的 DMA WDK IEEE 1394 总线
- 基于流的 DMA WDK IEEE 1394 总线
- DMA 传输 WDK IEEE 1394 总线
- 数据包 DMA WDK IEEE 1394 总线
- 最小化数据包标头
- 标头 WDK IEEE 1394 总线
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f0f3a23f2d45c6d8b7f24114b059ef599cc3901c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555799"
---
# <a name="isochronous-listen-options-for-ieee-1394-devices"></a>等时侦听的 IEEE 1394 设备的选项





本部分介绍各种等时侦听选项。

### <a name="receiving-or-stripping-packet-headers"></a>接收或最小化数据包标头

主机控制器可能会或可能不会自动去除关闭同步数据包标头。 总线驱动程序设置的主机\_INFO\_支持\_RETURNING\_ISO\_HDR 标志**HostCapabilities**隶属[**获取\_本地\_主机\_INFO2** ](https://msdn.microsoft.com/library/windows/hardware/ff537147)结构，如果主机控制器是否执行*不*自动删除关闭同步数据包标头。

此外，主机控制器可能支持可配置最小化的标头。 总线驱动程序设置的主机\_INFO\_支持\_ISOCH\_STRIPPING 标志的 HostCapabilities 是否可以配置主机控制器去除标头。 若要实际配置主机控制器去除标头，该驱动程序提交[**请求\_ISOCH\_分配\_资源**](https://msdn.microsoft.com/library/windows/hardware/ff537649)与资源的请求\_条带\_其他\_QUADLETS 标志设置。 **NQuadletsToStrip**成员指定 quadlets 剥离开头的每个数据包的数目。 例如， **nQuadletsToStrip** = 1 会剥离同步数据包标头。

### <a name="stream-versus-packet-based-dma"></a>与基于数据包的 DMA Stream

基于流的和基于数据包的 DMA 策略需要基础主机控制器的支持。 所有主机控制器都支持至少一个 DMA 策略，并且 OHCI 符合主机控制器都支持这两个。

基于数据包的 DMA 和基于流的数字媒体适配器具有相似特征的所有数据包时的大小相同。 但 DMA 两个分类有明显不同的特征时的数据包大小而异。

在基于流的 DMA 主机控制器忽略数据包边界填充 I/O 缓冲区，使它将写入的数据中无间隔。 若要确定特定数据包的位置，您必须知道所有以前的数据包的长度。

在基于数据包的 DMA 中主机控制器将写入每次可缓存的只是一个同步数据包。 因此在数据包模式下，主控制器空间的数据写入，以便每个数据包在距离是最大数据包大小的整数倍的 I/O 缓冲区的开头处开始。 如果小于最大值是数据包的一个特定的数据包，位于该数据包的末尾和下一步的开始之间的数据是数据包的未定义。 因此小于最大大小的数据包时，就会浪费一些缓冲区空间。 例如，大到足以始终保留 10 个数据包的缓冲区包含十个数据包，即使某些数据包都不会小于允许的最大大小。

无论你选择哪个 DMA 模式下，某些设计折中应用。 例如，缓冲区大小的选择会影响你的设备，无论哪种 DMA 模式中，您将使用的性能。 大型缓冲区提供效率，因为避免一些与初始化大量的缓冲区关联的开销。 此外，减少缓冲区意味着更少 DMA 描述符所需。 但是，更大的缓冲区增加 I/O 操作的开始和在其中总线驱动程序通知功能驱动程序缓冲区已满的时刻之间的延迟。

如果主机控制器支持两种类型的 DMA，总线驱动程序将设置为默认为基于流的 DMA 主控制器。 若要将主机控制器重置为基于数据包的 DMA，驱动程序应设置资源\_使用\_数据包\_基于标志时分配的资源句柄。

驱动程序使用[**请求\_获取\_本地\_主机\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff537644)总线请求 (使用**u.GetLocalHostInformation.nLevel** IRB 成员 = GET\_主机\_功能) 来确定主控制器的特征。 总线驱动程序将返回[**获取\_本地\_主机\_INFO2** ](https://msdn.microsoft.com/library/windows/hardware/ff537147)结构和中的设置标志**HostCapabilities**若要指示主机控制器支持的成员：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>DMA 类型</th>
<th>HostCapabilities 标志</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>基于流的</p></td>
<td><p>HOST_INFO_STREAM_BASED</p></td>
</tr>
<tr class="even">
<td><p>packet-based</p></td>
<td><p>HOST_INFO_PACKET_BASED</p></td>
</tr>
</tbody>
</table>

 

 

 




