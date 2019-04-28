---
title: Acpi.sys Windows ACPI 驱动程序
description: Windows ACPI 驱动程序，Acpi.sys，是 Windows 操作系统的收件箱组件。
ms.assetid: 38ca54e0-defe-48b2-ab00-a5f688c2eb01
keywords:
- ACPI 驱动程序 WDK 电源管理
- 枚举器 WDK 电源管理
- PDOs WDK 电源管理
- 筛选器 DOs WDK 电源管理
- 物理设备对象 WDK 电源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: ee177f689b1deebcd1b1fbe275a15686d3304f0a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63339108"
---
# <a name="acpisys-the-windows-acpi-driver"></a>Acpi.sysWindows ACPI 驱动程序


Windows ACPI 驱动程序，Acpi.sys，是 Windows 操作系统的收件箱组件。 Acpi.sys 的职责包括电源管理的支持和即插即用 (PnP) 设备枚举。 有的硬件平台上[ACPI BIOS](acpi-bios.md)，则[HAL](windows-kernel-mode-hal-library.md)会导致要在位于底部的系统启动期间加载的 Acpi.sys[设备树](device-tree.md)。 Acpi.sys 充当操作系统和 ACPI BIOS 之间的接口。 Acpi.sys 是透明的设备树中的其他驱动程序。

Acpi.sys 特定的硬件平台上执行其他任务可能包括重新编程 COM 端口的资源或使系统唤醒的 USB 控制器。

**本主题中**

-   [ACPI 设备](#acpi-devices)
-   [ACPI 控制方法](#acpi-control-methods)
-   [ACPI 规范](#acpi-specification)
-   [ACPI 调试](#acpi-debugging)

## <a name="acpi-devices"></a>ACPI 设备


硬件平台供应商来描述该平台的硬件拓扑在 ACPI BIOS 中指定 ACPI 命名空间的层次的结构。 有关详细信息，请参阅[ACPI Namespace 层次结构](https://msdn.microsoft.com/library/windows/hardware/dn495659)。

对于在 ACPI 命名空间层次结构中所述的每个设备，Windows ACPI 驱动程序，Acpi.sys，创建筛选器设备对象 （筛选器执行操作） 或物理设备对象 (PDO)。 如果设备已集成到系统主板，Acpi.sys 创建筛选器设备对象，表示一个 ACPI 总线筛选器，并将其附加到设备堆栈上面总线驱动程序 (PDO)。 对于所述在 ACPI 名称空间中，但不是在系统板上的其他设备，Acpi.sys 创建 PDO 实例。 Acpi.sys 提供电源管理和设备堆栈的即插即用功能通过这些设备对象。 有关详细信息，请参阅[ACPI 设备的设备堆栈](https://msdn.microsoft.com/library/windows/hardware/ff536137)。

为其 Acpi.sys 创建设备对象的设备称为[ACPI 设备](https://msdn.microsoft.com/library/windows/hardware/ff536161)。 ACPI 设备集到下一步，从不同的硬件平台而异，依赖于 ACPI BIOS 和主板的配置。 请注意 Acpi.sys 加载的 ACPI 总线筛选器只在 ACPI 名称空间中所述和永久连接到的硬件平台的设备 （通常情况下，此设备已集成到核心硅或焊接到系统板）。 并非所有主板设备都具有 ACPI 总线筛选器。

所有 ACPI 功能都是透明的更高级别的驱动程序。 这些驱动程序必须在任何给定的设备堆栈中进行的 ACPI 筛选器存在任何假设。

Acpi.sys 和 ACPI BIOS 支持 ACPI 设备的基本功能。 若要增强的 ACPI 设备功能，设备供应商可以提供 WDM 功能驱动程序。 有关详细信息，请参阅[ACPI 设备功能驱动程序操作](https://msdn.microsoft.com/library/windows/hardware/ff536152)。

由定义块中指定的 ACPI 设备[系统说明表](https://msdn.microsoft.com/library/windows/hardware/dn495660)ACPI BIOS 中。 此外，设备的定义块指定的操作区域，这是一个用来访问设备数据的设备内存的连续块。 仅 Acpi.sys 修改操作区域中的数据。 设备的功能驱动程序可以读取操作区域中的数据，但不能修改数据。 调用时，[的操作区域处理程序](https://msdn.microsoft.com/library/windows/hardware/ff536143)传输到和从 Acpi.sys 中的数据缓冲区的操作区域中的字节。 功能驱动程序和 Acpi.sys 的组合的操作是特定于设备的和由硬件供应商定义的 ACPI BIOS 中。 一般情况下，功能驱动程序和 Acpi.sys 访问以执行特定于设备的操作和检索信息的操作区域中的特定区域。 有关详细信息，请参阅[支持运营区域](https://msdn.microsoft.com/library/windows/hardware/ff536162)。

## <a name="acpi-control-methods"></a>ACPI 控制方法


ACPI 控制方法是声明和定义简单操作，以便查询和配置 ACPI 设备的软件对象。 控制方法存储在 ACPI BIOS 中，并调用 ACPI 机器语言 (AML) 字节代码格式进行编码。 设备的控制方法是从系统固件加载到内存中的设备的 ACPI 名称空间，并由 Windows ACPI 驱动程序，Acpi.sys 解释。

若要调用的控制方法，ACPI 设备内核模式驱动程序将启动[ **IRP\_MJ\_设备\_控制**](https://msdn.microsoft.com/library/windows/hardware/ff550744) Acpi.sys 由处理的请求。 有关在 ACPI 枚举设备上加载的驱动程序，Acpi.sys 始终实现物理设备对象 (PDO) 中驱动程序堆栈。 有关详细信息，请参阅[评估 ACPI 控制方法](https://msdn.microsoft.com/library/windows/hardware/ff536139)。

## <a name="acpi-specification"></a>ACPI 规范


有关最新*高级配置和电源接口规范*，请参阅[ACPI 5.0 规范](https://www.uefi.org/specifications)统一可扩展固件接口论坛网站中提供。 ACPI 规范的修订 5.0 引入了一组功能，可支持芯片 (SoC) 集成线路上基于系统和实现的低功率的移动 Pc[连接待机](https://msdn.microsoft.com/library/windows/hardware/mt282515)电源模型。 从 Windows 8 和 Windows 8.1 Windows ACPI 驱动程序，Acpi.sys，支持 ACPI 5.0 规范中的新功能。 有关详细信息，请参阅[SoC 平台的 Windows ACPI 设计指南](https://msdn.microsoft.com/library/windows/hardware/dn495676)。

## <a name="acpi-debugging"></a>ACPI 调试


系统集成商和 ACPI 设备驱动程序开发人员可以使用 Microsoft [AMLI 调试器](https://msdn.microsoft.com/library/windows/hardware/ff551079)AML 代码进行调试。 由于 AML 是解释性的语言，AML 调试需要特殊软件工具。 检查的版本的 Windows ACPI 驱动程序，Acpi.sys，包含一个调试器组件以支持 AML 调试。 有关 AMLI 调试器的详细信息，请参阅[ACPI 调试](https://msdn.microsoft.com/library/windows/hardware/ff537808)。 有关如何下载 Windows 调试内部版本的信息，请参阅[下载检查生成的 Windows](https://msdn.microsoft.com/library/windows/hardware/ff549603)。 有关编译成 AML ACPI 源语言 (ASL) 的信息，请参阅[Microsoft ASL Compiler](https://msdn.microsoft.com/library/windows/hardware/dn551195)。

 

 




