---
title: 为 I/O 操作分配控制器对象
description: 为 I/O 操作分配控制器对象
ms.assetid: 8a5e3741-f8ea-4e27-bb7f-6c20da1d618d
keywords:
- 控制器对象 WDK 内核，分配
- ControllerControl 例程，控制器对象分配
- IoAllocateController
- 分配控制器对象
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: a3b548c844942ef099a9dbcc761d7ba14529e34e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367874"
---
# <a name="allocating-controller-objects-for-io-operations"></a>为 I/O 操作分配控制器对象





使用控制器对象的驱动程序启动其设备后，就可以处理 Irp 发送到其目标设备对象。 每当 IRP 需要对程序 I/O 操作的控制器对象所表示的物理设备驱动程序，该驱动程序调用[ **IoAllocateController**](https://msdn.microsoft.com/library/windows/hardware/ff548224)。 下图说明了此类调用。

![说明为 i/o 分配控制器对象的关系图](images/3ctlaloc.png)

上图所示，驱动程序必须提供多个*ControllerObject*返回的指针[ **IoCreateController** ](https://msdn.microsoft.com/library/windows/hardware/ff548395)时它将调用[ **IoAllocateController**](https://msdn.microsoft.com/library/windows/hardware/ff548224)。 以及此指针，它必须将指针传递给驱动程序提供表示当前的 I/O 请求的目标的设备对象[ *ControllerControl* ](https://msdn.microsoft.com/library/windows/hardware/ff542049)例程，并为任何*上下文*其*ControllerControl*例程将需要设置设备进行请求的 I/O 操作。

**IoAllocateController**队列的驱动程序提供*ControllerControl*例程如果控制器对象所表示的设备正在使用中。 否则为*ControllerControl*例程使用在上图中所示的输入参数立即调用。 输入*上下文*指针，指向**IoAllocateController**传递给驱动程序*ControllerControl*例程运行时。

使用以下准则来确定存储的上下文信息的位置：

-   驱动程序提供的上下文区域不应是控制器扩展中，除非该驱动程序处理每个 IRP 到完成，然后启动物理控制器上的另一个操作。 否则，由其他驱动程序例程或在收到新 IRP，可能会覆盖控制器扩展中的上下文区域。

-   即使该驱动程序与重叠的设备的另一个设备对象的 I/O 操作，无法覆盖在目标设备对象的设备扩展中的上下文区域。

-   如果为特定设备对象发出另一个 I/O 请求，并且该驱动程序有[ *StartIo* ](https://msdn.microsoft.com/library/windows/hardware/ff563858)例程，其设备扩展中的上下文区域也无法覆盖因为将传入的 IRP当驱动程序调用时排队等待[ **IoStartPacket** ](https://msdn.microsoft.com/library/windows/hardware/ff550370)相同 IRP 将仍保留在设备队列之前驱动程序调用[ **IoStartNextPacket**](https://msdn.microsoft.com/library/windows/hardware/ff550358)之前完成当前 IRP 为该设备对象。

I/O 管理器将传递一个指向*DeviceObject*-&gt;**CurrentIrp**到*ControllerControl*例程如果驱动程序具有*StartIo*例程。 如果驱动程序管理的 Irp 自己队列，而不让*StartIo*例程，I/O 管理器不能授予*ControllerControl*一个指针，指向当前 IRP 的例程。 当驱动程序调用**IoAllocateController**，它应作为的一部分传递当前 IRP*上下文*的可访问的数据。

调用的驱动程序例程**IoAllocateController**必须执行在 IRQL = 调度\_级别调用发生时。 进行此调用中的驱动程序及其*StartIo*例程已在运行在调度\_级别。

*ControllerControl*例程将 IRP 的请求的操作的物理控制器设置。

上图中所示*ControllerControl*例程将返回类型的值[ **IO\_分配\_操作**](https://msdn.microsoft.com/library/windows/hardware/ff550534)，可以是系统定义的以下值之一：

-   如果*ControllerControl*例程可以启动物理控制器上的另一个操作，它应返回**DeallocateObject**以使该驱动程序可以重叠下一个请求的 I/O 操作。

    例如，如果*ControllerControl*例程可以计划一个磁盘上查找操作的磁盘控制器、 完成该 IRP，并返回**DeallocateObject**，则*ControllerControl*可以再次调用例程进行编程传输操作中的其他磁盘上的磁盘控制器，如果任何传输请求当前正在排队到其他磁盘。

-   如果当前 IRP 需要做进一步的处理其他驱动程序、 例程*ControllerControl*例程必须返回**KeepObject**。

    例如，如果程序传输操作中的磁盘控制器驱动程序，但直到传输完成后，无法完成 IRP *ControllerControl*例程必须返回**KeepObject**。

当*ControllerControl*例程返回**KeepObject**，驱动程序的 ISR 通常运行时，设备中断，并将其[ *DpcForIsr* ](https://msdn.microsoft.com/library/windows/hardware/ff544079)或[ *CustomDpc* ](https://msdn.microsoft.com/library/windows/hardware/ff542972)例程完成 I/O 操作和目标设备对象当前 IRP。

每当*ControllerControl*例程返回**KeepObject**，完成 IRP 的例程必须调用[ **IoFreeController** ](https://msdn.microsoft.com/library/windows/hardware/ff549104). 应调用此类的驱动程序例程**IoFreeController**越早越好，以便可以立即设置其下一个设备 I/O 操作。

 

 




