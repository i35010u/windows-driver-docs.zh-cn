---
title: 了解通过设备树等待/唤醒 Irp 的路径
description: 了解通过设备树等待/唤醒 Irp 的路径
ms.assetid: 35118367-d20b-45c9-a296-656028339c59
keywords:
- 等待/唤醒 Irp WDK 电源管理，设备树路径
- 总线驱动程序 WDK 电源管理
- USB WDK 电源管理
- 功能的驱动程序 WDK 电源管理
- FDOs WDK 电源管理
- 筛选器 DOs WDK 电源管理
- 物理设备对象 WDK 电源管理
- PDOs WDK 电源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 58cea02da33eb028b76b361ec20682be5a85b0e9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545276"
---
# <a name="understanding-the-path-of-waitwake-irps-through-a-device-tree"></a>了解通过设备树等待/唤醒 Irp 的路径





在单个设备堆栈内的电源策略所有者发送等待/唤醒 IRP 和所有驱动程序处理等待/唤醒 IRP，如中所述[等待/唤醒操作概述](overview-of-wait-wake-operation.md)中的详细说明和[发送等待/唤醒 IRP](sending-a-wait-wake-irp.md)并[接收等待/唤醒 IRP](receiving-a-wait-wake-irp.md)分别。

中的一个分支[设备树](device-tree.md)（其包含叶 devnode 和 devnodes 的父级、 祖父，等等），驱动程序必须相互协作，确保等待/唤醒 IRP 达到可以让所有必要的驱动程序唤醒的硬件。

ACPI 在计算机上，ACPI 负责启用与从每个叶设备的唤醒信号相关联的特定于系统的常规用途事件 (GPE) 寄存器。 因此，驱动程序必须请求，并且正等待/唤醒 Irp 直到一位达到 ACPI 筛选器驱动程序 （在启动时设备堆栈中插入） 或基础[Windows ACPI 驱动程序](acpi-driver.md)，Acpi.sys。 在响应中，ACPI 启用注册，直到该信号到达时，然后完成 IRP 保存挂起的 IRP。 ACPI 可以响应唤醒信号，因为它不转发 IRP 到较低的驱动程序。

ACPI 筛选器驱动程序，如基础 ACPI 驱动程序本身，是透明的其他驱动程序。 若要提供硬件设计中最大的灵活性，在任何设备堆栈中的 ACPI 筛选器驱动程序的准确位置是特定于设备和系统。 在设计时驱动程序，不能进行任何假设设备堆栈中的 ACPI 筛选器位置存在。

请注意，枚举子级的驱动程序创建一个 PDO 为每个孩子的设备和父设备 FDO。 因此，该驱动程序充当子设备的总线驱动程序和父设备函数驱动程序/策略所有者。 因此，只要总线驱动程序收到子 PDO 等待/唤醒 IRP，它应请求另一个等待/唤醒 IRP 与其父 PDO。

### <a href="" id="sample-usb-configuration"></a>

下图显示了示例配置中发生这种情况。

![说明示例 usb 配置关系图](images/wwhw.png)

在此示例配置、 键盘和调制解调器是 USB 集线器，又是 USB 主控制器，由 PCI 总线枚举的子级的子级。 下图显示的示例配置中的键盘的设备堆栈。

![说明示例 usb 键盘配置的设备堆栈的关系图](images/wwdobj.png)

上一图所示，从底部读取：

1.  [Windows ACPI 驱动程序](acpi-driver.md)，Acpi.sys，为 PCI 创建 PDO。

2.  PCI 驱动程序创建 PCI FDO 和 USB 主控制器 PDO，拥有 PCI 设备堆栈的策略。

3.  USB 主控制器驱动程序 （主机端口/微型端口驱动程序对） 创建 USB 主机控制器 FDO 和 USB 集线器 PDO。 它拥有 USB 主机控制器设备堆栈的策略。 请注意 Acpi.sys 以及此堆栈中创建筛选器执行操作。

4.  USB 集线器驱动程序创建 USB 集线器 FDO 和键盘 PDO。 此驱动程序拥有 USB 集线器设备堆栈的电源策略。

5.  功能驱动程序适用于键盘是 USB HID 类驱动程序/微型驱动程序对。 此驱动程序创建适用于键盘 FDO 并拥有其电源策略。 由于键盘不具有任何子设备，此驱动程序会创建没有 PDOs。

请注意，每个设备堆栈可能包含未显示的其他可选的筛选器 DOs。

若要允许键盘输入来唤醒系统，适用于键盘的策略所有者请求**IRP\_MN\_等待\_唤醒**对其 PDO。 下图中所示，该 IRP 引起其他等待/唤醒 Irp，一系列设置。

![等待/唤醒 irp 请求有关 usb 的示例配置](images/wwcascade.png)

