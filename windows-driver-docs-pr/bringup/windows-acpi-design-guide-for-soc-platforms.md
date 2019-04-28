---
title: SoC 平台的 Windows ACPI 设计指南
description: ACPI 5.0 定义新功能，可支持基于实现连接待机电源模型的 SoC ICs 的低功率的移动设备。
ms.assetid: 661BFB7E-D190-450D-A466-7D6AD0EAAAB0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c6479aa3ec938df80a873bac6f9dbad01f2f475a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63337324"
---
# <a name="windows-acpi-design-guide-for-soc-platforms"></a>SoC 平台的 Windows ACPI 设计指南


高级配置和电源接口规格 5.0 修正版（[ACPI 5.0 规格](https://www.uefi.org/specifications)）定义了一组新的功能，这些功能可以支持低功耗的移动设备，而这些移动设备则基于系统单芯片 (SoC) 集成电路并实现了连接待机电源模型。 从 Windows 8 和 Windows 8.1 开始，Windows 支持 SoC 基于平台的新 ACPI 5.0 的功能。

本部分包含 Windows Pc 和设备支持 ACPI 5.0 规范中的新功能的实现准则。 固件开发人员和系统设计人员可以使用这些准则以确保 Windows 在其平台上正常运行。 所有 Windows 固件要求的列表，请参阅的文档[Windows 认证计划](https://go.microsoft.com/fwlink/p/?linkid=227314)。

## <a name="in-this-section"></a>本节内容


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>主题</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="overview-of-windows-support-for-acpi-5-0.md" data-raw-source="[Overview of Windows support for ACPI 5.0](overview-of-windows-support-for-acpi-5-0.md)">ACPI 5.0 的 Windows 支持概述</a></p></td>
<td><p><a href="https://www.uefi.org/specifications" data-raw-source="[ACPI 5.0 specification](https://www.uefi.org/specifications)">ACPI 5.0 规范</a>支持基于 SoC 的移动平台的运行 Windows 8 和更高版本，但继续支持早期版本 Windows 中引入了许多有用的功能。 此设计指南将定向到专门适用于 SoC 基于平台的组成部分 ACPI 5.0 的实施者，并且介绍了在 ACPI 在这些平台上运行 Windows 中实现特定于 SoC 的功能的最佳做法。</p></td>
</tr>
<tr class="even">
<td><p><a href="acpi-system-description-tables.md" data-raw-source="[ACPI system description tables](acpi-system-description-tables.md)">ACPI 系统说明表</a></p></td>
<td><p>高级配置和电源接口 (ACPI) 硬件规范的实现不需要在 SoC 基于平台或 Windows Server 是基于 BIOS 的系统上，但许多 ACPI 软件规范是 （或可以） 所需。 ACPI 定义泛型、 可扩展的表传递机制，以及用于描述对操作系统的平台特定的表。</p></td>
</tr>
<tr class="odd">
<td><p><a href="device-management-namespace-objects.md" data-raw-source="[Device management namespace objects](device-management-namespace-objects.md)">设备管理命名空间对象</a></p></td>
<td><p><a href="https://www.uefi.org/specifications" data-raw-source="[ACPI 5.0 specification](https://www.uefi.org/specifications)">ACPI 5.0 规范</a>定义多种类型的命名空间可用于管理设备的对象。 例如，设备标识对象包含设备的连接到总线，例如 I2C，不支持子设备的硬件枚举的标识的信息。 其他类型的命名空间对象可以指定系统资源、 描述设备的依赖关系，并指示哪些设备可以被禁用。</p></td>
</tr>
<tr class="even">
<td><p><a href="general-purpose-i-o--gpio-.md" data-raw-source="[General-purpose I/O (GPIO)](general-purpose-i-o--gpio-.md)">通用 I/O (GPIO)</a></p></td>
<td><p>SoC 集成电路地广泛使用的通用 I/O (GPIO) 插针。 对于基于 SoC 的平台，Windows 定义 GPIO 硬件常规抽象和这种抽象形式需要高级配置和电源接口 (ACPI) 命名空间的支持。</p></td>
</tr>
<tr class="odd">
<td><p><a href="simple-peripheral-bus--spb-.md" data-raw-source="[Simple peripheral bus (SPB)](simple-peripheral-bus--spb-.md)">简单外设总线 (SPB)</a></p></td>
<td><p>SoC 集成电路充分利用简单，低-pin-计数和低功耗序列互连设备连接到外围设备平台。 I²C、 SPI 和 UARTs 是示例。 对于基于 SoC 的平台，Windows 提供了常规的简单外围总线 （存储） 硬件抽象和这种抽象形式需要高级配置和电源接口 (ACPI) 命名空间的新支持。</p></td>
</tr>
<tr class="even">
<td><p><a href="device-power-management.md" data-raw-source="[Device power management](device-power-management.md)">设备电源管理</a></p></td>
<td><p><a href="https://www.uefi.org/specifications" data-raw-source="[ACPI 5.0 specification](https://www.uefi.org/specifications)">ACPI 5.0 规范</a>定义一组命名空间对象来指定设备的设备电源信息。 例如，一组对象可以指定设备需要每个受支持的设备电源状态下的能源。 另一种对象类型可以描述从低功耗状态对硬件事件的响应唤醒设备的能力。</p></td>
</tr>
<tr class="odd">
<td><p><a href="acpi-defined-devices.md" data-raw-source="[ACPI-defined devices](acpi-defined-devices.md)">ACPI 定义的设备</a></p></td>
<td><p><a href="https://www.uefi.org/specifications" data-raw-source="[ACPI 5.0 specification](https://www.uefi.org/specifications)">ACPI 5.0 规范</a>定义多个设备类型来代表和控制典型平台功能。 例如，ACPI 定义电源按钮、 睡眠按钮和系统指标。 对于基于 SoC 的平台，Windows 提供了内置驱动程序以支持在本文中所述的 ACPI 定义设备。</p></td>
</tr>
<tr class="even">
<td><p><a href="other-acpi-namespace-objects.md" data-raw-source="[Other ACPI namespace objects](other-acpi-namespace-objects.md)">ACPI 命名空间的其他对象</a></p></td>
<td><p>对于设备的某些特定的类，有其他高级配置和电源接口 (ACPI) 命名空间对象下方的命名空间中的这些设备出现的要求。 本部分列出了用于基于 SoC 的平台所需的其他对象。</p></td>
</tr>
<tr class="odd">
<td><p><a href="acpi-device-specific-methods.md" data-raw-source="[ACPI device-specific methods](acpi-device-specific-methods.md)">ACPI 特定于设备的方法</a></p></td>
<td><p>若要支持更多的功能和扩展来选择技术堆栈，Windows 设备定义特定于设备的方法 (_DSM)。</p></td>
</tr>
</tbody>
</table>

 

 

 




