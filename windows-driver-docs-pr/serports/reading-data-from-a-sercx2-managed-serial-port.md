---
title: 从 SerCx2 托管串行端口读取数据
description: 串行控制器 (或 UART) 通常包含接收 FIFO。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a509a01471a356bf7abfe161f16901ade6a904d0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96811995"
---
# <a name="reading-data-from-a-sercx2-managed-serial-port"></a>从 SerCx2 托管串行端口读取数据

串行控制器 (或 UART) 通常包含接收 FIFO。 此 FIFO 提供从连接到串行端口的外围设备接收的数据的硬件控制缓冲。 若要从接收 FIFO 中读取数据，此设备的外围设备驱动程序将读取 ([**IRP \_ MJ \_ 读取**](/previous-versions/ff546883(v=vs.85))) 请求发送到串行端口。

如果串行端口继续接收数据的速度比外围设备驱动程序可以读取数据的速度快，则 receive FIFO 可能溢出。 为了防止因溢出而造成的数据丢失，外围设备驱动程序通常应将串行端口配置为使用硬件流控制。 通过流控制，当 receive FIFO 快要满时，串行控制器硬件自动向外围设备发出信号，以停止发送数据。 通常，由 SerCx2 管理的串行端口应使用硬件流控制。 有关详细信息，请参阅 [流控制详细信息](#flow-control-details)。

但是，不应使用流控制来停止外围设备发送数据的时间太长一段时间，否则设备可能无法继续正常运行。 例如，如果阻止设备从该缓冲区向串行端口发送数据过长，则可能会有可能溢出的内部数据缓冲区。

**在此页上**

- [使用异步读取请求](#using-asynchronous-read-requests)
- [间隔超时详细信息](#interval-time-out-details)
- [流控制详细信息](#flow-control-details)

## <a name="using-asynchronous-read-requests"></a>使用异步读取请求

为避免错误的操作和可能的数据丢失，外设驱动程序负责及时读取串行控制器的接收 FIFO 中的数据。 通常情况下，在接收数据之前，外围设备驱动程序会将异步读取请求发送到串行端口，以便将来从外围设备接收数据。 此读取请求始终处于挂起状态，直到 SerCx2 i/o 队列中的数据可从 receive FIFO 读取数据。

在大多数硬件平台上，外设驱动程序一次不需要有多个读取请求处于挂起状态。 在极少数情况下，驱动程序可能需要具有多个未完成的读取请求，但在接收到数据后，读取请求需要很长时间才能完成，然后才能完成，导致数据备份导致外围设备丢失数据或行为不正确。

假设外围设备驱动程序一次仅有一个挂起的读取请求，则此请求中的数据缓冲区的所需大小很大程度上取决于外围设备的已知行为。 例如，如果驱动程序事先知道要从设备接收多少字节的数据，则驱动程序会将请求中的缓冲区大小设置为此字节数。 一旦用 receive FIFO 中的数据填充了缓冲区，就会立即完成读取请求。 作为响应，驱动程序可以异步发送新的读取请求以等待下一个数据块。

但是，外设驱动程序可能不会提前知道要从外围设备获得的数据量。 在这种情况下，驱动程序将读取请求中的数据缓冲区设置为合适的大小，然后根据间隔超时值识别外围设备的数据的结束时间。 为读取缓冲区选择适当的大小可能需要详细了解外围设备的工作方式。 如果读取缓冲区太小，则驱动程序必须发送一个或多个其他读取请求才能完成数据读取。

## <a name="interval-time-out-details"></a>间隔超时详细信息


若要设置读和写请求的超时参数，外设驱动程序可以向串行端口发送 [**IOCTL \_ 串行 \_ 集 \_ 超时**](/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_set_timeouts) 请求。 读取的超时值由此请求中的 **ReadIntervalTimeout**、 **ReadTotalTimeoutMultiplier** 和 **ReadTotalTimeoutConstant** 参数值控制。 **ReadIntervalTimeout** 指定接收事务中两个连续字节之间允许的最大时间间隔。 如果 **ReadTotalTimeoutMultiplier** 和 **ReadTotalTimeoutConstant** 均为零，且在将读取请求发送到串行端口时串行控制器的 receive FIFO 为空，则此请求不会超时 (，因此，在该端口收到至少一个字节的新数据之前，将在 SerCx2 i/o 队列) 中保持挂起状态。 有关详细信息，请参阅 [**串行 \_ 超时**](/windows-hardware/drivers/ddi/ntddser/ns-ntddser-_serial_timeouts)。

芯片上系统上的串行端口 (SoC) 集成线路可以从外围设备接收数据，其高峰速率为每秒多兆位或更大。 此设备的外围设备驱动程序的开发人员可能会将 **ReadIntervalTimeout** 参数指定的时间间隔超时值设置 () 设置为毫秒或更小，但此值不可能具有所需的效果。 这是因为用于检测间隔超时的计时器的准确性受系统时钟的粒度限制。

例如，如果系统时钟周期为15毫秒，驱动程序将 **ReadIntervalTimeout** 值设置为1毫秒，则从0到小15毫秒的任意位置的从零到字节的间隔可能会触发超时。偶尔，此设置可能导致在从外围设备进行数据传输的过程中出现超时。 若要确保仅在此传输完成后发生超时，驱动程序可以将 **ReadIntervalTimeout** 设置为一个大于15毫秒的值。 例如，如果 **ReadIntervalTimeout** 设置为20毫秒，则以30毫秒为单位的字节到字节间隔可可靠地触发超时，而15毫秒或更短时间间隔不会触发超时。

有关计时器准确性如何取决于系统时钟的详细信息，请参阅 [计时器准确性](../kernel/timer-accuracy.md)。

## <a name="flow-control-details"></a>流控制详细信息


最佳做法是，使用 SerCx2 托管串行端口的外围设备驱动程序应将这些端口配置为使用硬件流控制来防止从溢出接收 FIFO。 如果没有挂起的读取请求，则 SerCx2 不提供超过接收 FIFO 容量的接收数据的软件缓冲。 如果允许此 FIFO 溢出，则数据将丢失。

若要启用硬件流控制，外设驱动程序可以发送 [**IOCTL \_ 串行 \_ SET \_ HANDFLOW**](/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_set_handflow) 请求来设置串行端口的握手和流控制设置。 或者，驱动程序可能会发送 [**IOCTL \_ 串行 \_ 应用 \_ 默认 \_ 配置**](/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_apply_default_configuration) 请求，将串行端口配置为使用一组包括硬件流控制的默认硬件设置。 **IOCTL \_ 串行 \_ 集 \_ HANDFLOW** 请求使用 [**串行 \_ HANDFLOW**](/windows-hardware/drivers/ddi/ntddser/ns-ntddser-_serial_handflow)结构来描述流控制设置。 **IOCTL \_ 串行 \_ 应用 \_ 默认 \_ 配置** 请求可能包含与供应商指定的数据格式类似的信息。

如果外围设备驱动程序使用 **IOCTL \_ 串行 \_ SET \_ HANDFLOW** 请求来启用硬件流控制，则驱动程序应在此请求的 **串行 \_ HANDFLOW** 结构中设置以下标志：

- 结构的 \_ \_ **ControlHandShake** 成员中的串行 CTS 握手标志。 此标志允许串行端口对接收操作使用流控制。
- \_ \_ FlowReplace 成员中的串行 rts 控制和串行 \_ rts \_ 握手 **FlowReplace** 标志。 这些标志使串行端口可以使用传输操作的流控制。
