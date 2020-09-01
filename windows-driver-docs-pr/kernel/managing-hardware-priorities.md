---
title: 管理硬件优先级
description: 管理硬件优先级
ms.assetid: c27eb357-49d7-4f50-9554-643b70ca33dc
keywords:
- 优先级标准 WDK 内核
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
ms.openlocfilehash: dc5621df25305ce479972fe7800430385e72e387
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89189781"
---
# <a name="managing-hardware-priorities"></a>管理硬件优先级





驱动程序例程执行的 IRQL 决定了可调用的内核模式驱动程序支持例程。 例如，某些驱动程序支持例程要求调用方以 IRQL = 调度 \_ 级别运行。 如果调用方在任何比被动级别高的 IRQL 运行，则不能安全地调用其他的 \_ 。

下面是一个 IRQLs 列表，其中调用了最常实现的标准驱动程序例程。 IRQLs 按从低到高的优先级列出。

<a href="" id="passive-level"></a>**被动 \_ 级别**  
**中断屏蔽** -无。

**调用的驱动程序例程** 被动 \_ 级别： [**DriverEntry**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)、 [*AddDevice*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)、重新 [*初始化*](/windows-hardware/drivers/ddi/ntddk/nc-ntddk-driver_reinitialize)、 [*卸载*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload) 例程、大多数调度例程、驱动程序创建的线程和工作线程。

<a href="" id="apc-level"></a>**APC \_ 级别**  
**屏蔽中断** — APC \_ 级别中断被屏蔽。

**调用的驱动程序例程** APC \_ 级别-某些调度例程 (参阅 [调度例程和 IRQLs](dispatch-routines-and-irqls.md)) 。

<a href="" id="dispatch-level"></a>**调度 \_ 级别**  
**屏蔽中断**  -分派 \_ 级别和 APC \_ 级别的中断被屏蔽。 可能会发生设备、时钟和电源故障中断。

