---
title: 管理设备队列
description: 管理设备队列
ms.assetid: 8b7d39f8-0449-4e9b-a54c-fe60ee60842c
keywords:
- 设备队列 WDK Irp，管理
- 补充 IRP 队列 WDK 内核
- StartIo 例程，补充设备队列
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: b42f9735f08de48925380515fb21761f0679c1e6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386020"
---
# <a name="managing-device-queues"></a>管理设备队列





通常 （除了 FSDs) I/O 管理器创建一个关联的设备队列对象，当驱动程序调用[ **IoCreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocreatedevice)。 它还提供了[ **IoStartPacket** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iostartpacket)并[ **IoStartNextPacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iostartnextpacket)，哪些驱动程序可以调用具有插入到 Irp 的 I/O 管理器关联的设备的队列或调用其[ *StartIo* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_startio)例程。

因此，很少需要 （或特别有用） 驱动程序为 Irp 设置其自己的设备队列对象。 可能的候选项是驱动程序，如 SCSI 端口驱动程序，必须协调通过一定数量的异类设备通过单个控制器或总线适配器提供服务的紧密耦合的类驱动程序的传入 Irp 的。

换而言之，磁盘阵列控制器的驱动程序是更有可能使用比若要设置补充设备队列对象，而有略有更有可能使用的驱动程序的外接程序总线适配器和一组类驱动程序的驱动程序创建控制器对象补充设备队列。

### <a name="using-supplemental-device-queues-with-a-startio-routine"></a>补充设备队列使用 StartIo 例程

通过调用**IoStartPacket**并**IoStartNextPacket**，驱动程序的调度和[ *DpcForIsr* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_dpc_routine) (或[ *CustomDpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-kdeferred_routine)) 例程同步调用到其*StartIo*例程使用驱动程序创建的设备对象时，I/O 管理器创建的设备队列。 端口驱动程序与*StartIo*例程， **IoStartPacket**并**IoStartNextPacket**插入和移除 Irp 端口驱动程序的共享设备的设备队列中控制器/适配器。 如果端口驱动程序还会设置补充设备队列来保存请求来自紧密耦合更高级别的类驱动程序，它必须"排序"传入 Irp 到其补充设备队列中，通常在其*StartIo*例程。

端口驱动程序必须确定每个 IRP 再尝试将该 IRP 插入相应的队列中的对应的补充设备队列。 指向目标设备对象的指针与 IRP 传递给驱动程序的调度例程。 该驱动程序应保存在"排序"传入 Irp 中使用的指针。 请注意，设备对象指针传递给*StartIo*例程是驱动程序自己的设备对象，它表示设备控制器/适配器，所以它不能用于此目的。

队列任何 Irp 之后, 该驱动程序程序来执行请求其共享的控制器/适配器。 因此，端口驱动程序可以是在调用之前处理先，先来先服务的基础上的所有设备的入站请求[ **KeInsertDeviceQueue** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keinsertdevicequeue)将 IRP 放入特定的类驱动程序的设备的队列。

通过使用所有 Irp 自己设备队列来处理通过其*StartIo*序列化的例程，基础端口驱动程序通过共享设备 （或总线） 控制器/适配器向所有附加设备的操作。 通过为单独的设备队列中每个受支持的设备有时持有 Irp，此端口驱动程序会禁止通过其共享硬件来执行 I/O 的每个其他设备时提高 I/O 吞吐量为已经忙设备 Irp 的处理。

以响应对的调用**IoStartPacket**从端口驱动程序的调度例程，I/O 管理器可以调用该驱动程序*StartIo*立即例程或放入设备队列 IRP与端口驱动程序的共享的控制器适配器的设备对象相关联。

端口驱动程序必须维护其自己的状态信息有关每个服务通过共享的设备控制器/适配器的异构设备。

**设计具有补充设备队列的类/端口驱动程序时，请记住以下：**

-   驱动程序不能轻松地获得到的上面本身，在其设备堆栈顶部的设备对象除外的任何驱动程序创建的设备对象的指针。

    根据设计，I/O 管理器不提供用于获取一个指针，此类支持例程。 此外，驱动程序的加载的顺序使较低的驱动程序，以提供更高级别的驱动程序的设备对象，具有尚未创建任何较低级别驱动程序添加其设备时已不可能。

    尽管**IoGetAttachedDeviceReference**返回驱动程序的堆栈中对象的指针到最高级别的设备驱动程序应使用该指针仅可以指定对其堆栈的 I/O 请求的目标。 驱动程序不应尝试读取或写入的设备对象。

-   驱动程序不能使用指向由上面本身，除要将请求发送到其自己设备堆栈顶部的任何驱动程序创建的设备对象的指针。

    两个驱动程序以包含多个处理器安全的方式之间没有无法同步到单个设备对象 （和其设备扩展） 的访问。 既不驱动程序可以做出有关 I/O 处理其他驱动程序当前如何进行任何假设。

即使对于紧密耦合的类/端口驱动程序，每个类驱动程序应使用指向端口驱动程序的设备对象的指针仅将传递上使用的 Irp **IoCallDriver**。 基础端口驱动程序必须维护其自己的状态，可能在端口驱动程序的设备扩展，有关紧密地处理任何请求中耦合类驱动程序设备。

### <a name="managing-supplemental-device-queues-across-driver-routines"></a>管理驱动程序例程补充设备队列

一组紧密耦合类驱动程序的补充设备队列中的队列 Irp 任何端口驱动程序还必须处理以下情况下有效：

1.  其调度例程已插入 Irp 为特定的设备驱动程序创建的设备队列中该设备。

2.  对于其他设备的 Irp 继续进入，以添加到驱动程序的队列*StartIo*例程替换**IoStartPacket**，并通过共享的设备控制器处理。

3.  设备控制器不进入空闲状态，但保留在驱动程序创建的设备队列中每个 IRP 还必须添加到队列的驱动程序*StartIo*例程越早越好。

因此，在端口驱动程序*DpcForIsr*例程必须尝试将 IRP 从为特定的设备驱动程序的内部设备队列传输到每个控制器的适配器共享的设备队列时端口驱动程序完成 IRP，按如下所示：

1.  *DpcForIsr*例程调用**IoStartNextPacket**能够*StartIo*例程开始的处理下一步 IRP 已排入队列的共享的设备控制器。

2.  *DpcForIsr*例程调用[ **KeRemoveDeviceQueue** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keremovedevicequeue)出列持有的设备的代表其内部设备队列中下一步 IRP （如果有）要完成 IRP。

3.  如果**KeRemoveDeviceQueue**返回一个非 NULL 指针， *DpcForIsr*例程调用**IoStartPacket**只需取消排队的 IRP 能够与它已排入队列的共享设备控制器/适配器。 否则为调用**KeRemoveDeviceQueue**只需将设备队列对象的状态重置为不忙，并*DpcForIsr*例程省略调用**IoStartPacket**.

4.  然后，将*DpcForIsr*例程调用[ **IoCompleteRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest)与输入 IRP 为其端口驱动程序只需完成 I/O 处理，通过设置 I/O通过满足 I/O 请求错误或状态块。

请注意上述顺序意味着*DpcForIsr*例程还必须确定当前 （输入） IRP 为了管理内部队列的 Irp 高效地完成的设备。

如果端口驱动程序会尝试等待，直到其共享的控制器/适配器处于空闲状态之前取消排队的 Irp 持有其补充设备队列中，该驱动程序可能会为其出现大量的 I/O 需求时立即提供每个其他设备服务为其设备当前的 I/O 需求已实际得更亮。

 

 




