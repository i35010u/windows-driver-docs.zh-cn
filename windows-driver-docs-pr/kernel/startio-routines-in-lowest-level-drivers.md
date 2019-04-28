---
title: 最低级驱动程序中的 StartIo 例程
description: 最低级驱动程序中的 StartIo 例程
ms.assetid: f79f8929-bcf4-46a2-bf0e-0f8fb0720dd9
keywords:
- StartIo 例程，最低级别的驱动程序
- I/O 控制请求 WDK 内核
- 缓冲的 I/O WDK 内核
- 直接 I/O WDK 内核
- 同步 WDK Irp
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: b100a04e9389f40d152f9c70f50760c1f0af43a6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331939"
---
# <a name="startio-routines-in-lowest-level-drivers"></a>最低级驱动程序中的 StartIo 例程





驱动程序的调度例程 I/O 管理器的调用是满足设备 I/O 请求中的第一个阶段。 [ *StartIo* ](https://msdn.microsoft.com/library/windows/hardware/ff563858)例程是第二个阶段。 每个设备驱动程序与*StartIo*例程是可能调用[ **IoStartPacket** ](https://msdn.microsoft.com/library/windows/hardware/ff550370)从其[ *DispatchRead* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)并[ *DispatchWrite* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程，并通常的 I/O 操作的子集的控制代码它在支持其[ *DispatchDeviceControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程。 **IoStartPacket**例程将 IRP 添加到设备的系统提供的设备队列，或如果队列为空，立即调用的驱动程序*StartIo*例程来处理 IRP。

您可以假定，当驱动程序的*StartIo*调用例程，目标设备是否不忙。 这是因为 I/O 管理器调用*StartIo*两种情况下; 两者中任何一个的驱动程序的调度例程就已调用**IoStartPacket**和设备队列为空，或者驱动程序的[*DpcForIsr* ](https://msdn.microsoft.com/library/windows/hardware/ff544079)例程完成另一个请求，并已只需调用[ **IoStartNextPacket** ](https://msdn.microsoft.com/library/windows/hardware/ff550358)取消排队下一步 IRP。

之前*StartIo*例程中最高级别的设备驱动程序被调用时，驱动程序的调度例程应探测和锁定用户缓冲区，如果有必要，若要设置有效映射中 IRP 的缓冲区地址排队到其*StartIo*例程。 如果直接 I/O （或既不缓冲，也不直接 I/O），最高级别的设备驱动程序设置了其设备对象，该驱动程序无法延迟锁定用户缓冲区到其*StartIo*例程; 每个*StartIo*IRQL 在任意线程上下文中调用例程 = 调度\_级别。

**请注意**  任何缓冲区内存的驱动程序的访问*StartIo*必须锁定或从常驻，系统空间内存分配例程，并且必须可在任意线程上下文中访问。

 

一般情况下，任何较低级别设备驱动程序*StartIo*例程负责调用[ **IoGetCurrentIrpStackLocation** ](https://msdn.microsoft.com/library/windows/hardware/ff549174)与输入的 IRP，然后执行任何操作特定于请求的处理后才能启动其设备上的 I/O 操作。 特定于请求的处理可以包括：

-   设置或更新有关当前请求的驱动程序维护任何状态信息。 状态信息可能存储在目标设备对象的设备扩展中或由驱动程序分配的非分页池的某处。

    例如，如果设备驱动程序维护 InterruptExpected 布尔值，表示当前的传输操作中，其*StartIo*例程可能会将此变量设置为**TRUE**。 如果该驱动程序维护当前操作的超时计数器及其*StartIo*例程可以设置此值，或*StartIo*例程可能会排队的驱动程序[ *CustomTimerDpc* ](https://msdn.microsoft.com/library/windows/hardware/ff542983)例程。

    如果*StartIo*例程共享访问的状态信息或[硬件资源](hardware-resources.md)必须通过旋转锁与其他驱动程序例程，保护状态信息或资源。 (请参阅[旋转锁](spin-locks.md)。)

    如果*StartIo*例程与驱动程序的共享访问状态信息或资源[ *InterruptService* ](https://msdn.microsoft.com/library/windows/hardware/ff547958)例程， *StartIo*必须使用[ **KeSynchronizeExecution** ](https://msdn.microsoft.com/library/windows/hardware/ff553302)调用[ *SynchCritSection* ](https://msdn.microsoft.com/library/windows/hardware/ff563928)例程访问的状态或资源信息。 (请参阅[使用临界区](using-critical-sections.md)。)

-   将序列号分配到 IRP，以防驱动程序必须处理 IRP 时记录设备 I/O 错误。

    请参阅[日志记录错误](logging-errors.md)有关详细信息。

-   如果有必要，转换中的驱动程序的 I/O 的参数堆栈位置成特定于设备的值。

    例如，磁盘驱动程序可能需要计算传输操作中，物理磁盘地址的起始扇区或字节偏移量以及是否传输的请求的长度将高于特定扇区边界或超过传输能力其物理设备。

-   如果驱动程序控制可移动介质设备，编程的 I/O 设备工作，通知其基础文件系统，如果已更改媒体之前检查媒体的更改。

    有关详细信息，请参阅[支持可移动介质](supporting-removable-media.md)。

-   如果设备使用 DMA，检查是否请求**长度**(要传输的字节数的 IRP 的驱动程序的 I/O 堆栈位置中找到) 应将拆分成部分传输操作中所述[输入/输出技术](i-o-programming-techniques.md)，假设紧密耦合的更高级别的驱动程序不会不 presplit 大型传输的设备驱动程序。

    *StartIo*例程的此类设备驱动程序还可以负责调用[ **KeFlushIoBuffers** ](https://msdn.microsoft.com/library/windows/hardware/ff552041)和驱动程序使用基于数据包的 DMA 调用[ **AllocateAdapterChannel** ](https://msdn.microsoft.com/library/windows/hardware/ff540573)驱动程序的[ *AdapterControl* ](https://msdn.microsoft.com/library/windows/hardware/ff540504)例程。

    请参阅[适配器对象和 DMA](adapter-objects-and-dma.md)，并[维护缓存一致性](maintaining-cache-coherency.md)，有关其他详细信息。

-   如果设备使用 PIO，缓冲区的基虚拟地址映射所述在 IRP **Irp-&gt;MdlAddress**，为与系统空间地址[ **MmGetSystemAddressForMdlSafe**](https://msdn.microsoft.com/library/windows/hardware/ff554559).

    对于读取请求，该设备驱动程序的*StartIo*例程可以负责调用[ **KeFlushIoBuffers** ](https://msdn.microsoft.com/library/windows/hardware/ff552041) PIO 之前开始操作。 请参阅[维护缓存一致性](maintaining-cache-coherency.md)有关详细信息。

-   如果非 WDM 驱动程序将使用控制器对象，则调用[ **IoAllocateController** ](https://msdn.microsoft.com/library/windows/hardware/ff548224)注册其[ *ControllerControl* ](https://msdn.microsoft.com/library/windows/hardware/ff542049)例程。

-   如果该驱动程序处理可取消 Irp，检查输入 IRP 是否已被取消。

-   如果之前处理完后，可以取消输入的 IRP *StartIo*例程必须调用[ **IoSetCancelRoutine** ](https://msdn.microsoft.com/library/windows/hardware/ff549674) IRP 和入口点驱动程序的[*取消*](https://msdn.microsoft.com/library/windows/hardware/ff540742)例程。 *StartIo*例程必须获取对其调用取消自旋锁**IoSetCancelRoutine**。 或者，可以使用驱动程序[ **IoSetStartIoAttributes** ](https://msdn.microsoft.com/library/windows/hardware/ff550330)若要设置*无法*属性*StartIo*到例程 **，则返回 TRUE**。 这可以防止系统尝试取消已传递到 IRP *StartIo*通过调用[ **IoStartPacket**](https://msdn.microsoft.com/library/windows/hardware/ff550370)。

作为一般规则，使用缓冲的 I/O 的驱动程序的更简单*StartIo*比另一个使用直接 I/O 例程。 使用缓冲的 I/O 驱动程序传输少量数据的每个传输请求，而那些使用直接 I/O (是否 DMA 或 PIO) 传输大量数据传入或传出可以跨物理页边界在系统内存中的锁定的缓冲区。

更高级别的驱动程序的物理设备驱动程序通常设置其设备对象以匹配其各自的设备驱动程序的上面。 但是，最高级别的驱动程序，尤其是文件系统驱动程序，可以设置设备对象为既不直接，也不缓冲 I/O。

为缓冲的 I/O 设置其设备对象的驱动程序可以依赖的 I/O 管理器将在它发送到该驱动程序的所有 Irp 传递有效的缓冲区。 设置为直接 I/O 的设备对象的较低级驱动程序可以依赖其链中所有通过任何中间驱动程序发送到基础较低级别的设备驱动程序的 Irp 传递有效的缓冲区中的最高级别的驱动程序。

### <a name="using-buffered-io-in-startio-routines"></a>在 StartIo 例程中使用缓冲的 I/O

如果驱动程序的[ *DispatchRead*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)， [ *DispatchWrite*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)，或[ *DispatchDeviceControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程确定请求是否有效以及调用[ **IoStartPacket**](https://msdn.microsoft.com/library/windows/hardware/ff550370)，I/O 管理器会调用驱动程序的[ *StartIo*](https://msdn.microsoft.com/library/windows/hardware/ff563858)例程，以立即处理 IRP，如果设备队列为空。 如果队列不为空， **IoStartPacket**队列 IRP。 最后，调用[ **IoStartNextPacket** ](https://msdn.microsoft.com/library/windows/hardware/ff550358)来自驱动程序的[ *DpcForIsr* ](https://msdn.microsoft.com/library/windows/hardware/ff544079)或[ *CustomDpc* ](https://msdn.microsoft.com/library/windows/hardware/ff542972)例程会导致要取消排队 IRP，调用的驱动程序的 I/O 管理器*StartIo*例程。

*StartIo*例程调用[ **IoGetCurrentIrpStackLocation** ](https://msdn.microsoft.com/library/windows/hardware/ff549174)并确定必须执行哪些操作来满足请求。 预处理 IRP 之前编程物理设备所需的任何方式来执行 I/O 请求。

如果对物理访问设备 （或设备扩展） 必须与同步[ *InterruptService* ](https://msdn.microsoft.com/library/windows/hardware/ff547958)例程*StartIo*例程必须调用[ *SynchCritSection* ](https://msdn.microsoft.com/library/windows/hardware/ff563928)例程，以执行必要的设备编程。 有关详细信息，请参阅[使用临界区](using-critical-sections.md)。

使用缓冲的 I/O 的物理设备驱动程序将传输到或从系统空间分配的缓冲区，I/O 管理器，该驱动程序将在每个 IRP 中查找数据**Irp-&gt;AssociatedIrp.SystemBuffer**。

### <a name="using-direct-io-in-startio-routines"></a>在 StartIo 例程中使用直接 I/O

如果驱动程序的[ *DispatchRead*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)， [ *DispatchWrite*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)，或[ *DispatchDeviceControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程确定请求是否有效以及调用[ **IoStartPacket**](https://msdn.microsoft.com/library/windows/hardware/ff550370)，I/O 管理器会调用驱动程序的*StartIo*到例程立即处理 IRP，如果设备队列为空。 如果队列不为空， **IoStartPacket**队列 IRP。 最后，调用[ **IoStartNextPacket** ](https://msdn.microsoft.com/library/windows/hardware/ff550358)来自驱动程序的[ *DpcForIsr* ](https://msdn.microsoft.com/library/windows/hardware/ff544079)或[ *CustomDpc* ](https://msdn.microsoft.com/library/windows/hardware/ff542972)例程会导致要取消排队 IRP，调用的驱动程序的 I/O 管理器*StartIo*例程。

*StartIo*例程调用[ **IoGetCurrentIrpStackLocation** ](https://msdn.microsoft.com/library/windows/hardware/ff549174)并确定必须执行哪些操作来满足请求。 预处理以任何方式有必要，如分离到部分传输范围的大型 DMA 传输请求，然后将状态保存有关 IRP**长度**必须拆分传入传输请求。 然后，该程序要执行 I/O 请求的物理设备。

如果对物理访问设备 （或设备扩展） 必须与同步，驱动程序的 ISR *StartIo*例程必须使用驱动程序提供*SynchCritSection*例程，以执行有必要编程。 有关详细信息，请参阅[使用临界区](using-critical-sections.md)。

使用直接 I/O 任何驱动程序将数据读入到或将数据写入从锁定的缓冲区，由内存描述符列表 (MDL) 描述该驱动程序查找中在 IRP **Irp-&gt;MdlAddress**。 此类驱动程序通常使用设备控制请求缓冲的 I/O。 有关详细信息，请参阅[StartIo 例程中处理 I/O 控制请求](#ddk-handling-i-o-control-requests-in-startio-routines-kg)。

MDL 类型为驱动程序不能直接访问是不透明类型。 相反，使用 PIO 的驱动程序将用户空间缓冲区重新映射通过调用[ **MmGetSystemAddressForMdlSafe** ](https://msdn.microsoft.com/library/windows/hardware/ff554559)与**Irp-&gt;MdlAddress**作为参数。 此外使用 DMA 的驱动程序通过**Irp-&gt;MdlAddress**以在其能够重新映射到为其设备的逻辑范围的缓冲区地址的传输操作期间支持例程。

除非拆分大型 DMA 传输请求的基础的设备驱动程序，最低级别的设备驱动程序的紧密耦合的更高级别的驱动程序*StartIo*例程必须拆分大于其设备每个传输请求可以管理单个传输操作中。 使用系统的驱动程序 DMA 都需要拆分系统 DMA 控制器或其设备，以便在单个传输操作中处理过大的传输请求。

如果设备是从属的 DMA 设备，其驱动程序必须与一个驱动程序分配的适配器对象，表示 DMA 通道和驱动程序提供同步传输通过系统 DMA 控制器[ *AdapterControl*](https://msdn.microsoft.com/library/windows/hardware/ff540504)例程。 主总线 DMA 设备的驱动程序还必须使用驱动程序分配的适配器对象来同步其传输，并且必须提供*AdapterControl*例程，如果使用系统的基于数据包的 DMA 支持或[ *AdapterListControl* ](https://msdn.microsoft.com/library/windows/hardware/ff540513)例程，如果使用支持系统的分散/集中。

具体取决于驱动程序的设计，它可能与控制器对象同步物理设备上的传输和设备控制操作，并提供[ *ControllerControl* ](https://msdn.microsoft.com/library/windows/hardware/ff542049)例程。

请参阅[适配器对象和 DMA](adapter-objects-and-dma.md)并[控制器对象](using-controller-objects.md)有关详细信息。

### <a href="" id="ddk-handling-i-o-control-requests-in-startio-routines-kg"></a>处理 StartIo 例程中的 I/O 控制请求

从驱动程序的一般情况下，传递设备 I/O 控制请求的一个子集[ *DispatchDeviceControl* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)或[ *DispatchInternalDeviceControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)进行进一步处理驱动程序的日常*StartIo*例程。 在驱动程序*StartIo*例程仅必须处理有效的设备控制请求需要设备状态更改或返回有关当前设备状态的易失性信息。

每个新的驱动程序必须支持相同类型的设备与所有其他驱动程序相同的公共 I/O 控制代码集。 系统定义的公共的、 特定于设备的类型的 I/O 控制代码[ **IRP\_MJ\_设备\_控制**](https://msdn.microsoft.com/library/windows/hardware/ff550744)为缓冲请求的请求。

因此，物理设备驱动程序进行数据传输到或从每个驱动程序将查找在 IRP 中的系统空间缓冲区**Irp-&gt;AssociatedIrp.SystemBuffer**针对设备控制请求。 即使为直接 I/O 设置其设备对象的驱动程序使用缓冲的 I/O 以满足设备控制请求与公共 I/O 控制代码。

每个 I/O 控制代码的定义确定该请求的传输的数据进行缓冲处理。 任何定义的特定于驱动程序的 I/O 控制代码的私下[ **IRP\_MJ\_内部\_设备\_控制**](https://msdn.microsoft.com/library/windows/hardware/ff550766)请求之间配对驱动程序可以定义的代码使用缓冲的方法、 直接的方法或方法都不。 作为一般规则，应定义任何私人定义的 I/O 控制代码使用方法都不如果紧密耦合的更高级别的驱动程序必须分配缓冲区为该请求。

### <a name="programming-the-device-for-io-operations"></a>编程的 I/O 操作的设备

通常情况下， *StartIo*最低级别的设备驱动程序中的例程必须同步访问的任何内存或设备将其注册共享到驱动程序的 ISR 通过[ **KeSynchronizeExecution**](https://msdn.microsoft.com/library/windows/hardware/ff553302)调用驱动程序提供[ *SynchCritSection* ](https://msdn.microsoft.com/library/windows/hardware/ff563928)例程。 在驱动程序*StartIo*例程使用*SynchCritSection*例程进行实际的 I/O 在 DIRQL 编程物理设备。 有关详细信息，请参阅[使用临界区](using-critical-sections.md)。

然后再调用**KeSynchronizeExecution**，则*StartIo*例程必须执行该请求所需任何预处理。 预处理可能包括计算的初始部分传输范围和保存其他驱动程序例程的初始请求相关的任何状态信息。

如果设备驱动程序使用 DMA，其*StartIo*例程通常调用[ **AllocateAdapterChannel** ](https://msdn.microsoft.com/library/windows/hardware/ff540573)与驱动程序提供[ *AdapterControl* ](https://msdn.microsoft.com/library/windows/hardware/ff540504)例程。 在这些情况下， *StartIo*例程推迟编程到物理设备负责*AdapterControl*例程。 它，反过来，可以调用**KeSynchronizeExecution**具有驱动程序提供*SynchCritSection*例程 DMA 传输程序设备。

 

 




