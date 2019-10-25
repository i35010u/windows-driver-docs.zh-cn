---
title: 设置 IEEE 1394 设备的常时等量传输
description: 设置 IEEE 1394 设备的常时等量传输
ms.assetid: 5161da54-0f20-496c-bf64-dc756b987de2
keywords:
- 同步 i/o WDK IEEE 1394 总线，设置
- 总线周期 WDK IEEE 1394 总线
- 同步通道 WDK IEEE 1394 总线
- 资源句柄 WDK IEEE 1394 总线
- 缓冲 WDK IEEE 1394 总线
- 加速 WDK IEEE 1394 总线
- 分配带宽
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a41644e5f7c124b459100f2995461e36b701ed74
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841523"
---
# <a name="setting-up-isochronous-transfer-for-ieee-1394-devices"></a>设置 IEEE 1394 设备的常时等量传输


在驱动程序可以启动其设备之前，必须执行以下步骤：

### <a href="" id="step-1---choose-the-transfer-speed-"></a>步骤1。 选择 "传输速度"。

IEEE 1394 总线可支持多种不同的速度，受硬件允许的限制。 即使特定设备支持某种速度，它也可能插入到另一个仅支持低速度的设备中。 驱动程序必须在运行时在设备和计算机之间确定传输速度。 它们通过请求查询总线驱动程序， [ **\_获取\_设备请求之间的\_速度\_** ](https://msdn.microsoft.com/library/windows/hardware/ff537645) ，以确定总线上两个设备之间的最大可能速度，或者设备和主计算机。

### <a href="" id="step-2---allocate-bandwidth-"></a>步骤2。 分配带宽。

在进行任何同步数据传输之前，驱动程序必须在总线上保留带宽。 总线会跟踪分配的带宽量，直到达到固定量（根据 IEEEE 1394-1995 规范），可以发送的最大带宽为一个*总线周期*的80%，即125毫微秒）;这样，在释放一些当前分配的带宽之前，不允许任何其他设备获取带宽。 驱动程序将[**请求提交\_ISOCH\_将\_带宽请求分配**](https://msdn.microsoft.com/library/windows/hardware/ff537647)给总线驱动程序以保留带宽。

如果请求成功，则总线驱动程序将返回一个带宽句柄。 驱动程序在以后对总线驱动程序的带宽相关请求中使用此句柄。 例如，驱动程序可以使用[**请求\_ISOCH\_设置句柄上\_通道\_带宽**](https://msdn.microsoft.com/library/windows/hardware/ff537658)来调整分配的带宽量。 当驱动程序已使用已分配的带宽完成时，它必须使用[**REQUEST\_ISOCH\_免费\_带宽**](https://msdn.microsoft.com/library/windows/hardware/ff537652)来释放带宽，使总线上的其他设备可以使用该带宽。

如果请求失败，则驱动程序不得尝试任何数据传输。 未能分配带宽的驱动程序可以在后续尝试中对其进行分配，因此，它们应该将其置于以后可以尝试分配带宽的状态。 在总线重置后尝试分配带宽很可能会成功，因为系统会在总线重置后自动释放以前分配的所有带宽和通道。

由于刚才提到的原因，在总线重置后，成功分配带宽的驱动程序必须重新分配带宽和通道。 此外，在重置后，带宽句柄会过时，并且必须通过调用[ **\_ISOCH\_自由\_带宽**](https://msdn.microsoft.com/library/windows/hardware/ff537652)来释放内存，除非使用 IRB\_标志分配带宽\_允许\_远程\_可用标志集。

### <a href="" id="step-3---allocate-a-channel-"></a>步骤3。 分配通道。

在带宽分配请求成功后，驱动程序会请求一个*同步通道*用于写入数据。 多个设备可以在一个同步通道上读取数据包，但只有一个设备可以写入通道。 接收同步数据包的设备不会在返回中发送确认数据包。

驱动程序通过将[**请求发送\_ISOCH\_** ](https://msdn.microsoft.com/library/windows/hardware/ff537648)向总线驱动程序分配\_通道请求来请求通道。 驱动程序可能会请求特定通道，或 ISOCH\_任何\_通道，以分配任何可用通道。 成功时，总线驱动程序会返回分配的通道。 如果总线驱动程序返回错误代码，则驱动程序不得尝试任何数据传输，并且必须释放在步骤2中分配的带宽。

驱动程序不应假定因为某个通道当前不可用，因此它将永远不可用。 频道可能随时都可免费使用，因此，驱动程序应将其本身置于可以尝试在以后分配通道的状态。

### <a href="" id="step-4---allocate-a-resource-handle-"></a>步骤4。 分配资源句柄。

驱动程序分配通道后，会为该通道分配资源句柄。 在所有后续步骤中，驱动程序使用资源句柄来指定通道。

驱动程序为通道分配资源句柄，方法是将[**请求提交\_ISOCH\_将请求\_资源请求分配**](https://msdn.microsoft.com/library/windows/hardware/ff537649)给总线驱动程序。

当驱动程序分配资源句柄时，它还指定标志，指示将如何使用附加到句柄的缓冲区：

-   如果驱动程序将使用该通道从设备读取数据（ [ **\_ISOCH\_侦听**](https://msdn.microsoft.com/library/windows/hardware/ff537655)操作的请求），则它会将\_侦听标志中\_使用的资源设置\_。 如果驱动程序将使用该通道将数据写入到设备（ [ **\_ISOCH\_交谈**](https://msdn.microsoft.com/library/windows/hardware/ff537660)操作的请求），则它会将\_\_使用的资源设置为\_交谈标志。

-   驱动程序使用该句柄为事务提供数据缓冲区。 （有关详细信息，请参阅步骤5。）总线驱动程序按顺序使用缓冲区，直到它运行完毕，然后暂停操作，直到设备驱动程序附加了更多的缓冲区。 有关详细信息，请参阅[IEEE 1394 设备的缓冲同步 DMA 传输](https://docs.microsoft.com/windows-hardware/drivers/ieee/buffering-isochronous-dma-transfers-for-ieee-1394-devices)。

-   驱动程序可以指定将操作同步到同步循环时钟的某个值。 有关详细信息，请参阅[IEEE 1394 设备的同步同步选项](https://docs.microsoft.com/windows-hardware/drivers/ieee/isochronous-synchronization-options-for-ieee-1394-devices)。

-   驱动程序可以设置同步侦听的选项。 驱动程序可以指示是否从数据包中去除同步数据包标头。 该驱动程序还可以指示是否应将到达的数据复制到等待数据中，每个缓冲区一个数据包，或者每个缓冲区是否应填充数据。 有关详细信息，请参阅[IEEE 1394 设备的同步侦听选项](https://docs.microsoft.com/windows-hardware/drivers/ieee/isochronous-listen-options-for-ieee-1394-devices)。

如果此请求失败，驱动程序应释放在前面的步骤中分配的所有同步资源。

### <a href="" id="step-5---attach-buffers-to-the-resource-handle-"></a>步骤5。 将缓冲区附加到资源句柄。

一旦驱动程序分配了资源句柄，它就会将缓冲区附加到句柄。 主机 DMA 控制器将从附加的缓冲区中读取数据或向其写入数据。

对于每个缓冲区，驱动程序都传递[**ISOCH\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/1394/ns-1394-_isoch_descriptor)结构，描述如何使用缓冲区。 在缓冲区的 ISOCH\_描述符结构中，驱动程序可以指定下列信息：

-   每帧的最大字节数。 传输数据时，主机控制器会将数据缓冲区拆分为此大小的数据包。

-   可选的回调例程。 总线驱动程序在处理完毕后调用此例程

-   同步选项。 有关同步选项的说明，请参阅[IEEE 1394 设备的同步同步选项](https://docs.microsoft.com/windows-hardware/drivers/ieee/isochronous-synchronization-options-for-ieee-1394-devices)。

-   在同步对话操作中，驱动程序可以将此缓冲区指定为要预置到接下来的几个数据包的标头列表。 有关详细信息，请参阅[IEEE 1394 设备的同步交谈选项](https://docs.microsoft.com/windows-hardware/drivers/ieee/isochronous-talk-options-for-ieee-1394-devices)。

操作开始后，驱动程序可以分离不再需要的缓冲区，并可以附加更多的缓冲区。 当总线驱动程序已完成处理最后一个缓冲区的处理时，驱动程序可以使用[**ISOCH\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/1394/ns-1394-_isoch_descriptor)中标识的回调例程发出信号。 有关 IEEE 1394 设备的 DMA 缓冲的说明，请参阅[针对 ieee 1394 设备缓冲同步 Dma 传输](https://docs.microsoft.com/windows-hardware/drivers/ieee/buffering-isochronous-dma-transfers-for-ieee-1394-devices)。

### <a href="" id="step-6---begin-the-data-transfer"></a>步骤6。 开始数据传输

若要从设备读取，驱动程序会发出[**请求\_ISOCH\_侦听**](https://msdn.microsoft.com/library/windows/hardware/ff537655)请求。 若要写入设备，驱动程序会发出[ **\_ISOCH\_交谈**](https://msdn.microsoft.com/library/windows/hardware/ff537660)请求的请求。 然后，该驱动程序可以按照相应的设备特定方式激活设备以进行读取或写入。

 

 