当总线驱动程序收到[ **IRP\_MN\_等待\_唤醒**](https://msdn.microsoft.com/library/windows/hardware/ff551766)针对其创建 PDO，它必须请求另一个**IRP\_MN\_等待\_唤醒**设备 stack 为其拥有的电源策略并创建 FDO。

上一图所示：

1.  键盘驱动程序调用[ **PoRequestPowerIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff559734)发送等待/唤醒到其 PDO IRP (IRP1)。

    电源管理器分配 IRP，并将其通过 I/O 管理器发送到键盘设备堆栈的顶部。 驱动程序集[ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354)例程并传递 IRP 下堆栈，直到它达到键盘 PDO。 USB 集线器驱动程序，它相当于键盘的总线驱动程序，保存挂起的 IRP1。

2.  由于唤醒信号到达时，USB 集线器驱动程序不能将系统唤醒，USB 集线器驱动程序必须调用**PoRequestPowerIrp**请求等待/唤醒 IRP (IRP2) 的 USB 集线器设备堆栈。

    电源管理器将此 IRP 发送到 USB 集线器设备堆栈的顶部。 在此驱动程序堆栈集*IoCompletion*例程，并传递到 USB IRP 托管控制器驱动程序 （充当 USB 集线器的总线驱动程序）。 USB 主控制器驱动程序保留 IRP2 挂起，直到键盘向唤醒事件发出信号。

3.  同样，USB 主控制器驱动程序不能将系统唤醒，因此 USB 主控制器驱动程序调用**PoRequestPowerIrp**发送等待/唤醒 IRP (IRP3) 与 USB 托管控制器设备堆栈。

    电源管理器将发送此 IRP 到 USB 主控制器的顶部设备堆栈驱动程序在其中设置*IoCompletion*例程，并传递 IRP 向 PCI 驱动程序 （充当 USB 集线器的总线驱动程序）。 PCI 驱动程序保留 IRP3 挂起，直到键盘向唤醒事件发出信号。

4.  PCI 驱动程序无法唤醒系统，这样 PCI 驱动程序可以调用**PoRequestPowerIrp**发送等待/唤醒 IRP (IRP4) 到 PCI 设备堆栈。 其父级是 ACPI 是总线驱动程序在根设备。

    电源管理器将 IRP 发送到堆栈顶部的 PCI 总线设备;其驱动程序设置完成例程，并将传递到 IRP [Windows ACPI 驱动程序](acpi-driver.md)，Acpi.sys。

5.  Acpi.sys 可以唤醒系统，因此它不会等待/唤醒 IRP 发送到任何其他 PDO。 Acpi.sys 保留 IRP4 挂起，直到到达唤醒信号。

当键盘断言唤醒信号时，Acpi.sys 截取它。 ACPI，但是，不能确定键盘添加仅的信号是通过根设备的信号。 Acpi.sys 然后完成 IRP4，并在 I/O 管理器调用*IoCompletion*例程旅行备份 PCI 设备堆栈。 IRP4 完毕和全部*IoCompletion*例程已运行，调用 PCI 驱动程序的回调例程。 在其回调例程中，PCI 驱动程序确定信号是通过 USB 主控制器。 PCI 驱动程序然后完成 IRP3。 键盘驱动程序收到 IRP1 之前，通过 USB 主机控制器堆栈和 USB 集线器堆栈，会发生相同的序列。 现在，键盘驱动程序可以唤醒事件，根据需要提供服务。

必须设置一个驱动程序将等待/唤醒 IRP 发送到父 PDO，每次[*取消*](https://msdn.microsoft.com/library/windows/hardware/ff540742)自己 IRP 的例程。 设置*取消*例程，该驱动程序有机会取消新 IRP，如果触发了该 IRP 已取消。 在 USB 示例中，如果键盘驱动程序取消其等待/唤醒 IRP （从而禁用键盘唤醒），则 USB 集线器、 USB 主控制器和 PCI 驱动程序必须取消它们由于键盘 IRP 发送 Irp。 有关详细信息，请参阅[取消的等待/唤醒 Irp 的例程](canceling-a-wait-wake-irp.md#ddk-cancel-routines-for-wait-wake-irps-kg)。

尽管父驱动程序可能会枚举可以等待/唤醒启用的多个子级，但只有一个等待/唤醒 IRP 可以处于挂起状态对 PDO。 在这种情况下，父驱动程序应确保它保持等待/唤醒 IRP 挂起时的任何其设备为启用了唤醒。 若要执行此操作，该驱动程序内部每次递增计数器收到等待/唤醒 IRP。 每次该驱动程序完成后等待/唤醒 IRP，它递减计数和结果值为非零值，如果将另一个等待/唤醒 IRP 发送到其设备堆栈。

例如，在前面所演示的 USB 配置[USB 的示例配置](#sample-usb-configuration)图，USB 集线器枚举两个设备、 键盘和调制解调器。 当 USB 集线器驱动程序收到等待/唤醒 IRP 适用于键盘 PDO 时，它对自己 PDO 请求 IRP 之前递增等待/唤醒 Irp 的计数。 如果调制解调器的策略所有者更高版本启用了唤醒调制解调器，USB 集线器驱动程序等待新的调制解调器 PDO IRP 并增加其等待/唤醒的引用计数。 但是，因为 USB 集线器 PDO 不能包含两个同时挂起的等待唤醒 Irp，USB 集线器驱动程序不会请求新等待/唤醒 IRP 的 USB 集线器 PDO。

USB 集线器驱动程序从键盘或调制解调器唤醒信号时，确定哪些设备发出信号，完成相应 IRP，并减少其引用计数。 由于已为唤醒启用这两种设备 （并且因此其引用计数为非零值），它必须发送另一个等待/唤醒 IRP 以"rearm"唤醒自己 PDO 自己设备的堆栈。 （这同样适用的 USB 主控制器和 PCI 驱动程序。）

驱动程序不，但是，发送本身 IRP 以重新启用等待/唤醒的唤醒信号刚到在同一设备上。 仅设备电源策略管理器可以执行该操作。 不自动重新启用等待/唤醒。

 

 