**调用的驱动程序例程** 调度 \_ 级别： [*StartIo*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio)、 [*AdapterControl*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_control)、 [*AdapterListControl*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_list_control)、 [*ControllerControl*](https://msdn.microsoft.com/library/windows/hardware/ff542049)、 [*IoTimer*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_timer_routine)、 [*取消*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_cancel) (，同时保留取消自旋锁) 、 [*DpcForIsr*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_dpc_routine)、 [*CustomTimerDpc*](https://msdn.microsoft.com/library/windows/hardware/ff542983)、 [*CustomDpc*](/windows-hardware/drivers/ddi/wdm/nc-wdm-kdeferred_routine) 例程。

<a href="" id="dirql"></a>**DIRQL**  
**屏蔽中断**  -所有中断均为 IRQL &lt; = 驱动程序中断对象的 DIRQL。 可能会出现带有较高 DIRQL 值的设备中断，以及时钟和电源故障中断。

在 DIRQL （ [*InterruptService*](/windows-hardware/drivers/ddi/wdm/nc-wdm-kservice_routine)， [*SynchCritSection*](/windows-hardware/drivers/ddi/wdm/nc-wdm-ksynchronize_routine) 例程）调用的驱动程序例程。

APC 级别和被动级别之间唯一的区别在于 \_ \_ ，在 apc 级别执行的进程 \_ 无法获取 apc 中断。 但这两个 IRQLs 都表示一个线程上下文，并且都表示代码可以分页。

最低级别驱动程序在运行以下三个 IRQLs 之一时处理 Irp：

-   被动 \_ 级别，不会在处理器上屏蔽中断， (s) 

    **DriverEntry**、 *AddDevice*、重新 *初始化*和 *卸载* 例程也是在被动 \_ 级别运行，就像任何驱动程序创建的系统线程一样。

-   \_ \_ \_ 在*StartIo*例程中，在处理器上屏蔽了调度级别和 APC 级别中断

    *AdapterControl*、 *AdapterListControl*、 *ControllerControl*、 *IoTimer*、 *cancel* (在持有 Cancel 自旋锁) 的情况下，也可以在调度级别运行 *CustomTimerDpc* 例程 \_ ，如 *DpcForIsr* 和 *CustomDpc* 例程。

-   设备 IRQL (DIRQL) ，其中的所有中断均小于或等于驱动程序中断)  (对象的 *SynchronizeIrql* ，在 ISR 和 *SynchCritSection* 例程

大多数较高级别的驱动程序在运行以下两个 IRQLs 中的一个时处理 Irp：

-   被动 \_ 级别，不会在驱动程序的调度例程中的处理器上屏蔽中断

    **DriverEntry**、重新 *初始化*、 *AddDevice*和 *卸载* 例程也是在被动级别运行 \_ ，就像任何驱动程序创建的系统线程或工作线程回调例程或文件系统驱动程序。

-   \_ \_ \_ 在驱动程序的*IoCompletion*例程 (s 中，在处理器上屏蔽了调度级别和 APC 级别中断) 

    *IoTimer*、 *Cancel*和 *CustomTimerDpc* 例程也在调度 \_ 级别运行。

在某些情况下，大容量存储设备的中间和最低级别驱动程序将以 IRQL APC \_ 级别进行调用。 具体而言，这可能出现在页面错误中，文件系统驱动程序将 [**IRP \_ MJ \_ 读取**](./irp-mj-read.md) 请求发送到较低的驱动程序。

大多数标准驱动程序例程以 IRQL 运行，这使它们只需调用适当的支持例程即可。 例如，在以 IRQL 调度级别运行时，设备驱动程序必须调用 [**AllocateAdapterChannel**](/windows-hardware/drivers/ddi/wdm/nc-wdm-pallocate_adapter_channel) \_ 。 由于大多数设备驱动程序从 *StartIo* 例程调用这些例程，因此它们通常是在调度 \_ 级别运行的。

请注意，没有 *StartIo* 例程的设备驱动程序，因为它会设置和管理其自己的 irp 队列，因此， \_ 如果它应调用 **AllocateAdapterChannel**，则不一定会在调度级别 IRQL 上运行。 此类驱动程序必须将对 **AllocateAdapterChannel** 的调用嵌套在对 [**KeRaiseIrql**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keraiseirql) 和 [**KeLowerIrql**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kelowerirql) 的调用之间，以便在调用 **AllocateAdapterChannel** 时，它在所需的 irql 处运行，并在调用例程重新获得控制时还原原始的 irql。

调用驱动程序支持例程时，请注意以下各项。

- 使用小于当前 IRQL 的输入*NewIrql*值调用[**KeRaiseIrql**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keraiseirql)会导致错误。 调用 [**KeLowerIrql**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kelowerirql) ，但还原原始 IRQL (也就是说，调用 **KeRaiseIrql** 后) 也会导致错误。

- 在 IRQL &gt; = 调度级别运行时 \_ ，为内核定义的调度程序对象调用 [**KeWaitForSingleObject**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitforsingleobject) 或 [**KeWaitForMultipleObjects**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitformultipleobjects) 以等待非零时间间隔将导致严重错误。

- 可以安全地等待事件、信号量、互斥体或计时器设置为 "已终止" 状态的唯一驱动程序例程是：在 IRQL 被动级别（如 \_ 驱动程序创建的线程、 **DriverEntry** 和重新 *初始化* 例程）的 nonarbitrary 线程上下文中运行的驱动程序例程，或用于原本同步 i/o (操作的调度例程，如大多数设备 i/o 控制请求) 。

- 即使以 IRQL 被动级别运行 \_ ，可分页驱动程序代码也不得 [**调用 KeSetEvent**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kesetevent)、 [**KeReleaseSemaphore**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasesemaphore)或 [**KeReleaseMutex**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasemutex) ，并将输入 *Wait* 参数设置为 **TRUE**。 此类调用可能会导致严重页错误。

- 如果任何运行在超过 IRQL APC 级别的例程， \_ 都既不能从分页池分配内存，也不能安全地访问分页池中的内存。 如果以 IRQL 级别运行的例程 \_ 导致页错误，则会出现严重错误。

- 当驱动程序 \_ 调用 [**KeAcquireSpinLockAtDpcLevel**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keacquirespinlockatdpclevel) 和 [**KeReleaseSpinLockFromDpcLevel**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasespinlockfromdpclevel)时，该驱动程序必须在 IRQL 调度级别运行。

  当驱动程序 &lt; 调用 KeAcquireSpinLock 时，它可以在 IRQL = 调度 \_ 级别运行，但它必须通过调用**KeReleaseSpinLock**来释放该自旋锁。 **KeAcquireSpinLock** 换句话说，它是一种编程错误，用于通过调用**KeReleaseSpinLockFromDpcLevel**释放通过**KeAcquireSpinLock**获取的旋转锁。

  驱动程序在以 IRQL 调度级别运行时，不能调用 **KeAcquireSpinLockAtDpcLevel**、 **KeReleaseSpinLockFromDpcLevel**、 **KeAcquireSpinLock**或 **KeReleaseSpinLock** &gt; \_ 。

- 如果调用方未在引发的 IRQL 下运行，则调用使用自旋锁（如**ExInterlocked<em>Xxx</em> **例程）的支持例程会将当前处理器上的 IRQL 提升为调度 \_ 级别或 DIRQL。

- 以 IRQL 被动级别运行的驱动程序代码 &gt; \_ 应尽快执行。 例程的运行时间越大，更重要的是，更重要的是，更重要的是，它可以优化该例程，使其尽可能快地执行。 例如，任何调用 **KeRaiseIrql** 的驱动程序都应该尽快使对 **KeLowerIrql** 的调用。

有关确定优先级的详细信息，请参阅 [计划、线程上下文和 IRQL](https://go.microsoft.com/fwlink/p/?linkid=59757) 白皮书。

 

