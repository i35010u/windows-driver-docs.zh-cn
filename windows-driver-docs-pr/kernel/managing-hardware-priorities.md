---
title: 管理硬件优先级
description: 管理硬件优先级
ms.assetid: c27eb357-49d7-4f50-9554-643b70ca33dc
keywords:
- 优先化条件 WDK 内核
- 硬件优先级 WDK 内核
- IRQL 级别 WDK 内核
- PASSIVE_LEVEL WDK
- APC_LEVEL WDK
- DISPATCH_LEVEL WDK
- DIRQL WDK
- 中断服务例程 WDK 内核，硬件优先级
- Isr WDK 内核，硬件优先级
ms.date: 05/08/2018
ms.localizationpriority: medium
ms.openlocfilehash: 0a2b9f120722c0917b198bfb99f0d7bcf26b5283
ms.sourcegitcommit: fee68bc5f92292281ecf1ee88155de45dfd841f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/10/2019
ms.locfileid: "67716961"
---
# <a name="managing-hardware-priorities"></a>管理硬件优先级





驱动程序例程的执行的 IRQL 确定它可以调用的内核模式驱动程序支持例程。 例如，某些驱动程序支持例程需要该调用方处于运行状态在 IRQL = 调度\_级别。 其他人不能在如果调用方被动比更高版本的任何 irql 运行安全地调用\_级别。

下面是最常实现的标准驱动程序例程称为于 Irql 的列表。 于 Irql 列出了从最低到最高优先级。

<a href="" id="passive-level"></a>**PASSIVE\_LEVEL**  
**中断应用掩码**-None。

**在调用驱动程序例程**被动\_级别 — [**DriverEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)， [ *AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_add_device)， [*重新初始化*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nc-ntddk-driver_reinitialize)， [*卸载*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_unload)例程，大多数的调度例程，驱动程序创建线程时，工作线程回调。

<a href="" id="apc-level"></a>**APC\_LEVEL**  
**屏蔽关闭中断**— APC\_级别中断应用掩码。

**驱动程序在调用的例程**APC\_级别 — 一些调度例程 (请参阅[调度例程和于 Irql](dispatch-routines-and-irqls.md))。

<a href="" id="dispatch-level"></a>**调度\_级别**  
**屏蔽关闭中断** — 调度\_级别和 APC\_级别中断应用掩码。 设备、 时钟和电源故障可能发生中断。

