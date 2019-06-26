---
title: 从 SerCx2 托管串行端口读取数据
description: 串行控制器 （或 UART） 通常包括接收先进先出。
ms.assetid: 36522E60-3616-4431-8C8C-3EAC4A6E4422
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 25b15708fcebf515bbebd121865eaf2d3ae76809
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356855"
---
# <a name="reading-data-from-a-sercx2-managed-serial-port"></a>从 SerCx2 托管串行端口读取数据

串行控制器 （或 UART） 通常包括接收先进先出。 此 FIFO 提供了硬件控制从外围设备连接到串行端口接收的数据缓冲。 若要从接收 FIFO 读取数据，此设备的外围设备驱动程序发送读取 ([**IRP\_MJ\_读取**](https://docs.microsoft.com/previous-versions/ff546883(v=vs.85))) 到串行端口的请求。

如果串行端口速度超过外围设备驱动程序可以读取的数据仍以接收数据，接收可以溢出先进先出。 若要防止数据丢失，由于发生溢出，外围设备驱动程序通常应配置要使用硬件流控制的串行端口。 用流控制串行控制器硬件自动发出信号外围设备停止发送数据时接收 FIFO 是几乎已满。 通常，由 SerCx2 的串行端口应使用硬件流控制。 有关详细信息，请参阅[流控制详细信息](#flow-control-details)。

但是，不应使用流控制停用外围设备将数据发送太长时间，或该设备可能不会继续正常运行。 例如，外围设备可能有一个内部数据缓冲区，如果设备已阻止的时间太长将数据从此缓冲区发送到串行端口可以溢出。

**此页上**

- [使用异步读取的请求](#using-asynchronous-read-requests)
- [间隔超时详细信息](#interval-time-out-details)
- [流控制详细信息](#flow-control-details)

## <a name="using-asynchronous-read-requests"></a>使用异步读取的请求

为了避免不正确的操作和可能造成数据丢失，外围设备驱动程序负责从串行控制器中读取数据的方式及时接收先进先出。 通常情况下，接收数据之前，外围设备驱动程序的异步读取的请求的未来数据到达预期的串行端口将从发送到外围设备。 此读取 SerCx2 I/O 队列中挂起的请求保持，直到数据可从接收 FIFO 读取。

在大多数的硬件平台上不需要一次同时拥有多个此类读取的请求挂起的外围设备驱动程序。 在极少数情况下，驱动程序可能需要具有多个未完成的读取的请求，如果收到数据后，读取的请求需要太长时间进程可以完成的生成数据备份会导致丢失数据或行为的外围设备之前不正确。

假定外围设备驱动程序具有一次只能有一个挂起的此类读取的请求，此请求中的数据缓冲区的所需的大小很大程度上取决于外围设备的已知行为。 例如，如果驱动程序知道提前多少个字节的数据时会出现该设备的情况，驱动程序对此数量的字节数的请求中设置的缓冲区大小。 读取的请求中接收先进先出的数据填充缓冲区时，就立即完成。 在响应中，驱动程序可以以异步方式发送一个新的读取请求等待下一个数据块。

但是，外围设备驱动程序可能不知道提前外围设备时会出现的情况多少数据。 在这种情况下，该驱动程序设置为合适的大小，则读取请求中的数据缓冲区，然后依赖于标识来自外围设备的数据的结束时间间隔超时。 选择适当的读取缓冲区的大小可能会要求掌握有关外围设备的运行方式的详细的知识。 如果读取的缓冲区因过小，该驱动程序必须发送一个或多个其他读取的请求，以完成读取的数据。

## <a name="interval-time-out-details"></a>间隔超时详细信息


若要设置的超时参数的读取和写入请求，外围设备驱动程序可以发送[ **IOCTL\_串行\_设置\_超时**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/ni-ntddser-ioctl_serial_set_timeouts)到串行端口的请求。 由控制的读取超时**ReadIntervalTimeout**， **ReadTotalTimeoutMultiplier**，并**ReadTotalTimeoutConstant**中此请求的参数值。 **ReadIntervalTimeout**指定两个连续字节中接收事务之间允许的最大时间间隔。 如果**ReadTotalTimeoutMultiplier**并**ReadTotalTimeoutConstant**是均为零，并接收串行控制器的先进先出为空时的读取的请求发送到串行端口，此请求不会不留出时间扩展 （并因此一直处于挂起状态 SerCx2 I/O 队列中的） 之前该端口接收至少一个字节的新数据后。 有关详细信息，请参阅[**串行\_超时**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/ns-ntddser-_serial_timeouts)。

芯片 (SoC) 集成线路上的系统上的串行端口可能能够从多个兆位 / 秒或更大的峰值费率外围设备接收数据。 此设备的外围设备驱动程序开发人员可能会想到设置间隔超时值 (所指定的**ReadIntervalTimeout**参数) 以毫秒为单位或更低，但此值是不可能具有所需效果。 这是因为系统时钟的粒度受限于用于检测间隔超时计时器的准确性。

例如，如果系统时钟时间是 15 毫秒，并且驱动程序设置**ReadIntervalTimeout**值为 1 毫秒，从 0 到稍有超过 15 毫秒的范围中的任意位置的字节到间隔可能触发一次扩展。有时，此设置可能会导致超时，以便从外围设备的数据传输期间发生。 若要确保，仅在此传输完成后，则会出现超时，该驱动程序可以设置**ReadIntervalTimeout**到一定程度上大于 15 毫秒的值。 例如，如果**ReadIntervalTimeout**设置为 20 毫秒，30 毫秒到字节间隔可靠地触发超时，并小于或等于 15 毫秒的时间间隔不会触发超时时间。

有关如何计时器准确性取决于系统时钟的详细信息，请参阅[计时器准确性](https://docs.microsoft.com/windows-hardware/drivers/kernel/timer-accuracy)。

## <a name="flow-control-details"></a>流控制详细信息


最佳做法是，使用 SerCx2 托管串行端口的外围设备驱动程序应配置为使用硬件流控制以防止溢出接收先进先出这些端口。 如果没有挂起的读取请求，SerCx2 提供接收数据的超出了接收先进先出的容量无软件缓冲。 如果允许此 FIFO 溢出，数据都会丢失。

若要启用硬件流控制，外围设备驱动程序可能会发送[ **IOCTL\_串行\_设置\_HANDFLOW** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/ni-ntddser-ioctl_serial_set_handflow)请求设置握手和流控制串行端口的设置。 或驱动程序可能会发送[ **IOCTL\_串行\_应用\_默认\_CONFIGURATION** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/ni-ntddser-ioctl_serial_apply_default_configuration)配置要使用的一组的串行端口的请求包括硬件流控制的默认硬件设置。 **IOCTL\_串行\_设置\_HANDFLOW**请求使用[**串行\_HANDFLOW** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/ns-ntddser-_serial_handflow)结构介绍了流控制设置。 **IOCTL\_串行\_应用\_默认\_配置**请求可能包含供应商指定的数据格式的类似信息。

如果外围设备驱动程序将使用**IOCTL\_串行\_设置\_HANDFLOW**请求启用硬件流控制，该驱动程序应在设置以下标志**序列\_HANDFLOW**此请求中的结构：

- SERIAL\_CTS\_握手中的标志**ControlHandShake**结构中的成员。 此标志可使串行端口使用的流控制接收操作。
- SERIAL\_RTS\_控件和 SERIAL\_RTS\_握手标志中**FlowReplace**成员。 这些标志启用要使用的流控制的串行端口的传输操作。
