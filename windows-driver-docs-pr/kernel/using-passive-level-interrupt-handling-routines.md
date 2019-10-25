---
title: 使用被动级别中断服务例程
description: 从 Windows 8 开始，驱动程序可以使用 IoConnectInterruptEx 例程来注册被动级 InterruptService 例程（ISR）。
ms.assetid: 122BDE14-1552-4F7B-88D3-030423713E00
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 95eeabc811ae2eab45d6e57cdaa62af37b73303b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835920"
---
# <a name="using-passive-level-interrupt-service-routines"></a>使用被动级别中断服务例程


从 Windows 8 开始，驱动程序可以使用[**IoConnectInterruptEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioconnectinterruptex)例程来注册被动级[*INTERRUPTSERVICE*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-kservice_routine)例程（ISR）。 发生关联的中断时，内核的中断陷阱处理程序会将此例程计划为以 IRQL = 被动\_级别运行。 如果 ISR 只能通过 i/o 请求访问设备的硬件寄存器，则它可能需要在被动级别运行。 被动级别 ISR 可以 synchrononously 将 i/o 请求发送到设备，并在请求完成前阻止。

## <a name="registering-a-passive-level-isr"></a>注册被动级 ISR


**IoConnectInterruptEx**的输入参数是指向[**IO\_连接\_中断\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_connect_interrupt_parameters)结构的指针。 若要注册被动级别的 ISR，请将此结构的**版本**成员设置为完全\_指定或连接\_行\_\_。 如果**Version** = CONNECT\_完全\_指定，请将**Irql**成员设置为被动\_级别，将**SynchronizeIrql**成员设置为被动\_level，将**旋转锁**成员设置为**NULL**。 如果**Version** = CONNECT\_LINE\_，则将 set **SynchronizeIrql** = 被动\_LEVEL 和**旋转锁** = **NULL**。

如果中断对象指定被动级 ISR， [**KeSynchronizeExecution**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesynchronizeexecution)例程将使用内核同步事件对象而不是自旋锁来将[*SynchCritSection*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-ksynchronize_routine)例程的执行与 ISR 同步。

此事件对象由注册被动级 ISR 的调用中的**IoConnectInterruptEx**例程分配。 调用方不能在此调用中提供自旋锁。 （也就是说，如果 ISR 要在被动级别运行，则调用方必须将 IO 的**旋转锁**成员设置 **\_将\_中断\_参数**结构设置为 NULL。）否则， **IoConnectInterruptEx**将失败并返回错误状态状态\_无效\_参数。

如果所提供中断对象的 ISR 在 IRQL = 被动\_级别运行，则[**KeAcquireInterruptSpinLock**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551914(v=vs.85))和[**KeReleaseInterruptSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleaseinterruptspinlock)例程会导致 bug 检查。

## <a name="devices-that-require-passive-level-interrupt-handling"></a>需要被动级别中断处理的设备


对于表明级别触发的中断请求的内存映射设备，设备的 ISR 通常在 DIRQL 中从内核的中断陷阱处理程序中调用。 ISR 操作设备中的硬件寄存器，以关闭中断。

但是，如果关联的设备发出通知级别触发的中断请求，但不能直接从内核的 DIRQL 中调用的 ISR 访问设备的硬件寄存器，则 ISR 可能需要在 IRQL = 被动\_级别运行中断陷阱处理程序。 例如，设备寄存器可能未进行内存映射，或在寄存器访问期间可能暂时阻止了 ISR。

从 Windows 8 开始，驱动程序可以注册被动级 ISR。 发生中断时，内核的中断陷阱处理程序会将 ISR 计划为以 IRQL = 被动\_级别运行。 在处理程序返回之前，它必须在中断控制器（或[GPIO 控制器](https://docs.microsoft.com/windows-hardware/drivers/gpio/gpio-driver-support-overview)）中使中断静音。 如果设备发出信号表示边缘触发中断，处理程序将清除中断控制器中的中断。 如果设备发出信号表示级别触发的中断，则处理程序会临时屏蔽中断控制器中的中断;ISR 运行后，内核解除中断。

## <a name="an-example"></a>示例


可能需要被动级别 ISR 的设备示例是连接到低功耗串行总线的传感器设备，例如 I I I C。 从 Windows 8 开始，由[SPB framework 扩展](https://docs.microsoft.com/windows-hardware/drivers/spb/spb-framework-extension)（SpbCx）提供对 i2c C 和其他[简单外围总线](https://docs.microsoft.com/previous-versions/hh450903(v=vs.85))（SPBs）的支持。

若要访问连接了 i2c 的传感器设备的寄存器，传感器驱动程序会向传感器设备发送 i/o 请求，该请求由 SpbCx 以及总线的控制器驱动程序进行处理。 若要执行请求的操作，SPB 控制器必须通过总线串行传输数据。 此传输相对较慢，并且不能在运行 DIRQL 的 ISR 的时间约束内执行。 但是，被动级 ISR 可以同步发送 i/o 请求，然后在请求完成前阻止。

如果 ISR 向中断的设备发送 i/o 请求，则此示例中的被动级别 ISR 可能会被阻止一段较长的时间。 在这种情况下，控制器必须先完成到 D0 电源状态的转换，然后才能在总线上传输数据。

与 PCI （如 PCI）相比，在此示例中，I i2c 总线不提供特定于总线的方式来将中断请求传达给处理器。 相反，传感器设备可能会将中断发送到 GPIO 控制器设备上的 pin，然后将中断请求中继到处理器。 有关详细信息，请参阅[GPIO 中断](https://docs.microsoft.com/windows-hardware/drivers/gpio/gpio-interrupts)。

通常，GPIO 控制器的硬件寄存器是内存映射的，可通过内核的中断陷阱处理程序在 DIRQL 进行访问。 当传感器设备导致中断时，处理程序必须通过操作 GPIO 控制器的注册中的中断位来使中断静音。

对于级别触发的中断，内核的中断陷阱处理程序会在 GPIO pin 处屏蔽中断请求，然后计划传感器设备的 ISR 在被动级别运行。 ISR 必须清除传感器设备发出的中断请求。 ISR 返回后，内核会在 GPIO pin 解除中断请求。

对于边缘触发的中断，内核的陷阱处理程序会清除 GPIO pin 中的中断请求，然后将传感器设备的 ISR 计划为在被动级别运行。

## <a name="worker-routines"></a>辅助例程


在对**IoConnectInterruptEx**的调用中，驱动程序可以选择在被动级别 ISR 和辅助例程之间拆分中断的处理。 通常情况下，ISR 应执行中断的初始处理（例如，使级别触发的中断静音），并将额外的处理推迟到辅助进程。 尽管 ISR 和 worker 在被动级别运行，但 ISR 以相对较高的优先级运行，并且可能会延迟其他高优先级任务。 这些任务可能包括用于新中断的被动级别的 Isr。

在极少数情况下，中断可能需要很少的处理，那就是被动级 ISR 可以为中断执行所有处理，并且不需要任何工作例程。

有关在 KMDF 驱动程序中使用被动级 Isr 的信息，请参阅[支持被动级别中断](https://docs.microsoft.com/windows-hardware/drivers/wdf/supporting-passive-level-interrupts)。

 

 




