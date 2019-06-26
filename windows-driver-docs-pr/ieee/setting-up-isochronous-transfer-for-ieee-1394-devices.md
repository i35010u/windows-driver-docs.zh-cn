---
title: 设置 IEEE 1394 设备的常时等量传输
description: 设置 IEEE 1394 设备的常时等量传输
ms.assetid: 5161da54-0f20-496c-bf64-dc756b987de2
keywords:
- 同步 I/O WDK IEEE 1394 总线设置
- 总线周期 WDK IEEE 1394 总线
- 等时通道 WDK IEEE 1394 总线
- 资源句柄 WDK IEEE 1394 总线
- 缓冲区 WDK IEEE 1394 总线
- WDK IEEE 1394 总线速度
- 分配的带宽
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 32c4c0632a3d5dfce9f031172ba84863d44d66b2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381025"
---
# <a name="setting-up-isochronous-transfer-for-ieee-1394-devices"></a>设置 IEEE 1394 设备的常时等量传输


驱动程序可以启动其设备之前，它们必须执行以下步骤：

### <a href="" id="step-1---choose-the-transfer-speed-"></a>第 1 步。 选择传输速度。

IEEE 1394 总线可以支持多个不同的限制为硬件所允许的速度。 即使特定设备支持某些速度，它可能会插入到另一台设备，仅支持较低的速度。 驱动程序必须在运行时确定设备和计算机之间的传输速度。 这些查询使用总线驱动程序[**请求\_获取\_速度\_BETWEEN\_设备**](https://msdn.microsoft.com/library/windows/hardware/ff537645)请求以确定可能的最大速度之间在总线上的两个设备或设备，并在主计算机。

### <a href="" id="step-2---allocate-bandwidth-"></a>第 2 步。 分配的带宽。

同步数据传输的所有发生之前，该驱动程序必须保留在总线上的带宽。 总线跟踪分配，直到它达到固定的量的带宽量 (根据 IEEEE 1394 1995年规范中，可以发送的最大带宽是 80%的其中一个*总线周期*，这是 125 纳秒为单位); 它就会执行不允许获取带宽，直到当前已分配带宽的一部分，将释放任何其他设备。 该驱动程序提交[**请求\_ISOCH\_分配\_带宽**](https://msdn.microsoft.com/library/windows/hardware/ff537647)保留带宽到总线驱动程序的请求。

如果请求成功，总线驱动程序返回带宽句柄。 驱动程序在将来带宽相关请求到总线驱动程序中使用此句柄。 例如，可以使用该驱动程序[**请求\_ISOCH\_设置\_通道\_带宽**](https://msdn.microsoft.com/library/windows/hardware/ff537658)句柄来调整带宽量分配。 使用已分配的带宽完成后，驱动程序，它必须使用[**请求\_ISOCH\_免费\_带宽**](https://msdn.microsoft.com/library/windows/hardware/ff537652)来释放带宽，以便可以使用它总线上的其他设备。

如果请求失败，该驱动程序必须尝试传输的所有数据。 无法分配带宽的驱动程序可能能够在后续尝试进行分配，因此，它们应该在他们才能尝试分配的带宽更高版本时相应的状态中保留本身。 尝试总线重置后可能会成功，因为系统会自动释放所有以前分配的带宽和频道，在总线重置后分配带宽。

在分配的带宽，成功的驱动程序必须重新他们的带宽和频道分配后一个总线重置，刚刚提到的原因。 此外之后重置，, 带宽句柄会变得陈旧和必须通过调用释放[**请求\_ISOCH\_免费\_带宽**](https://msdn.microsoft.com/library/windows/hardware/ff537652)，除非已带宽分配与 IRB\_标志\_允许\_远程\_免费标志设置。

### <a href="" id="step-3---allocate-a-channel-"></a>第 3 步。 分配一个通道。

带宽分配后请求成功，驱动程序请求*等时通道*要写入数据。 多个设备可以读取数据包上一个同步通道，但只有一个设备可以将写入到一个通道。 接收同步数据包的设备不返回发送确认数据包。

驱动程序通过发送请求一个通道[**请求\_ISOCH\_分配\_通道**](https://msdn.microsoft.com/library/windows/hardware/ff537648)总线驱动程序的请求。 该驱动程序可能会请求特定通道或 ISOCH\_ANY\_分配任何可用的通道的通道。 如果成功，总线驱动程序返回的已分配的通道。 如果总线驱动程序返回错误代码，驱动程序必须尝试传输的所有数据，并在必须解除分配它们在步骤 2 中分配的带宽。

驱动程序不应假定的通道当前不可用，因为它将永远不会在可用。 通道可能会变得可用在任何时候，因此驱动程序应使本身处于它们可以尝试在适当的时候更高版本分配通道的状态。

### <a href="" id="step-4---allocate-a-resource-handle-"></a>第 4 步。 分配资源句柄。

后驱动程序分配一个通道，它会为该通道分配资源句柄。 在所有后续步骤中，驱动程序使用的资源句柄指定的通道。

驱动程序分配资源句柄的通道提交[**请求\_ISOCH\_分配\_资源**](https://msdn.microsoft.com/library/windows/hardware/ff537649)总线驱动程序的请求。

当驱动程序分配一个资源句柄时，它还指定标志，指示将如何使用附加到该句柄的缓冲区：

-   如果该驱动程序将使用通道从设备读取数据 ( [**请求\_ISOCH\_侦听**](https://msdn.microsoft.com/library/windows/hardware/ff537655)操作)，它会设置资源\_用于\_IN\_正在监听标志。 如果驱动程序将使用该通道将数据写入到设备 ( [**请求\_ISOCH\_对话**](https://msdn.microsoft.com/library/windows/hardware/ff537660)操作)，它会设置资源\_用于\_IN\_谈话标志。

-   驱动程序使用该句柄为事务提供数据缓冲区。 （有关详细信息请 Step 5）。总线驱动程序按顺序使用缓冲区，直到用完，然后暂停操作，直到设备驱动程序将附加更多的缓冲区。 请参阅[IEEE 1394 设备缓冲同步 DMA 传输](https://docs.microsoft.com/windows-hardware/drivers/ieee/buffering-isochronous-dma-transfers-for-ieee-1394-devices)有关详细信息。

-   驱动程序可能会指定为某个值的同步周期时钟的同步操作。 请参阅[IEEE 1394 设备同步的同步选项](https://docs.microsoft.com/windows-hardware/drivers/ieee/isochronous-synchronization-options-for-ieee-1394-devices)有关详细信息。

-   该驱动程序可以设置等时侦听的选项。 该驱动程序可以指示是否同步数据包标头都会去除的数据包。 该驱动程序还可以指示是否应将到达的数据复制到每个缓冲区，等待数据缓冲区一个数据包或每个缓冲区应填充数据。 请参阅[IEEE 1394 设备的同步侦听选项](https://docs.microsoft.com/windows-hardware/drivers/ieee/isochronous-listen-options-for-ieee-1394-devices)有关详细信息。

如果此请求失败，驱动程序应释放它们分配在前面步骤中的所有同步资源。

### <a href="" id="step-5---attach-buffers-to-the-resource-handle-"></a>第 5 步。 将缓冲区附加到的资源句柄。

后驱动程序分配一个资源句柄，它将缓冲区附加到该句柄。 主机 DMA 控制器将从中读取数据或将数据写入到的附加缓冲区。

与每个缓冲区，驱动程序通过[ **ISOCH\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/1394/ns-1394-_isoch_descriptor)结构-描述如何将使用缓冲区。 在缓冲区的 ISOCH\_描述符结构，该驱动程序可以指定以下信息：

-   最大每一帧的字节数。 当传输数据，主控制器会数据缓冲区拆分成此大小的数据包。

-   一个可选的回调例程。 总线驱动程序完成处理时调用此例程

-   同步选项。 请参阅[IEEE 1394 设备同步的同步选项](https://docs.microsoft.com/windows-hardware/drivers/ieee/isochronous-synchronization-options-for-ieee-1394-devices)有关同步选项的说明。

-   对等时讨论操作，该驱动程序可以将此缓冲区指定为要预置到下一步的几个数据包标头的列表。 请参阅[IEEE 1394 设备的同步通信选项](https://docs.microsoft.com/windows-hardware/drivers/ieee/isochronous-talk-options-for-ieee-1394-devices)有关详细信息。

操作开始后，驱动程序可以分离它不再需要的缓冲区，可以附加更多的缓冲区。 该驱动程序可以使用回调例程中标识[ **ISOCH\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/1394/ns-1394-_isoch_descriptor)发出信号本身时总线驱动程序已完成处理附加的最后一个缓冲区。 请参阅[IEEE 1394 设备缓冲同步 DMA 传输](https://docs.microsoft.com/windows-hardware/drivers/ieee/buffering-isochronous-dma-transfers-for-ieee-1394-devices)DMA 缓冲的 IEEE 1394 设备的说明。

### <a href="" id="step-6---begin-the-data-transfer"></a>步骤 6。 开始数据传输

若要从设备驱动程序问题读取[**请求\_ISOCH\_侦听**](https://msdn.microsoft.com/library/windows/hardware/ff537655)请求。 要写入到设备驱动程序问题[**请求\_ISOCH\_对话**](https://msdn.microsoft.com/library/windows/hardware/ff537660)请求。 然后，驱动程序可以激活设备进行读取或写入，以相应的特定于设备的方式。

 

 




