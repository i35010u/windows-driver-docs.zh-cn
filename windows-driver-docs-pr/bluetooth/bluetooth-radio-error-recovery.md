---
title: 蓝牙无线收发器重置和恢复
description: 蓝牙无线电自动错误恢复机制
keywords:
- 蓝牙无线电错误恢复
- 蓝牙 PLDR
ms.date: 09/18/2019
ms.localizationpriority: medium
ms.openlocfilehash: 8f484eeaba2de84e266e5a7caca1b8274cefb52e
ms.sourcegitcommit: 937974aa9bbe0262a7ffe9631593fab48c4e7492
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2020
ms.locfileid: "90009913"
---
# <a name="bluetooth-radio-reset-and-recovery"></a>蓝牙无线收发器重置和恢复

蓝牙无线电重置和恢复是 Windows 10 版本1803及更高版本中的一项技术，为蓝牙无线电收发器引入了强大的重置和恢复机制。 此机制使蓝牙无线收发器能够从导致故障、失去连接或无响应操作命令的硬件故障中恢复。 目标是自动恢复广播，使用户体验无缝，同时降低需要系统重新启动的可能性。

蓝牙无线电重置和恢复可以通过或不带固件依赖项实现。 IHV 或 OEM 合作伙伴可以使用受支持的设备或固件级重置机制来扩展所有 Windows 电脑上可用的基于软件的重置机制，以增加成功恢复的可能性。

> [!IMPORTANT]
> **本主题适用于开发人员。** 如果你是遇到蓝牙问题的客户，请参阅 [修复 Windows 10 中的蓝牙问题](https://support.microsoft.com/help/14169/windows-10-fix-bluetooth-problems)。

## <a name="bluetooth-reset-and-recovery-scenarios"></a>蓝牙重置和恢复方案

有三大类别的问题需要启动蓝牙重置和恢复：

- **总线枚举故障：** 无线电无法通过蓝牙的基础总线 (进行枚举或重新枚举，这通常是 USB 或 UART) ，如 " _可视失败状态_ " 中所示 (黄色感叹号) 在设备管理器中，这可能是底层硬件错误的征兆。

- **驱动程序枚举失败：** 基础总线成功枚举 _后_ ，蓝牙无线电处于失败状态。 这通常发生在为收音机构建驱动程序堆栈时，例如，当在蓝牙无线电设备节点上安装了筛选器或函数驱动程序时 (devnode) 。 如果驱动程序在一个或多个启动操作过程中遇到错误，则会发生故障，因此会报告 PnP 故障。 此类操作的一个示例可能是设备的固件下载。

- **非枚举失败：** 设备未处于故障状态，但不能正常运行，如驱动程序堆栈所示。 这些是枚举路径以外的故障，可能是一般的关键传输特定故障或特定于设备的故障，例如灾难性固件错误。 在这些情况下，将使用下面所述的蓝牙重置和恢复机制。

## <a name="reset-and-recovery-mechanisms"></a>重置和恢复机制

尽管有不同的方法可从失败状态进行恢复，但蓝牙仍使用基于 ACPI 的标准恢复机制来尝试将无线电恢复到工作状态。

[GUID_DEVICE_RESET_INTERFACE_STANDARD](../kernel/working-with-guid-device-reset-interface-standard.md) 定义了两个重置级别。 请注意：

- 重置机制仅适用于 **内部设备** ，因此不支持外部可插入蓝牙无线电收发器（如连接器）。

- 重置机制需要在 Windows (中同时支持这两种功能：通常由函数驱动程序堆栈) 并且底层固件 (通常在 ACPI BIOS) 中执行重置。

- 实际的重置机制是特定于系统的机制。

| 重置级别 | 实现 |
| --- | --- |
| 功能级设备重置 (FLDR)  | 重置操作仅限于特定设备，不适用于其他设备。 没有重新枚举。 函数驱动程序必须假设硬件在操作后恢复为其原始状态。  不保留中间状态。
| 平台级别设备重置 (PLDR)  | Reset 操作会影响特定设备以及通过相同的电源导轨或重置线路连接到该设备的所有其他设备。 Reset 操作导致从总线中将设备报告为缺失，并重新枚举设备。 这种类型的重置对系统的影响最大，因为共享资源的所有设备都将恢复到其原始状态。|

- **若要支持 FLDR** ，必须在_ADR_ 命名空间中定义一个 __RST 方法，如 [ACPI 固件：功能级重置](../kernel/resetting-and-recovering-a-device.md#acpi-firmware-function-level-reset)中所述。

- **若要支持 PLDR** ，必须在_ADR_ 命名空间中定义 _RST 或 _PR3 方法，如 [ACPI 固件：平台级重置](../kernel/resetting-and-recovering-a-device.md#acpi-firmware-platform-level-reset)。 请注意，如果使用的是 __PR3_ 方法，ACPI 将使用 D3Cold 电源周期机制重置。 这会模拟设备断电，并随后将其还原。 如果任何其他设备共享相同的电源导轨，则它们也会重置。 如果 __PRR_ () PowerResource 定义和引用 __RST_方法，则使用该 PowerResource 的所有设备将受到影响。

  - 由于 PLDR 仅适用于内部设备，因此必须在 ACPI 中将其声明为。 对于 USB 设备，若要指定内部 (用户看不到的端口) 并且可以连接到集成设备，请设置 __UPC。PortIsConnectable_ byte 到0xff 和 __PLD。UserVisible_ 位到0。

  - 如果将 __PR3_ (D3Cold) 机制用于 PLDR，请确保 SystemWake 和 DeviceWake 等方案继续工作。 通常，这意味着为 D2 定义了适当的电源资源，例如 __pr2) _。 下表是一项有用的指南：

| 电源状态 | ACPI 资源 | 行为 |  
| --- | --- | --- |  
| D2 | _PR2 | 此状态的类定义缩减功能所需的任何电源或时钟。 |  
| D3 热 (reqd。 )  | _PR2 | 与 (D2，D1 或 D0) 支持的下一个更高状态相同的资源。 |  
| D3cold | _PR3 | 仅设备在其总线上显示和响应特定于总线的命令所需的电源或时钟。|  

### <a name="related-links"></a>相关链接

[重置和恢复设备](../kernel/resetting-and-recovering-a-device.md)