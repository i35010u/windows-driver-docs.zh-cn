---
title: 针对 ACPI 5.0 的 Windows 支持概述
description: ACPI 5.0 规范支持在 Windows 8 及更高版本中运行的基于 SoC 的移动平台，但继续支持在早期版本的 Windows 中引入的许多有用功能。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b5fd58952f3ea18b986ad0bf127986d14a48e6d2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96783601"
---
# <a name="overview-of-windows-support-for-acpi-50"></a>针对 ACPI 5.0 的 Windows 支持概述


[ACPI 5.0 规范](https://uefi.org/specifications)支持运行 windows 8 及更高版本的基于 SoC 的移动平台，支持和支持 windows Server 2016 及更高版本，但继续支持在早期版本的 windows 中引入的许多有用功能。 此设计指南将实施者指引到 ACPI 5.0 的各个部分，这些组件专门适用于基于 SoC 的平台以及为 Windows Server 2016 设计的系统，并介绍了在 ACPI 中实现特定于 SoC 的功能以在这些平台上运行 Windows 的最佳实践。

## <a name="scope"></a>范围


本设计指南的目标受众是固件开发人员和系统设计人员，他们需要提供固件支持和实现指南。 观察和遵循这些准则有助于确保 SoC 平台和 Windows Server 2016 系统上的 Windows 功能正常。

此设计指南专门针对支持低功率 S0 空闲的硬件精简 ACPI 平台。 但是，大多数指南也适用于符合 ACPI 5.0 且运行 Windows 8 或更高版本或 Windows Server 2012 或更高版本的平台。 此外，本主题假定 clamshell 外形规格或无线、多点触控移动平台。 因此，它将自身局限于预计在此类平台上广泛使用的技术。 对于本文档中未涵盖的技术，读者会将 ACPI 规范本身称为 "实现信息"。

## <a name="firmware-revision-support"></a>固件版本支持


Windows 支持基于 [ACPI 5.0 规范](https://uefi.org/specifications)的固件修订版本。

**注意**  Windows 支持在 ACPI 5.0 规范中定义的一小部分功能。 对于更高版本的固件，Windows 没有显式检查。 如果此固件包含必要的支持，则 Windows 将支持符合 ACPI 规范的更高版本的固件，如本设计指南中所述。

 

## <a name="in-this-section"></a>在本节中


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
<td><p><a href="summary-of-acpi-support-in-windows.md" data-raw-source="[Summary of ACPI support in Windows](summary-of-acpi-support-in-windows.md)">Windows 中的 ACPI 支持摘要</a></p></td>
<td><p>本主题概述了支持基于 SoC 的平台上的 Windows 所需的高级配置和电源接口 (ACPI) 5.0 功能的子集。</p></td>
</tr>
<tr class="even">
<td><p><a href="hardware-requirements-for-soc-based-platforms.md" data-raw-source="[Hardware requirements for SoC-based platforms](hardware-requirements-for-soc-based-platforms.md)">基于 SoC 的平台的硬件要求</a></p></td>
<td><p><a href="https://uefi.org/specifications" data-raw-source="[ACPI 5.0 specification](https://uefi.org/specifications)">ACPI 5.0 规范</a>引入了一组新的硬件要求，以支持运行 Windows 的基于 SoC 的平台。 ACPI 5.0 支持硬件降低的系统设计以降低成本，并支持连接待机电源型号，以延长电池寿命。</p></td>
</tr>
<tr class="odd">
<td><p><a href="acpi-namespace-hierarchy.md" data-raw-source="[ACPI namespace hierarchy](acpi-namespace-hierarchy.md)">ACPI 命名空间层次结构</a></p></td>
<td><p>ACPI 命名空间层次结构必须准确地对平台的硬件拓扑进行建模，从处理器的系统总线开始 ( "_SB" ) 。 通常，连接到总线或控制器的设备在命名空间中显示为该总线或控制器设备的子。</p></td>
</tr>
<tr class="even">
<td><p><a href="microsoft-asl-compiler.md" data-raw-source="[Microsoft ASL compiler](microsoft-asl-compiler.md)">Microsoft ASL 编译器</a></p></td>
<td><p>Microsoft ACPI 源语言 (版本 5.0 ASL) 编译器支持高级配置和电源接口规范中的功能，修订 5.0 (<a href="https://uefi.org/specifications" data-raw-source="[ACPI 5.0 specification](https://uefi.org/specifications)">ACPI 5.0 规范</a>) 。 ASL 编译器随 Windows 驱动程序工具包一起分发 (WDK) 8.1。</p></td>
</tr>
</tbody>
</table>

 

 

 




