---
title: ControllerControl 例程要求
description: ControllerControl 例程要求
ms.assetid: b311c0b0-f7b1-4276-a165-5c658657b198
keywords:
- 控制器对象 WDK 内核，编写 ControllerControl 例程
- ControllerControl 例程，编写
- ControllerControl 例程，要求
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: b97da170071373b0d61e4001fe6fa4e450ddcac7
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89189825"
---
# <a name="controllercontrol-routine-requirements"></a>ControllerControl 例程要求





顾名思义， [*ControllerControl*](https://msdn.microsoft.com/library/windows/hardware/ff542049) 例程与控制器对象相关联。 当 *ControllerControl* 例程执行时，控制器对象表示的硬件是免费的，并且通常不会由其他驱动程序例程访问控制器扩展，除非控制器扩展包含与驱动程序的 ISR 共享的上下文。

通常， *ControllerControl* 例程至少会执行以下操作：

1.  更新或初始化驱动程序在目标设备对象的设备扩展和控制器扩展中维护的任何上下文

    如果驱动程序使用 DMA，则其 *ControllerControl* 例程通常负责确定是否必须将给定的传输请求拆分为部分传输，因为每个 DMA 传输大小的系统强加限制或设备施加的限制。 在这些情况下，如果驱动程序具有*AdapterControl*例程， *ControllerControl*例程还负责调用[**AllocateAdapterChannel**](/windows-hardware/drivers/ddi/wdm/nc-wdm-pallocate_adapter_channel) 。

    如果驱动程序使用 PIO，则其*ControllerControl*例程还负责将[传输请求拆分](splitting-dma-transfer-requests.md)为部分传输范围，并负责将传输请求拆分为部分传输范围，并在**Irp &gt; MdlAddress**上将[**MmGetSystemAddressForMdlSafe**](./mm-bad-pointer.md)与 MDL 一起调用。

2.  为请求的 i/o 操作计划其硬件

    如果可从 ISR 访问设备或控制器扩展， *ControllerControl*例程必须使用通过调用[**KeSynchronizeExecution**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kesynchronizeexecution)调用的[*SynchCritSection*](/windows-hardware/drivers/ddi/wdm/nc-wdm-ksynchronize_routine)例程。 有关详细信息，请参阅 [使用关键部分](using-critical-sections.md)。

如果驱动程序具有 [*取消*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_cancel) 例程，则其 *ControllerControl* 例程还必须检查 **Irp- &gt; Cancel** 字段，以确定是否应取消当前 Irp，并执行以下操作之一：

如果 **Irp- &gt; Cancel** 设置为 **TRUE**，则 *ControllerControl* 例程必须执行以下操作：

1.  \_对于 "**状态**"，将 "设置状态" 设置为 "否"，对于 IRP 的 i/o 状态块中的**信息**为零。

2.  调用 [**IoFreeController**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iofreecontroller) 以释放控制器对象，以便可以立即启动下一设备操作。

3.  如果驱动程序管理自己的队列，请调用 [**IoStartNextPacket**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iostartnextpacket) 或取消下一个 IRP 的排队。

4.  完成已取消的 IRP with [**IoCompleteRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest) 并返回 control。

如果 **Irp- &gt; Cancel** 未设置为 **TRUE**，则 *ControllerControl* 例程必须执行以下操作：

1.  调用 [**IoSetCancelRoutine**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcancelroutine) 将 IRP 的 " *取消* " 例程入口点重置为 **NULL**。 如果驱动程序在设备对象中使用 i/o 管理器提供的设备队列，请为此调用获取 "取消旋转锁定"。

2.  使用通过调用[**KeSynchronizeExecution**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kesynchronizeexecution)调用的[*SynchCritSection*](/windows-hardware/drivers/ddi/wdm/nc-wdm-ksynchronize_routine)例程为请求的 i/o 操作计划硬件。 有关详细信息，请参阅 [使用关键部分](using-critical-sections.md)

有关处理可取消的 Irp 的详细信息，请参阅 [取消 irp](canceling-irps.md)。

对于附加到物理控制器/适配器的不同设备上的重叠操作除外的大多数中断驱动 i/o 操作， *ControllerControl* 例程应返回 **KeepObject** ，因为 [*DpcForIsr*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_dpc_routine) 或 [*CustomDpc*](/windows-hardware/drivers/ddi/wdm/nc-wdm-kdeferred_routine) 例程完成了操作和 IRP。

当 i/o 操作 () 满足当前请求时，将立即完成 IRP 的例程应调用 **IoFreeController** 和 **IoStartNextPacket** ，以便能够尽快处理下一次请求。

如果 *ControllerControl* 例程本身完成了 IRP，或者它可以设置一个目标设备对象 (磁盘) ，而该对象可能与另一个设备对象的操作重叠，则 *ControllerControl* 例程应返回 **DeallocateObject**。

 

