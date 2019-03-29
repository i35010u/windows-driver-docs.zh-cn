---
title: 使用被动级别中断服务例程
description: 从 Windows 8 开始，驱动程序可以使用 IoConnectInterruptEx 例程来注册一个被动级别 InterruptService 例程 (ISR)。
ms.assetid: 122BDE14-1552-4F7B-88D3-030423713E00
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 7359f2764e46f3def32118848f04a2483590fc0a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567323"
---
# <a name="using-passive-level-interrupt-service-routines"></a>使用被动级别中断服务例程


从 Windows 8 开始，驱动程序也可以使用[ **IoConnectInterruptEx** ](https://msdn.microsoft.com/library/windows/hardware/ff548378)例程，以注册一个被动级[ *InterruptService* ](https://msdn.microsoft.com/library/windows/hardware/ff547958)例程 (ISR)。 内核的中断的陷阱处理程序相关联的中断发生时，计划在 IRQL 运行此例程 = 被动\_级别。 ISR 可能需要在被动级别运行，如果它可以仅通过 I/O 请求访问设备的硬件寄存器。 被动级别 ISR 可以 synchrononously 发送 I/O 请求到设备并且该请求完成之前阻止。

## <a name="registering-a-passive-level-isr"></a>注册被动级别 ISR


输入的参数**IoConnectInterruptEx**指向的指针[ **IO\_CONNECT\_中断\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff550541)结构。 若要注册被动级别 ISR，设置**版本**任一连接到此结构的成员\_完全\_SPECIFIED 或 CONNECT\_行\_基于。 如果**版本**= CONNECT\_完全\_指定，设置**Irql**成员添加到被动\_级别**SynchronizeIrql**成员为被动\_级别，并**旋转锁**成员添加到**NULL**。 如果**版本**= CONNECT\_行\_参照，设置**SynchronizeIrql** = 被动\_级别和**旋转锁** = **NULL**。

如果中断对象指定被动级别 ISR， [ **KeSynchronizeExecution** ](https://msdn.microsoft.com/library/windows/hardware/ff553302)例程使用内核同步事件对象而不是数值调节钮锁定来同步执行[*SynchCritSection* ](https://msdn.microsoft.com/library/windows/hardware/ff563928)例程替换 ISR

此事件对象由分配**IoConnectInterruptEx**注册被动级别 ISR 调用例程 调用方必须提供此调用中的旋转锁。 (也就是说，调用方必须设置**SpinLock**的成员**IO\_CONNECT\_中断\_参数**结构为 NULL，如果 ISR 是被动级别运行。)否则为**IoConnectInterruptEx**失败并返回错误状态 STATUS\_无效\_参数。

[ **KeAcquireInterruptSpinLock** ](https://msdn.microsoft.com/library/windows/hardware/ff551914)并[ **KeReleaseInterruptSpinLock** ](https://msdn.microsoft.com/library/windows/hardware/ff553139)例程会导致的 bug 检查，如果提供 ISR中断对象运行在 IRQL = 被动\_级别。

## <a name="devices-that-require-passive-level-interrupt-handling"></a>设备需要被动级的中断处理


对于内存映射的设备，用于通知级别触发中断请求，设备的 ISR 是通常在从 DIRQL 内调用内核的中断的陷阱处理程序。 ISR 操作中要关闭中断的设备的硬件寄存器。

但是，ISR 可能需要运行在 IRQL = 被动\_不能直接从在内核内调用在 DIRQL 从 ISR 访问级别，如果关联的设备发出信号级别触发中断请求，但注册设备的硬件中断的陷阱处理程序。 例如，设备注册可能不是内存映射或 ISR 可能会暂时阻止注册访问期间。

从 Windows 8 开始，驱动程序可以注册被动级别 ISR. 当发生中断时，内核的中断的陷阱处理程序计划在 IRQL 运行 ISR = 被动\_级别。 在处理程序返回之前，它必须提示中断控制器中的中断 (或[GPIO 控制器](https://msdn.microsoft.com/library/windows/hardware/hh439512))。 如果设备信号边缘触发中断处理程序将清除中断控制器中的中断。 如果设备发出信号级别触发中断，则处理程序会暂时屏蔽中断控制器; 中的中断ISR 运行后，内核解除屏蔽的中断。

## <a name="an-example"></a>示例


可能需要被动级别 ISR 设备的一个示例是连接到低功耗串行总线，如 I²C 传感器设备。 从 Windows 8 开始，支持 I²C 以及其他[简单的外围总线](https://msdn.microsoft.com/library/windows/hardware/hh450903)(SPBs) 通过提供[存储框架扩展](https://msdn.microsoft.com/library/windows/hardware/hh406203)(SpbCx)。

若要访问 I²C 连接传感器设备的寄存器，传感器驱动程序将传感器设备发送的 I/O 请求，共同处理由 SpbCx 和总线控制器驱动程序。 若要执行所请求的操作，在存储控制器必须将数据传输按顺序通过总线。 此传输速度相对较慢，并且不能在 DIRQL 运行 ISR 的时间限制内执行。 但是，被动级别 ISR 可以同步发送的 I/O 请求，并一直阻止到该请求完成。

在此示例中被动级别 ISR 可能会阻止较长的时间，如果 I²C 总线控制器处于关闭状态，当 ISR 将 I/O 请求发送到中断的设备。 在这种情况下，控制器可以将数据传输通过总线前必须完成转换到 D0 电源状态。

如 PCI 总线，与在此示例中的 I²C 总线提供了没有总线特定于方法来传达给处理器的中断请求从外围设备。 相反，传感器设备可能会发出信号 GPIO 控制器设备，然后将中继到处理器中断请求 pin 中断。 有关详细信息，请参阅[GPIO 中断](https://msdn.microsoft.com/library/windows/hardware/hh406467)。

通常情况下，GPIO 控制器的硬件寄存器是内存映射，可通过内核的中断的陷阱处理程序访问在 DIRQL。 当传感器设备导致中断时，该处理程序必须通过操作在寄存器中 GPIO 控制器的中断位提示中断。

级别触发中断，内核的中断的陷阱处理程序掩盖了处的 GPIO 是固定的中断请求，然后安排传感器设备 ISR 以被动级别运行。 ISR 必须清除来自传感器设备的中断请求。 ISR 返回后，内核解除屏蔽在 GPIO pin 中断请求。

边缘触发中断，内核的陷阱处理程序清除处的 GPIO 是固定的中断请求，然后安排传感器设备 ISR 以被动级别运行。

## <a name="worker-routines"></a>辅助角色例程


在调用**IoConnectInterruptEx**，驱动程序包含拆分的被动级别 ISR 和辅助角色例程之间中断处理的选项。 作为一般规则，ISR 应进行初始处理的中断 （例如，静音级别触发中断），并将推迟到辅助角色的其他处理。 尽管 ISR 和辅助角色运行在被动级别，但 ISR 以相对较高优先级运行，并可能会延迟高优先级的其他任务。 这些任务可能包括被动级别 Isr 为的新的中断。

在极少数情况下，可能需要中断因此少处理被动级别 ISR 可以执行所有处理中断和没有辅助例程是必需的。

有关在 KMDF 驱动程序中使用被动级别 Isr 的信息，请参阅[支持被动级别中断](https://msdn.microsoft.com/library/windows/hardware/hh451035)。

 

 




