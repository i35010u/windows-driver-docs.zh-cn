---
title: Acpi .sys Windows ACPI 驱动程序
description: Windows ACPI 驱动程序 sys.databases 是 Windows 操作系统的收件箱组件。
ms.assetid: 38ca54e0-defe-48b2-ab00-a5f688c2eb01
keywords:
- ACPI 驱动程序 WDK 电源管理
- 枚举器 WDK 电源管理
- PDOs WDK 电源管理
- 筛选 DOs WDK 电源管理
- 物理设备对象 WDK 电源管理
ms.date: 06/16/2017
ms.localizationpriority: High
ms.openlocfilehash: f43a17c54033fd82a2f21596013571fcf658a4d0
ms.sourcegitcommit: c73954a5909ec8c7e189f77fd5813f2eb749687c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/07/2019
ms.locfileid: "72007636"
---
# <a name="acpisys-the-windows-acpi-driver"></a>Acpi.sysWindows ACPI 驱动程序


Windows ACPI 驱动程序 sys.databases 是 Windows 操作系统的收件箱组件。 Acpi 的责任包括对电源管理和即插即用（PnP）设备枚举的支持。 在具有[ACPI BIOS](acpi-bios.md)的硬件平台上， [HAL](windows-kernel-mode-hal-library.md)会导致在系统启动过程中从[设备树](device-tree.md)的基础加载 ACPI。 Acpi 作为操作系统和 ACPI BIOS 之间的接口。 对于设备树中的其他驱动程序，Acpi 是透明的。

Acpi 在特定硬件平台上执行的其他任务可能包括 reprogramming COM 端口的资源或启用 USB 控制器进行系统唤醒。

**本主题中的**

