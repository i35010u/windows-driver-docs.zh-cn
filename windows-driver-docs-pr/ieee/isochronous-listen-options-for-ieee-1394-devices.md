---
title: IEEE 1394 设备的常时等量侦听选项
description: IEEE 1394 设备的常时等量侦听选项
ms.assetid: a369b7f0-be85-49f0-bb09-d07cbd3d3558
keywords:
- 同步 i/o WDK IEEE 1394 总线，侦听选项
- 侦听选项 WDK IEEE 1394 总线
- 基于数据包的 DMA WDK IEEE 1394 总线
- 基于流的 DMA WDK IEEE 1394 总线
- DMA 传输 WDK IEEE 1394 总线
- 数据包 DMA WDK IEEE 1394 总线
- 去除数据包标头
- 标头 WDK IEEE 1394 总线
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0790f37e0ab98681f66f2b466819450db2017cea
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89382211"
---
# <a name="isochronous-listen-options-for-ieee-1394-devices"></a>IEEE 1394 设备的常时等量侦听选项





本部分介绍各种同步侦听选项。

### <a name="receiving-or-stripping-packet-headers"></a>接收或剥离数据包标头

主机控制器可能会也可能不会自动从同步数据包中去除标头。 \_ \_ \_ \_ \_ 如果主机控制器*不*会自动去除按同步数据包的标头，则总线驱动程序会将 "[**获取 \_ 本地 \_ 主机 \_ INFO2**](/windows-hardware/drivers/ddi/1394/ns-1394-_get_local_host_info2) " 结构的 " **HostCapabilities** " 成员的 ISO HDR 标志设置为 "主机信息"。

另外，主机控制器还可以支持可配置的标头。 \_ \_ \_ \_ 如果可以将主机控制器配置为去除标头，则总线驱动程序会将主机信息设置为支持 ISOCH 去除标志。 若要实际将主机控制器配置为包含标头，驱动程序将提交 [**请求 \_ ISOCH \_ 分配 \_ 资源**](https://msdn.microsoft.com/library/windows/hardware/ff537649) 请求， \_ 并 \_ \_ 设置其他 QUADLETS 标志。 **NQuadletsToStrip**成员指定要去除每个数据包开头的 quadlets 数。 例如， **nQuadletsToStrip** = 1 将去除同步数据包标头。

### <a name="stream-versus-packet-based-dma"></a>流与基于数据包的 DMA

基于流和数据包的 DMA 策略需要底层主机控制器的支持。 所有主机控制器都支持至少一个 DMA 策略，且 OHCI 兼容的主机控制器同时支持这两种策略。

当所有数据包大小相同时，基于数据包的 DMA 和基于流的 DMA 都具有类似的特征。 但当数据包大小变化时，这两种 DMA 的特征都非常不同。

在基于流的 DMA 中，主机控制器会在填充 i/o 缓冲区时忽略数据包边界，使其写入的数据中不存在任何空白。 若要确定特定包的位置，必须知道以前所有数据包的长度。

在基于数据包的 DMA 中，主机控制器只为每个缓冲区写入一个同步数据包。 因此，在数据包模式下，主机控制器会将其写入的数据空间空间，以便每个数据包从 i/o 缓冲区的开头开始，这是最大数据包大小的整数倍。 如果某个特定数据包的大小小于最大值，则该数据包末尾和下一数据包开头之间的数据是不确定的。 因此，当数据包小于最大值时，某些缓冲区空间会浪费。 例如，足以容纳10个数据包的缓冲区始终包含10个数据包，即使某些数据包小于允许的最大大小。

无论选择哪种 DMA 模式，都适用于某些设计折衷。 例如，无论使用哪种 DMA 模式，缓冲区大小的选择都会影响设备的性能。 较大的缓冲区可以提高效率，因为这样可以避免与初始化大量缓冲区相关的一些开销。 此外，缓冲区越少，要求的 DMA 描述符越少。 另一方面，较大的缓冲区增加了 i/o 操作开始与总线驱动程序通知函数驱动程序缓冲区已满的时刻之间的延迟。

如果主机控制器同时支持这两种类型的 DMA，则总线驱动程序会将主机控制器设置为默认的基于流的 DMA。 若要将主机控制器重置为基于数据包的 DMA，驱动程序应在 \_ \_ \_ 分配资源句柄时，将资源设置为使用基于数据包的标志。

驱动程序使用 [**请求 \_ 获取 \_ 本地 \_ 主机 \_ 信息**](https://msdn.microsoft.com/library/windows/hardware/ff537644) 总线请求 (，并使用 IRB = 获取主机功能) 的 **GetLocalHostInformation. nLevel** 成员 \_ \_ 确定主机控制器的特征。 总线驱动程序返回 " [**获取 \_ 本地 \_ 主机" \_ INFO2**](/windows-hardware/drivers/ddi/1394/ns-1394-_get_local_host_info2) 结构，并在 **HostCapabilities** 成员内设置标志，以指示主机控制器支持的内容：

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
<td><p>基于流</p></td>
<td><p>HOST_INFO_STREAM_BASED</p></td>
</tr>
<tr class="even">
<td><p>基于数据包</p></td>
<td><p>HOST_INFO_PACKET_BASED</p></td>
</tr>
</tbody>
</table>

 

 

