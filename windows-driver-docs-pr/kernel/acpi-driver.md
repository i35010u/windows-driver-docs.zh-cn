---
title: Windows ACPI 驱动程序 Acpi.sys
description: Windows ACPI 驱动程序 Acpi.sys 是 Windows 操作系统的收件箱组件。
ms.assetid: 38ca54e0-defe-48b2-ab00-a5f688c2eb01
keywords:
- ACPI 驱动程序 WDK 电源管理
- 枚举器 WDK 电源管理
- PDO WDK 电源管理
- 筛选器 DO WDK 电源管理
- 物理设备对象 WDK 电源管理
ms.date: 06/16/2017
ms.localizationpriority: High
ms.openlocfilehash: e5f294bf41358d1050e080ffa675283a5e9a8534
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89192265"
---
# <a name="acpisys-the-windows-acpi-driver"></a>Acpi.sysWindows ACPI 驱动程序


Windows ACPI 驱动程序 Acpi.sys 是 Windows 操作系统的收件箱组件。 Acpi.sys 的责任包括对电源管理和即插即用 (PnP) 设备枚举的支持。 在具有 [ACPI BIOS](acpi-bios.md) 的硬件平台上，[HAL](windows-kernel-mode-hal-library.md) 会导致系统启动期间在[设备树](device-tree.md)底部加载 Acpi.sys。 Acpi.sys 用作操作系统和 ACPI BIOS 之间的接口。 Acpi.sys 对设备树中的其他驱动程序透明。

Acpi.sys 在特定硬件平台上执行的其他任务可能包括对 COM 端口的资源重新编程或启用 USB 控制器以进行系统唤醒。

**本主题内容**

-   [ACPI 设备](#acpi-devices)
-   [ACPI 控制方法](#acpi-control-methods)
-   [ACPI 规范](#acpi-specification)
-   [ACPI 调试](#acpi-debugging)

## <a name="acpi-devices"></a>ACPI 设备


硬件平台供应商在 ACPI BIOS 中指定 ACPI 命名空间的层次结构，以描述平台的硬件拓扑。 有关详细信息，请参阅 [ACPI 命名空间层次结构](../bringup/acpi-namespace-hierarchy.md)。

对于 ACPI 命名空间层次结构中所述的每个设备，Windows ACPI 驱动程序 Acpi.sys 均会创建一个筛选器设备对象（筛选器 DO）或一个物理设备对象 (PDO)。 如果设备已集成到系统板中，则 Acpi.sys 会创建一个表示 ACPI 总线筛选器的筛选器设备对象，然后将其附加到设备堆栈中总线驱动程序 (PDO) 的正上方。 对于 ACPI 命名空间中已描述但系统板上不存在的其他设备，Acpi.sys 会创建 PDO。 Acpi.sys 通过这些设备对象将电源管理和 PnP 功能提供给设备堆栈。 有关详细信息，请参阅 [ACPI 设备的设备堆栈](../acpi/device-stacks-for-an-acpi-device.md)。

Acpi.sys 为之创建设备对象的设备称为 [ACPI 设备](../acpi/supporting-acpi-devices.md)。 ACPI 设备集因硬件平台而异，具体取决于 ACPI BIOS 和主板的配置。 请注意，Acpi.sys 只为 ACPI 命名空间中已描述且永久连接到硬件平台的设备（通常情况下，此设备已集成到核心芯片或焊接到系统板中）加载 ACPI 总线筛选器。 并非所有主板设备都具有 ACPI 总线筛选器。

所有 ACPI 功能对于更高级别的驱动程序都是透明的。 这些驱动程序不得假设任何指定设备堆栈中是否存在 ACPI 筛选器。

Acpi.sys 和 ACPI BIOS 支持 ACPI 设备的基本功能。 为增强 ACPI 设备的功能，设备供应商可以提供 WDM 功能驱动程序。 有关详细信息，请参阅 [ACPI 设备函数驱动程序的操作](../acpi/operation-of-an-acpi-device-function-driver.md)。

ACPI 设备由 ACPI BIOS 的[系统说明表](../bringup/acpi-system-description-tables.md)中的定义块指定。 设备的定义块还指定操作区域（一个用于访问设备数据的连续设备内存块）等等。 只有 Acpi.sys 会修改操作区域中的数据。 设备的函数驱动程序可以读取操作区域中的数据，但不能修改数据。 调用时，[操作区域处理程序](../acpi/implementing-an-operation-region-handler.md)会在操作区域和 Acpi.sys 中的数据缓冲区之间来回传输字节。 函数驱动程序和 Acpi.sys 的组合操作特定于设备，由硬件供应商在 ACPI BIOS 中定义。 通常，函数驱动程序和 Acpi.sys 会访问操作区域中的特定区域，以执行特定于设备的操作并检索信息。 有关详细信息，请参阅[支持操作区域](../acpi/supporting-an-operation-region.md)。

## <a name="acpi-control-methods"></a>ACPI 控制方法


ACPI 控制方法是软件对象，用于声明和定义简单操作以查询和配置 ACPI 设备。 控制方法存储在 ACPI BIOS 中，并以称为 ACPI 机器语言 (AML) 的字节代码格式编码。 设备的控制方法从系统固件加载到内存中的设备 ACPI 命名空间，并由 Windows ACPI 驱动程序 Acpi.sys 解释。

为了调用控制方法，ACPI 设备的内核模式驱动程序将启动一个 [**IRP\_MJ\_DEVICE\_CONTROL**](./irp-mj-device-control.md) 请求，该请求由 Acpi.sys 处理。 对于 ACPI 枚举的设备上加载的驱动程序，Acpi.sys 始终会在驱动程序堆栈中实现相应的物理设备对象 (PDO)。 有关详细信息，请参阅[评估 ACPI 控制方法](../acpi/evaluating-acpi-control-methods.md)。

## <a name="acpi-specification"></a>ACPI 规范


有关最新的*高级配置和电源接口规范*，请参阅“统一可扩展固件接口论坛”网站上的 [ACPI 5.0 规范](https://uefi.org/specifications)。 ACPI 规范 5.0 修订版引入了一组功能，这些功能用于支持基于系统单芯片 (SoC) 集成电路并实现了[连接待机](/windows-hardware/design/device-experiences/modern-standby)电源模型的低功耗移动电脑。 自 Windows 8 和 Windows 8.1 起，Windows ACPI 驱动程序 Acpi.sys 支持 ACPI 5.0 规范中的新增功能。 有关详细信息，请参阅 [SoC 平台的 Windows ACPI 设计指南](../bringup/windows-acpi-design-guide-for-soc-platforms.md)。

## <a name="acpi-debugging"></a>ACPI 调试


系统集成商和 ACPI 设备驱动程序开发人员可以使用 Microsoft [AMLI 调试器](../debugger/introduction-to-the-amli-debugger.md)调试 AML 代码。 由于 AML 是一种解释型语言，因此 AML 调试需要特殊的软件工具。

有关 AMLI 调试器的详细信息，请参阅 [ACPI 调试](../debugger/acpi-debugging.md)。

有关将 ACPI 源语言 (ASL) 编译到 AML 中的信息，请参阅 [Microsoft ASL 编译器](../bringup/microsoft-asl-compiler.md)。

 

