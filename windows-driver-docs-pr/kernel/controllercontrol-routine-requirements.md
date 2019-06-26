---
title: ControllerControl 例程要求
description: ControllerControl 例程要求
ms.assetid: b311c0b0-f7b1-4276-a165-5c658657b198
keywords:
- 控制器对象 WDK 内核，编写 ControllerControl 例程
- ControllerControl 例程编写
- ControllerControl 例程要求
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: d1e76d9d27587e802f918ff4830d90846d3f98a2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377217"
---
# <a name="controllercontrol-routine-requirements"></a>ControllerControl 例程要求





正如其名， [ *ControllerControl* ](https://msdn.microsoft.com/library/windows/hardware/ff542049)例程是与控制器对象相关联。 当*ControllerControl*例程执行、 是免费的控制器对象所表示的硬件和控制器扩展通常不所访问的另一个驱动程序例程除非控制器扩展包含与驱动程序的 ISR.共享的上下文

通常情况下， *ControllerControl*例程至少执行以下操作：

1.  更新或驱动程序保持在目标设备对象的设备扩展和控制器扩展任何上下文

    如果驱动程序使用 DMA，其*ControllerControl*例程通常负责确定是否给定的传输请求必须拆分为分部由于系统施加任何传输或设备施加的限制每次 DMA 传输的大小。 在这些情况下， *ControllerControl*例程还负责调用[ **AllocateAdapterChannel** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-pallocate_adapter_channel)如果驱动程序具有*AdapterControl*例程。

    如果驱动程序使用 PIO，其*ControllerControl*例程还负责[拆分传输请求](splitting-dma-transfer-requests.md)，则其硬件要求，到部分传输范围时，调用[**MmGetSystemAddressForMdlSafe** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)与在 MDL **Irp-&gt;MdlAddress**。

2.  程序请求的 I/O 操作其硬件

    如果扩展名为设备或控制器可以访问从 ISR *ControllerControl*例程必须使用[ *SynchCritSection* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-ksynchronize_routine)调用调用的例程[ **KeSynchronizeExecution**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kesynchronizeexecution)。 有关详细信息，请参阅[使用临界区](using-critical-sections.md)。

如果该驱动程序有[*取消*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_cancel)例程，其*ControllerControl*例程还必须检查**Irp-&gt;取消**字段若要确定是否应取消当前 IRP，并执行以下任一操作：

如果**Irp-&gt;取消**设置为**TRUE**，则*ControllerControl*例程必须执行以下操作：

1.  将状态设置\_取消**状态**对于该值为零**信息**IRP 的 I/O 状态块中。

2.  调用[ **IoFreeController** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-iofreecontroller)来释放控制器对象，因此可以立即开始下一个设备操作。

3.  调用[ **IoStartNextPacket** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iostartnextpacket)或取消排队下一步 IRP，如果该驱动程序管理其自己的队列。

4.  完成与已取消的 IRP [ **IoCompleteRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest)并将控制权返回。

如果**Irp-&gt;取消**未设置为**TRUE**，则*ControllerControl*例程而是必须执行以下操作：

1.  调用[ **IoSetCancelRoutine** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetcancelroutine)若要重置*取消*到 IRP 的例程的入口点**NULL**。 获取此调用取消自旋锁，如果该驱动程序使用 I/O 管理器提供的设备队列中的设备对象。

2.  请求的 I/O 操作，对硬件编程使用[ *SynchCritSection* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-ksynchronize_routine)调用调用的例程[ **KeSynchronizeExecution**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kesynchronizeexecution). 有关详细信息，请参阅[使用临界区](using-critical-sections.md)

有关处理可取消 Irp 的详细信息，请参阅[取消 Irp](canceling-irps.md)。

除最中断驱动 I/O 操作重叠方式连接到物理控制器/适配器，不同设备上的操作*ControllerControl*例程应返回**KeepObject**因为[ *DpcForIsr* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_dpc_routine)或[ *CustomDpc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-kdeferred_routine)例程完成该操作并且 IRP。

只要以满足当前请求的 I/O 操作完成后，应调用的例程将完成 IRP **IoFreeController**并**IoStartNextPacket** ，以便可以在下一个请求尽可能快地处理。

如果*ControllerControl*例程本身完成 IRP，或如果它可以设置的操作，例如磁盘寻道一个目标设备对象 （磁盘），可能重叠的与另一个设备对象，操作*ControllerControl*例程应返回**DeallocateObject**。

 

 