**在调用驱动程序例程**调度\_级别 — [*StartIo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_startio)， [ *AdapterControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_control)， [ *AdapterListControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_list_control)， [ *ControllerControl*](https://msdn.microsoft.com/library/windows/hardware/ff542049)， [ *IoTimer* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_timer_routine)， [*取消*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_cancel) （同时保留取消自旋锁）， [ *DpcForIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_dpc_routine)， [ *CustomTimerDpc*](https://msdn.microsoft.com/library/windows/hardware/ff542983)， [ *CustomDpc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-kdeferred_routine)例程。

<a href="" id="dirql"></a>**DIRQL**  
**屏蔽关闭中断** — 在 IRQL 所有中断&lt;= DIRQL 驱动程序的中断对象。 设备中断具有较高的 DIRQL 值会发生，以及时钟和电源故障中断。

驱动程序在 DIRQL 调用的例程 — [*InterruptService*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-kservice_routine)， [ *SynchCritSection* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-ksynchronize_routine)例程。

APC 的唯一区别\_级别和被动\_级别是，在 APC 进程执行\_级别不能获取 APC 中断。 这两个于 Irql 意味着线程上下文，但同时意味着代码可以调出。

最低级别的驱动程序处理 Irp，同时在三个于 Irql 之一运行：

-   被动\_级别，请与应用掩码中的驱动程序调度 routine(s) 处理器上没有中断

    **DriverEntry**， *AddDevice*，*重新初始化*，并且*卸载*例程还会在运行被动\_级别，与将任何驱动程序创建系统线程。

-   调度\_级别，请与调度\_级别和 APC\_级别中断应用掩码在处理器上，在*StartIo*例程

    *AdapterControl*， *AdapterListControl*， *ControllerControl*， *IoTimer*，*取消*(虽然它保留取消自旋锁），并*CustomTimerDpc*例程也运行在调度\_级别，因为*DpcForIsr*并*CustomDpc*例程。

-   设备的 IRQL (DIRQL)，与在小于或等于所有中断*SynchronizeIrql*的应用掩码中 ISR 处理器上的驱动程序的中断对象和*SynchCritSection*例程

最更高级别的驱动程序处理 Irp，同时在这两个两个于 Irql 运行：

-   被动\_级别，请与应用掩码中的驱动程序的调度例程处理器上没有中断

    **DriverEntry**，*重新初始化*， *AddDevice*，并且*卸载*例程还会在运行被动\_级别，与将任何驱动程序创建系统线程或工作线程回调例程或文件系统驱动程序。

-   调度\_级别，请与调度\_级别和 APC\_级别应用掩码中的驱动程序的处理器上的中断*IoCompletion* routine(s)

    *IoTimer*，*取消*，和*CustomTimerDpc*例程还会在运行调度\_级别。

在某些情况下，中间和最低级别的大容量存储设备的驱动程序调用在 IRQL APC\_级别。 具体而言，这可能是在文件系统驱动程序将发送页面错误[ **IRP\_MJ\_读取**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-read)请求到较低的驱动程序。

在允许它们只是为了调用相应的支持例程的 IRQL 运行大多数标准驱动程序例程。 例如，设备驱动程序必须调用[ **AllocateAdapterChannel** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-pallocate_adapter_channel)在 IRQL 调度运行时\_级别。 因为大多数设备驱动程序调用从这些例程*StartIo*例程，通常它们运行在调度\_已级别。

请注意，不具有的设备驱动程序*StartIo*例程因为它将设置和管理其自己的 Irp 的队列不一定处于调度\_级别 IRQL 时应调用**AllocateAdapterChannel**. 此类驱动程序必须将对其调用嵌套**AllocateAdapterChannel**调用之间[ **KeRaiseIrql** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keraiseirql)并[ **KeLowerIrql** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kelowerirql) ，以便调用时运行在所需的 IRQL **AllocateAdapterChannel**并还原原始的 IRQL 时调用的例程重新获得控制。

在调用时驱动程序支持例程，请注意以下。

- 调用[ **KeRaiseIrql** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keraiseirql)与输入*NewIrql*值小于当前 IRQL 会导致严重的错误。 调用[ **KeLowerIrql** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kelowerirql)若要还原原始的 IRQL 除外 (即之后调用, **KeRaiseIrql**) 还会导致错误。

- 在 IRQL 运行时&gt;= 调度\_级别、 调用[ **KeWaitForSingleObject** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kewaitforsingleobject)或者[ **KeWaitForMultipleObjects**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kewaitformultipleobjects)内核定义调度程序对象以等待非零间隔会导致严重的错误。

- 可以安全地等待事件、 信号量、 互斥锁或计时器设置为终止状态的唯一驱动程序例程是那些在 IRQL 被动的 nonarbitrary 线程上下文中运行\_级别，如驱动程序创建的线程， **DriverEntry**并*重新初始化*例程或对于本质上的同步 I/O 操作 （如大多数设备 I/O 控制请求） 的调度例程。

- 在被动 IRQL 运行时甚至\_级别，可分页的驱动程序代码必须调用[ **KeSetEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kesetevent)， [ **KeReleaseSemaphore** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kereleasesemaphore)，或[ **KeReleaseMutex** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kereleasemutex)输入*等待*参数设置为**TRUE**。 此类调用可能会导致严重的页面错误。

- 在运行时使用大于 IRQL APC 的任何例程\_级别既不从页面缓冲池分配的内存也不能安全地访问页面缓冲池内存。 如果运行在 IRQL 大于 APC 的例程\_级别将导致页错误，它是一个错误。

- 驱动程序必须运行在 IRQL 调度\_级别时，它调用[ **KeAcquireSpinLockAtDpcLevel** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keacquirespinlockatdpclevel)并[ **KeReleaseSpinLockFromDpcLevel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kereleasespinlockfromdpclevel).

  驱动程序可以运行在 IRQL &lt;= 调度\_级别时，它调用**KeAcquireSpinLock**但它必须通过调用释放该旋转锁**KeReleaseSpinLock**。 换而言之，它是编程错误释放自旋锁的情况下获取**KeAcquireSpinLock**通过调用**KeReleaseSpinLockFromDpcLevel**。

  驱动程序不能调用**KeAcquireSpinLockAtDpcLevel**， **KeReleaseSpinLockFromDpcLevel**， **KeAcquireSpinLock**，或**KeReleaseSpinLock** IRQL 在运行时&gt;调度\_级别。

- 调用支持例程使用旋转锁，如**ExInterlocked<em>Xxx</em>** 例程中，将引发 IRQL 当前处理器上调度到\_层，或如果调用方不是 DIRQL 到已运行引发 IRQL。

- 驱动程序代码运行在 IRQL&gt;被动\_级别应尽可能快地执行。 从该处例程运行，更重要的是很好的整体性能来优化该例程，以尽可能快地执行越高 IRQL。 例如，调用任何驱动程序**KeRaiseIrql**应进行相互调用**KeLowerIrql**就立即可以。

有关确定优先级的详细信息，请参阅[计划、 线程上下文和 IRQL](https://go.microsoft.com/fwlink/p/?linkid=59757)白皮书。

 

 




