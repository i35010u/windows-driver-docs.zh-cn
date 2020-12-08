---
title: 通过设备树了解等待/唤醒 IRP 的路径
description: 通过设备树了解等待/唤醒 IRP 的路径
keywords:
- 等待/唤醒 Irp WDK 电源管理，设备树路径
- 总线驱动程序 WDK 电源管理
- USB WDK 电源管理
- 函数驱动程序 WDK 电源管理
- FDOs WDK 电源管理
- 筛选器 DO WDK 电源管理
- 物理设备对象 WDK 电源管理
- PDO WDK 电源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 36fdb75120b4f30bbdba45115d7dfb30834257a7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96814235"
---
# <a name="understanding-the-path-of-waitwake-irps-through-a-device-tree"></a>通过设备树了解等待/唤醒 IRP 的路径





在单个设备堆栈中，电源策略所有者发送等待/唤醒 IRP，所有驱动程序都处理 wait/唤醒 IRP，如 [等待/唤醒操作概述](overview-of-wait-wake-operation.md) 和分别 [发送 WAIT/唤醒 Irp](sending-a-wait-wake-irp.md) 和 [接收 wait/唤醒 irp](receiving-a-wait-wake-irp.md)中所述。

在 [设备树](device-tree.md) 的分支内 (包含叶 devnode 以及其父代、祖辈) 的 devnodes，驱动程序必须合作，以确保等待/唤醒 IRP 达到可以启用所有必要硬件以进行唤醒的驱动程序。

在 ACPI 计算机上，ACPI 负责启用特定于系统的常规用途事件 (GPE) 注册与每个叶设备的唤醒信号关联。 因此，驱动程序必须请求和转发等待/唤醒 Irp，直到其中一个请求进入 ACPI 筛选器驱动程序， (在启动) 或基础 [WINDOWS ACPI 驱动程序](acpi-driver.md)Acpi.sys 时插入到设备堆栈中。 在响应中，ACPI 启用注册，使 IRP 处于挂起状态，直到收到信号，然后完成 IRP。 因为 ACPI 可以响应唤醒信号，所以它不会将 IRP 转发到较低的驱动程序。

ACPI 筛选器驱动程序（如基础 ACPI 驱动程序本身）对于其他驱动程序是透明的。 为了在硬件设计中提供最大的灵活性，任何设备堆栈中的 ACPI 筛选器驱动程序的确切位置都是设备和系统特定的。 设计驱动程序时，不能在设备堆栈中对 ACPI 筛选器的存在或位置做出任何假设。

请记住，枚举子项的驱动程序会为每个子设备创建一个 PDO，并为父设备创建一个 FDO。 驱动程序因此充当子设备的总线驱动程序和父设备的功能驱动程序/策略所有者。 因此，当总线驱动程序收到子 PDO 的等待/唤醒 IRP 时，它应为其父 PDO 请求其他等待/唤醒 IRP。

### <a href="" id="sample-usb-configuration"></a>

下图显示了这种情况的示例配置。

![演示示例 usb 配置的示意图](images/wwhw.png)

在示例配置中，键盘和调制解调器是 USB 集线器的子项，而 usb 集线器又是 USB 主机控制器的子控制器，它是由 PCI 总线枚举的。 下图显示了示例配置中的键盘设备堆栈。

![阐释示例 usb 键盘配置的设备堆栈的关系图](images/wwdobj.png)

如上图所示，从上到下进行读取：

1.  [WINDOWS ACPI 驱动程序](acpi-driver.md)Acpi.sys 创建用于 PCI 的 PDO。

2.  PCI 驱动程序创建 PCI FDO 和 USB 主机控制器 PDO，并拥有 PCI 设备堆栈的策略。

3.  USB 主机控制器驱动程序 (主机端口/微型端口驱动程序对) 创建 USB 主机控制器 FDO 和 USB 集线器 PDO。 它拥有 USB 主机控制器设备堆栈的策略。 请注意，Acpi.sys 还会在此堆栈中创建筛选器。

4.  USB 集线器驱动程序创建 USB 集线器 FDO 和键盘 PDO。 此驱动程序拥有 USB 集线器设备堆栈的电源策略。

5.  键盘的函数驱动程序是 USB HID 类 driver/微型驱动程序对。 此驱动程序为键盘创建 FDO，并拥有其电源策略。 由于键盘没有子设备，因此此驱动程序不会创建 PDOs。

请注意，每个设备堆栈可能包含未显示的其他可选筛选器 DOs。

为了允许键盘输入唤醒系统，键盘的策略所有者请求 **IRP \_ MN \_ 等待 \_ 唤醒** 。 该 IRP 将设置其他等待/唤醒 Irp 的链，如下图所示。

![等待/唤醒 irp 请求的示例 usb 配置](images/wwcascade.png)

当总线驱动程序接收到以其创建的 PDO 为目标的 [**irp \_ MN \_ 等待 \_ 唤醒**](./irp-mn-wait-wake.md) 时，它必须为其拥有电源策略的设备堆栈请求另一 **irp \_ MN \_ 等待 \_ 唤醒** ，并创建 FDO。

如上图所示：

1.  键盘驱动程序调用 [**PoRequestPowerIrp**](/windows-hardware/drivers/ddi/wdm/nf-wdm-porequestpowerirp) 将等待/唤醒 IRP (IRP1) 发送到其 PDO。

    电源管理器分配 IRP，并通过 i/o 管理器将其发送到键盘的设备堆栈顶部。 驱动程序设置 [*IoCompletion*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine) 例程，并将 IRP 向下传递到堆栈，直到它到达键盘 PDO。 USB 集线器驱动程序（用作键盘的总线驱动程序）包含 IRP1 挂起状态。

