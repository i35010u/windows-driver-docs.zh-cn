---
title: 传递 Power Irp
description: 传递 Power Irp
ms.assetid: 01473eb0-ae60-4a95-9ae7-97b2b982d3d1
keywords:
- power Irp WDK 内核传递
- 将 Irp 传递下设备堆栈 WDK
- DispatchPower 例程
- 调度例程 WDK 电源管理
- PoStartNextPowerIrp
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8f50fbb9803173cbd9b173c08fa26e00abf84741
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519136"
---
# <a name="passing-power-irps"></a>传递 Power Irp





必须将电源 Irp 一直向设备堆栈下传递给 PDO 以确保完全管理电源转换。 驱动程序处理 IRP，从而减少设备电源 IRP 传输时下设备堆栈。 驱动程序处理 IRP 应用中的设备电源[ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354)例程作为 IRP 传输到设备堆栈。

下图显示驱动程序需要通过 Windows 7 和 Windows Vista 中的设备堆栈 IRP 关机所采取的步骤。

![演示如何关闭 windows vista 中 power irp 传递的关系图](images/passirpvista.png)

上一图所示，在 Windows 7 和 Windows Vista 驱动程序必须执行以下步骤：

1.  调用[ **IoCopyCurrentIrpStackLocationToNext** ](https://msdn.microsoft.com/library/windows/hardware/ff548387)如果设置*IoCompletion*例程，或[ **IoSkipCurrentIrpStackLocation** ](https://msdn.microsoft.com/library/windows/hardware/ff550355)如果未设置*IoCompletion*例程。

    两个例程将设置下一步低驱动程序的 IRP 堆栈位置。 复制当前的堆栈位置可确保，IRP 堆栈指针设置为正确的位置时*IoCompletion*日常运行。

    如果编写不正确的驱动程序，可以调用错误**IoSkipCurrentIrpStackLocation** ，并设置完成例程，该驱动程序可能会覆盖由其下方的驱动程序设置完成例程。

2.  调用[ **IoSetCompletionRoutine** ](https://msdn.microsoft.com/library/windows/hardware/ff549679)若要设置*IoCompletion*例程中，如果完成例程是必需的。

3.  调用[ **IoCallDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff548336)将 IRP 传递到堆栈中的下一步低驱动程序。

下图显示了驱动程序需要传递在 Windows Server 2003、 Windows XP 和 Windows 2000 中的设备堆栈 IRP 关机所采取的步骤。

![向下 （windows server 2003、 windows xp 和 windows 2000） power irp 传递](images/passirp.png)

上图所示，驱动程序必须执行以下步骤：

1.  具体取决于驱动程序的类型，可能是调用[ **PoStartNextPowerIrp**](https://msdn.microsoft.com/library/windows/hardware/ff559776)。 有关详细信息，请参阅[调用 PoStartNextPowerIrp](calling-postartnextpowerirp.md)。

2.  调用[ **IoCopyCurrentIrpStackLocationToNext** ](https://msdn.microsoft.com/library/windows/hardware/ff548387)如果设置*IoCompletion*例程，或[ **IoSkipCurrentIrpStackLocation** ](https://msdn.microsoft.com/library/windows/hardware/ff550355)如果未设置*IoCompletion*例程。

    两个例程将设置下一步低驱动程序的 IRP 堆栈位置。 复制当前的堆栈位置可确保，IRP 堆栈指针设置为正确的位置时*IoCompletion*日常运行。

3.  调用[ **IoSetCompletionRoutine** ](https://msdn.microsoft.com/library/windows/hardware/ff549679)若要设置*IoCompletion*例程。 在中*IoCompletion*例程，大多数驱动程序[调用 PoStartNextPowerIrp](calling-postartnextpowerirp.md)以指示它已准备好处理 IRP 的下一个幂。

4.  调用[ **PoCallDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff559654)将 IRP 传递到堆栈中的下一步低驱动程序。

    驱动程序必须使用**PoCallDriver**，而非**IoCallDriver** （与其他 Irp) 以确保系统正确同步 power Irp。 有关详细信息，请参阅[调用 IoCallDriver vs。调用 PoCallDriver](calling-iocalldriver-versus-calling-pocalldriver.md)。

请记住， *IoCompletion*例程可以调用在 IRQL = 调度\_级别。 因此，如果驱动程序需要进行其他处理在 IRQL = 被动\_级别较低级别的驱动程序已完成与 IRP，驱动程序的后完成例程应将工作项排队，并返回状态\_详细\_处理\_必需。 工作线程必须完成 IRP。

在 Windows 98 / 驱动程序必须完成我来说，power Irp 在 IRQL = 被动\_级别。

### <a name="do-not-change-the-function-codes-in-a-power-irp"></a>不要更改 Power IRP 中的函数代码

除了处理 Irp，进行控制的常用规则[ **IRP\_MJ\_POWER** ](https://msdn.microsoft.com/library/windows/hardware/ff550784) Irp 具有以下特殊要求：接收电源的驱动程序 IRP 不得更改任何 I/O 堆栈中的位置 IRP，电源管理器或更高级别的驱动程序已设置的主版本号和次函数代码。 电源管理器依赖于这些函数代码，直到完成 IRP 保持不变。 此规则冲突的情况可能会导致难以调试的问题。 例如，操作系统可能会停止响应，或者"挂起"。

### <a name="do-not-block-while-handling-a-power-irp"></a>不会处理 Power IRP 时阻止

驱动程序必须处理 power Irp 时不会导致长时间的延迟。

传递时关闭电源 IRP，驱动程序应返回从其[ *DispatchPower* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)越早越好后调用例程**IoCallDriver** （在 Windows 7 和 Windows Vista）或**PoCallDriver** （在 Windows Server 2003、 Windows XP 和 Windows 2000）。 驱动程序不得等待内核事件或否则返回之前的延迟。 如果驱动程序不能在很短的时间处理 power IRP，它应返回状态\_PENDING 和直到 IRP 完成的 power 排队所有传入 Irp。 (请注意，此行为是不同的 PnP Irp 和[ *DispatchPnP* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程，允许阻止。)

如果该驱动程序必须等待另一个驱动程序进一步向设备堆栈下的电源操作，则应返回状态\_PENDING 从其*DispatchPower*例程，并且已设置*IoCompletion*用于 power IRP 例程。 该驱动程序可以执行任何任务中它需要*IoCompletion*例程，，然后调用**PoStartNextPowerIrp** （Windows Server 2003、 Windows XP 和 Windows 2000 仅） 和[ **IoCompleteRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548343)。

例如，设备的电源策略所有者通常将设备电源 IRP 发送以便设置在设备电源状态下适用于请求的系统电源状态的系统电源 IRP 按住。

在这种情况下，应设置电源策略所有者*IoCompletion*支持 IRP、 将系统电源 IRP 传递给下一个较低的驱动程序，并返回状态为系统中的例程\_PENDING 从其*DispatchPower*例程。

在中*IoCompletion*例程，它将调用**PoRequestPowerIrp**发送设备电源 IRP，将指针传递到请求中的回调例程。 *IoCompletion*例程应返回状态\_详细\_处理\_必需。

最后，该驱动程序，关闭系统 IRP 将来自传递回调例程。 驱动程序必须等待中的内核事件及其*DispatchPower*例行事务和使用信号*IoCompletion*例程的 IRP 它当前正在处理; 系统死锁可能会发生。 有关详细信息，请参阅[处理设备电源策略所有者中系统集 Power IRP](handling-a-system-set-power-irp-in-a-device-power-policy-owner.md)。

在类似的情况下，当系统即将进入睡眠状态，电源策略所有者可能需要完成一些挂起的 I/O 设备 IRP 发送到其设备关闭电源之前。 而不是 I/O 完成时发生的事件发出信号并等待在其*DispatchPower*例程，该驱动程序应将工作项排队并返回状态\_从 PENDING *DispatchPower*例程。 在工作线程，它等待 I/O 完成并随后将发送设备电源 IRP。 有关详细信息，请参阅[ **IoAllocateWorkItem**](https://msdn.microsoft.com/library/windows/hardware/ff548276)。

 

 




