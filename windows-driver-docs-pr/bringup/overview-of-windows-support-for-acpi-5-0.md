---
title: 针对 ACPI 5.0 的 Windows 支持概述
description: ACPI 5.0 规范支持基于 SoC 的移动平台的运行 Windows 8 和更高版本，但继续支持早期版本 Windows 中引入了许多有用的功能。
ms.assetid: BAFBA051-FEDA-469B-9B67-C74D252C84F9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: daf042596bfd3ec168f9263f8c92b17cd1646f22
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353976"
---
# <a name="overview-of-windows-support-for-acpi-50"></a>针对 ACPI 5.0 的 Windows 支持概述


[ACPI 5.0 规范](https://uefi.org/specifications)启用支持的基于 SoC 的移动平台的运行 Windows 8 和更高版本，并启用和支持的 Windows Server 2016 及更高版本，但仍支持许多有用的功能中引入的Windows 的早期版本。 此设计指南将定向到专门适用于 SoC 基于平台以及与面向 Windows Server 2016 的系统的组成部分 ACPI 5.0 的实施者，并且介绍了在 ACPI 上运行 Windows 中实现特定于 SoC 的功能的最佳做法这些平台。

## <a name="scope"></a>范围


此设计指南的目标受众是固件开发人员和系统设计人员需要的固件支持和实现指南。 观察并遵守这些指导原则将有助于确保适当的 Windows 在 SoC 平台和 Windows Server 2016 的系统上的功能。

此设计指南专门针对硬件减少 ACPI 支持的平台低能耗空闲状态的 S0。 但是，大部分指南也适用于符合 ACPI 5.0 和运行 Windows 8 或更高版本，任何平台或 Windows Server 2012 或更高版本。 此外，本主题假定蛤外形规格或无线、 多-点触控的移动平台。 因此限制本身为希望在此类平台上广泛使用的技术。 有关本文档中未涉及的技术，读取器即为 ACPI 规范本身的实施信息。

## <a name="firmware-revision-support"></a>固件修订版本支持


Windows 支持基于固件修订[ACPI 5.0 规范](https://uefi.org/specifications)。

**请注意**  Windows 支持 ACPI 5.0 规范中定义的功能的子集。 Windows 不具有显式签入被更高版本的固件修订。 Windows 将支持符合 ACPI 规范的更高版本的修订此固件包含必要的支持，如果此设计指南中所述的固件。

 

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
<td><p><a href="summary-of-acpi-support-in-windows.md" data-raw-source="[Summary of ACPI support in Windows](summary-of-acpi-support-in-windows.md)">在 Windows 中的 ACPI 支持的摘要</a></p></td>
<td><p>本主题总结了高级配置和电源接口 (ACPI) 5.0 基于 SoC 的平台上支持 Windows 所需的功能的子集。</p></td>
</tr>
<tr class="even">
<td><p><a href="hardware-requirements-for-soc-based-platforms.md" data-raw-source="[Hardware requirements for SoC-based platforms](hardware-requirements-for-soc-based-platforms.md)">SoC 基于平台的硬件要求</a></p></td>
<td><p><a href="https://uefi.org/specifications" data-raw-source="[ACPI 5.0 specification](https://uefi.org/specifications)">ACPI 5.0 规范</a>引入了一组新的硬件要求，以支持运行 Windows 的基于 SoC 的平台。 ACPI 5.0 支持硬件减少系统设计，以降低成本，并支持连接待机电源模型以启用长的电池使用寿命。</p></td>
</tr>
<tr class="odd">
<td><p><a href="acpi-namespace-hierarchy.md" data-raw-source="[ACPI namespace hierarchy](acpi-namespace-hierarchy.md)">ACPI 命名空间层次结构</a></p></td>
<td><p>ACPI 命名空间层次结构必须准确地建模平台的硬件拓扑，从处理器的系统总线 ("_SB")。 一般情况下，连接到总线或控制器的设备显示为该总线或控制器设备命名空间中的子项。</p></td>
</tr>
<tr class="even">
<td><p><a href="microsoft-asl-compiler.md" data-raw-source="[Microsoft ASL compiler](microsoft-asl-compiler.md)">Microsoft ASL 编译器</a></p></td>
<td><p>5\.0 版本的 Microsoft ACPI 源语言 (ASL) 编译器支持高级配置和电源接口规范，修订版本 5.0 中的功能 (<a href="https://uefi.org/specifications" data-raw-source="[ACPI 5.0 specification](https://uefi.org/specifications)">ACPI 5.0 规范</a>)。 使用 Windows Driver Kit (WDK) 8.1 分发 ASL 编译器。</p></td>
</tr>
</tbody>
</table>

 

 

 