-   [ACPI 设备](#acpi-devices)
-   [ACPI 控制方法](#acpi-control-methods)
-   [ACPI 规范](#acpi-specification)
-   [ACPI 调试](#acpi-debugging)

## <a name="acpi-devices"></a>ACPI 设备


硬件平台供应商在 ACPI BIOS 中指定 ACPI 命名空间的层次结构，以描述平台的硬件拓扑。 有关详细信息，请参阅[ACPI 命名空间层次结构](https://docs.microsoft.com/windows-hardware/drivers/bringup/acpi-namespace-hierarchy)。

对于 ACPI 命名空间层次结构中所述的每个设备，Windows ACPI 驱动程序，Acpi 都创建筛选器设备对象（筛选器）或物理设备对象（PDO）。 如果设备已集成到系统板中，则 Acpi 会创建一个代表 ACPI 总线筛选器的筛选器设备对象，然后将其直接连接到总线驱动程序（PDO）上方的设备堆栈。 对于 ACPI 命名空间中所述但在系统板上没有的其他设备，Acpi 会创建 PDO。 Acpi 通过这些设备对象，将电源管理和 PnP 功能提供给设备堆栈。 有关详细信息，请参阅[ACPI 设备的设备堆栈](https://docs.microsoft.com/windows-hardware/drivers/acpi/device-stacks-for-an-acpi-device)。

Acpi .sys 为其创建设备对象的设备称为[Acpi 设备](https://docs.microsoft.com/windows-hardware/drivers/acpi/supporting-acpi-devices)。 ACPI 设备集在硬件平台与下一平台之间有所不同，具体取决于 ACPI BIOS 和主板的配置。 请注意，Acpi 只为 ACPI 命名空间中所述的设备加载 ACPI 总线筛选器，并且该筛选器将永久连接到硬件平台（通常情况下，此设备已集成到核心硅或焊接到系统板中）。 并非所有主板设备都具有 ACPI 总线筛选器。

所有 ACPI 功能对于更高级别的驱动程序都是透明的。 这些驱动程序不得假设任何指定设备堆栈中是否存在 ACPI 筛选器。

Acpi 和 ACPI BIOS 支持 ACPI 设备的基本功能。 若要增强 ACPI 设备的功能，设备供应商可以提供 WDM 函数驱动程序。 有关详细信息，请参阅[ACPI 设备功能驱动程序的操作](https://docs.microsoft.com/windows-hardware/drivers/acpi/operation-of-an-acpi-device-function-driver)。

ACPI 设备由 ACPI BIOS 中[系统描述表](https://docs.microsoft.com/windows-hardware/drivers/bringup/acpi-system-description-tables)中的定义块指定。 设备的定义块指定操作区域，这是一个用于访问设备数据的连续设备内存块。 只有 sys.databases 会修改操作区域中的数据。 设备的函数驱动程序可以读取操作区域中的数据，但不能修改数据。 调用时，[操作区域处理程序](https://docs.microsoft.com/windows-hardware/drivers/acpi/implementing-an-operation-region-handler)会将操作区域中的字节传输到 Acpi 中的数据缓冲区。 函数驱动程序和 Acpi 的组合操作是特定于设备的，由硬件供应商在 ACPI BIOS 中定义。 通常，函数驱动程序和 Acpi 可访问操作区域中的特定区域，以执行特定于设备的操作并检索信息。 有关详细信息，请参阅[支持操作区域](https://docs.microsoft.com/windows-hardware/drivers/acpi/supporting-an-operation-region)。

## <a name="acpi-control-methods"></a>ACPI 控制方法


ACPI 控制方法是声明和定义简单操作以查询和配置 ACPI 设备的软件对象。 控制方法存储在 ACPI BIOS 中，并以称为 ACPI 机器语言（AML）的字节代码格式进行编码。 设备的控制方法从系统固件加载到内存中的设备 ACPI 命名空间，并由 Windows ACPI 驱动程序 sys.databases 解释。

若要调用控制方法，ACPI 设备的内核模式驱动程序将启动[**IRP @ no__t-2mj-zl-ntd @ no__t-3DEVICE @ no__t**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)请求，该请求由 ACPI 处理。 对于在 ACPI 枚举设备上加载的驱动程序，Acpi 始终实现驱动程序堆栈中的物理设备对象（PDO）。 有关详细信息，请参阅[评估 ACPI 控制方法](https://docs.microsoft.com/windows-hardware/drivers/acpi/evaluating-acpi-control-methods)。

## <a name="acpi-specification"></a>ACPI 规范


有关最新的*高级配置和电源接口规范*，请参阅统一可扩展固件接口论坛网站上提供的[ACPI 5.0 规范](https://uefi.org/specifications)。 ACPI 规范的修订版本5.0 引入了一组功能，用于支持基于芯片（SoC）集成线路上的系统并实现[连接待机](https://docs.microsoft.com/windows-hardware/design/device-experiences/modern-standby)电源型号的低功耗移动 pc。 自 Windows 8 和 Windows 8.1 起，Windows ACPI 驱动程序 sys.databases 支持 ACPI 5.0 规范中的新增功能。 有关详细信息，请参阅[用于 SoC 平台的 WINDOWS ACPI 设计指南](https://docs.microsoft.com/windows-hardware/drivers/bringup/windows-acpi-design-guide-for-soc-platforms)。

## <a name="acpi-debugging"></a>ACPI 调试


系统集成商和 ACPI 设备驱动程序开发人员可以使用 Microsoft [AMLI 调试器](https://docs.microsoft.com/windows-hardware/drivers/debugger/introduction-to-the-amli-debugger)来调试 AML 代码。 由于 AML 是一种解释型语言，因此 AML 调试需要特殊的软件工具。 Windows ACPI 驱动程序的已检查版本（Acpi）包含支持 AML 调试的调试器组件。 有关 AMLI 调试器的详细信息，请参阅[ACPI 调试](https://docs.microsoft.com/windows-hardware/drivers/debugger/acpi-debugging)。 有关如何下载 Windows 的已检查生成的信息，请参阅[下载 windows 的已检查生成](https://docs.microsoft.com/windows-hardware/drivers/devtest/obtaining-the-checked-build)。 有关将 ACPI 源语言（ASL）编译为 AML 的信息，请参阅[MICROSOFT ASL 编译器](https://docs.microsoft.com/windows-hardware/drivers/bringup/microsoft-asl-compiler)。

 

 