2.  由于 USB 集线器驱动程序无法在唤醒信号到达时唤醒系统，因此 USB 集线器驱动程序必须调用 **PoRequestPowerIrp** ，以便为 usb 集线器设备堆栈请求等待/唤醒 IRP (IRP2) 。

    Power manager 将此 IRP 发送到 USB 集线器设备堆栈的顶部。 此堆栈中的驱动程序设置 *IoCompletion* 例程，并将 IRP 向下传递到 usb 主机控制器驱动程序， (它充当 usb 集线器) 的总线驱动程序。 USB 主机控制器驱动程序包含 IRP2 挂起，直到键盘发出唤醒事件。

3.  同样，USB 主机控制器驱动程序无法唤醒系统，因此 USB 主机控制器驱动程序调用 **PoRequestPowerIrp** 将等待/唤醒 IRP (IRP3) 发送到 USB 主机控制器设备堆栈。

    Power manager 将此 IRP 发送到 USB 主机控制器设备堆栈的顶部，其中，驱动程序设置 *IoCompletion* 例程，并将 IRP 向下传递到 PCI 驱动程序 (，它充当 USB 集线器) 的总线驱动程序。 PCI 驱动程序将 IRP3 挂起，直到键盘发出唤醒事件。

4.  PCI 驱动程序无法唤醒系统，因此 PCI 驱动程序调用 **PoRequestPowerIrp** 将等待/唤醒 IRP (IRP4) 发送到 PCI 设备堆栈。 其父项是根设备，ACPI 是其总线驱动程序。

    电源管理器将 IRP 发送到 PCI 总线设备堆栈的顶部;其驱动程序设置完成例程，并将 IRP 向下传递到 [WINDOWS ACPI 驱动程序](acpi-driver.md)，Acpi.sys。

5.  Acpi.sys 可以唤醒系统，因此它不会将等待/唤醒 IRP 发送到任何其他 PDO。 Acpi.sys 在唤醒信号到达之前保留 IRP4 挂起状态。

当键盘断言唤醒信号时，Acpi.sys 会将其截取。 但是，ACPI 无法确定键盘是否宣称了信号，只是信号通过根设备发出。 然后 Acpi.sys IRP4 完成，并且 i/o 管理器会调用 *IoCompletion* 例程，并在 PCI 设备堆栈中进行备份。 当 IRP4 完成并且所有 *IoCompletion* 例程都已运行时，将调用 PCI 驱动程序的回调例程。 在其回调例程中，PCI 驱动程序确定信号是通过 USB 主机控制器发出的。 然后，PCI 驱动程序将完成 IRP3。 在键盘驱动程序收到 IRP1 之前，会通过 USB 主机控制器堆栈和 USB 集线器堆栈进行相同的序列。 此时，键盘驱动程序可以根据需要为唤醒事件服务。

驱动程序每次向父 PDO 发送等待/唤醒 IRP 时，都必须为其自己的 IRP 设置 " [*取消*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_cancel) " 例程。 设置 " *取消* " 例程将使该驱动程序有机会在取消新 IRP 的 irp 后取消该 irp。 在 USB 示例中，如果键盘驱动程序取消其等待/唤醒 IRP (因此禁用键盘唤醒) ，则 USB 集线器、USB 主机控制器和 PCI 驱动程序必须取消其由于键盘 IRP 而发送的 Irp。 有关详细信息，请参阅 [Wait/唤醒 irp 的取消例程](canceling-a-wait-wake-irp.md#ddk-cancel-routines-for-wait-wake-irps-kg)。

尽管父驱动程序可能会枚举可为等待/唤醒启用的多个子项，但 PDO 只能挂起一个等待/唤醒 IRP。 在这种情况下，父驱动程序应确保在为任何设备启用了唤醒功能的情况下，它会使等待/唤醒 IRP 处于挂起状态。 为此，在每次收到 wait/唤醒 IRP 时，驱动程序都会递增内部计数器。 每次驱动程序完成等待/唤醒 IRP 时，它都会递减计数，如果生成的值为非零，则将另一个等待/唤醒 IRP 发送到其设备堆栈。

例如，在前面所示的 [示例 Usb 配置](#sample-usb-configuration) 图中，usb 集线器枚举了两个设备：一个键盘和一个调制解调器。 当 USB 集线器驱动程序接收到键盘 PDO 的等待/唤醒 IRP 时，它会在为自己的 PDO 请求 IRP 之前递增等待/唤醒 Irp 的计数。 如果以后调制解调器的策略所有者启用了对调制解调器的唤醒，则 USB 集线器驱动程序会 pends 调制解调器 PDO 的新 IRP，并递增其等待/唤醒引用计数。 但是，因为 USB 集线器 PDO 不能同时等待两个挂起/唤醒 Irp，所以 USB 集线器驱动程序不会为 USB 集线器 PDO 请求新的等待/唤醒 IRP。

当唤醒信号到达键盘或调制解调器时，USB 集线器驱动程序将确定哪个设备已发出信号，完成相应的 IRP，并递减其引用计数。 由于这两个设备都已启用了唤醒 (，因此其引用计数不为零) ，因此它必须将其自己的设备堆栈另一个等待/唤醒 IRP 发送到 "重置" 自己的用于唤醒的 PDO。  (USB 主机控制器和 PCI 驱动程序也是如此。 ) 

但是，驱动程序不会将 IRP 发送到一个 IRP，以便在刚到达唤醒信号的同一设备上重新启用等待/唤醒。 只有设备电源策略管理器可以执行此操作。 重新启用等待/唤醒不是自动的。

 

