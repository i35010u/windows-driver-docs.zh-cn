---
title: 将平台扩展与操作系统版本相结合
description: 将平台扩展与操作系统版本相结合
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: be1edc990d1e0f0595dfa413281c348322bfaeba
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96782989"
---
# <a name="combining-platform-extensions-with-operating-system-versions"></a>将平台扩展与操作系统版本相结合


在 INF 文件的 " [**Inf 制造商" 部分**](inf-manufacturer-section.md) ，你可以提供特定于 Windows 操作系统的各种版本的 [**inf *型号* 部分**](inf-models-section.md) 。 这些特定于版本的 *模型* 部分使用 *TargetOSVersion* 修饰进行标识。

在同一个 INF 文件中，可以为不同版本的操作系统指定不同的 [**Inf *模式* 部分**](inf-models-section.md) 。 指定的版本指示将使用 INF *模型* 部分的目标操作系统版本。 如果未指定任何版本，Windows 将在所有操作系统的所有版本中都使用 *模型* 部分，而不使用 *TargetOSVersion* 修饰。

### <a name="targetosversion-decoration-format"></a>*TargetOSVersion* 效果格式

下面的示例演示 Windows XP 通过 Windows 10 版本1511的 *TargetOSVersion* 修饰的正确格式：

**nt** \[*体系结构* \] \[**.**\[*OSMajorVersion* \] OSMajorVersion \[**.**\[*OSMinorVersion* \] OSMinorVersion \[**.**\[*ProductType* \] ProductType \[**.**\[*SuiteMask*\]\]\]\]\]

从 Windows 10 版本1607开始，版本 (版本14310和更高版本) ， *TargetOSVersion* 修饰的正确格式包括 *BuildNumber*：

**nt** \[*体系结构* \] \[**.**\[*OSMajorVersion* \] OSMajorVersion \[**.**\[*OSMinorVersion* \] OSMinorVersion \[**.**\[*ProductType* \] ProductType \[**.**\[*SuiteMask* \] \] SuiteMask \[**.**\[*BuildNumber*\]\]\]\]\]

每个字段的定义如下：

<a href="" id="nt"></a>**nt**  
指定目标操作系统基于 NT。 Windows 2000 和更高版本的 Windows 都是基于 NT 的。

<a href="" id="architecture"></a>*种*  
标识硬件平台。 如果已指定，则必须是 **x86**、 **ia64** 或 **amd64**。 如果未指定，则关联的 INF *模式* 部分可用于任何硬件平台。

<a href="" id="osmajorversion"></a>*OSMajorVersion*  
一个数字，表示操作系统的主版本号。 下表定义了 Windows 操作系统的主版本。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Windows 版本</th>
<th align="left">主版本</th>
</tr>
</thead>
<tbody>
<tr class="even">
<td align="left"><p>Windows 10</p></td>
<td align="left"><p>10</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Windows Server 2012 R2</p></td>
<td align="left"><p>6</p></td>
</tr>
<tr class="even">
<td align="left"><p>Windows 8.1</p></td>
<td align="left"><p>6</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Windows Server 2012</p></td>
<td align="left"><p>6</p></td>
</tr>
<tr class="even">
<td align="left"><p>Windows 8</p></td>
<td align="left"><p>6</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Windows Server 2008 R2</p></td>
<td align="left"><p>6</p></td>
</tr>
<tr class="even">
<td align="left"><p>Windows 7</p></td>
<td align="left"><p>6</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Windows Server 2008</p></td>
<td align="left"><p>6</p></td>
</tr>
<tr class="even">
<td align="left"><p>Windows Vista</p></td>
<td align="left"><p>6</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Windows Server 2003</p></td>
<td align="left"><p>5</p></td>
</tr>
<tr class="even">
<td align="left"><p>Windows XP</p></td>
<td align="left"><p>5</p></td>
</tr>
</tbody>
</table>

 

<a href="" id="osminorversion"></a>*OSMinorVersion*  
一个数字，表示操作系统的次版本号。 下表定义了 Windows 操作系统的次版本。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Windows 版本</th>
<th align="left">次要版本</th>
</tr>
</thead>
<tbody>
<tr class="even">
<td align="left"><p>Windows 10</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Windows Server 2012 R2</p></td>
<td align="left"><p>3</p></td>
</tr>
<tr class="even">
<td align="left"><p>Windows 8.1</p></td>
<td align="left"><p>3</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Windows Server 2012</p></td>
<td align="left"><p>2</p></td>
</tr>
<tr class="even">
<td align="left"><p>Windows 8</p></td>
<td align="left"><p>2</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Windows Server 2008 R2</p></td>
<td align="left"><p>1</p></td>
</tr>
<tr class="even">
<td align="left"><p>Windows 7</p></td>
<td align="left"><p>1</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Windows Server 2008</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="even">
<td align="left"><p>Windows Vista</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Windows Server 2003</p></td>
<td align="left"><p>2</p></td>
</tr>
<tr class="even">
<td align="left"><p>Windows XP</p></td>
<td align="left"><p>1</p></td>
</tr>
</tbody>
</table>

 

<a href="" id="producttype"></a>*ProductType*

一个数字，表示 *winnt.sif* 中定义的 *一个* VER_NT_ *xxxx* 标志，如下所示：

**0x0000001** (VER_NT_WORKSTATION) 

**0x0000002** (VER_NT_DOMAIN_CONTROLLER) 

**0x0000003** (VER_NT_SERVER) 

如果指定了产品类型，则仅当操作系统与指定的产品类型匹配时，才会使用 INF 文件。 如果 INF 文件支持多个产品类型用于单个操作系统版本，则需要多个 *TargetOSVersion* 条目。

*SuiteMask*

一个数字，表示 *winnt.sif* 中定义的一个或多个 VER_SUITE_ *xxxx* 标志 *的组合*。 这些标志包括：

**0x00000001** (VER_SUITE_SMALLBUSINESS)   
**0x00000002** (VER_SUITE_ENTERPRISE)   
**0x00000004** (VER_SUITE_BACKOFFICE)   
**0x00000008** (VER_SUITE_COMMUNICATIONS)   
**0x00000010** (VER_SUITE_TERMINAL)   
**0x00000020** (VER_SUITE_SMALLBUSINESS_RESTRICTED)   
**0x00000040** (VER_SUITE_EMBEDDEDNT)   
**0x00000080** (VER_SUITE_DATACENTER)   
**0x00000100** (VER_SUITE_SINGLEUSERTS)   
**0x00000200** (VER_SUITE_PERSONAL)   
**0x00000400** (VER_SUITE_SERVERAPPLIANCE)   

如果指定了一个或多个套件掩码值，则仅当操作系统与所有指定的产品套件匹配时，才会使用 INF 文件。 如果 INF 文件支持单个操作系统版本的多个产品套件组合，则需要多个 *TargetOSVersion* 条目。

*BuildNumber*

指定该部分适用的 Windows 10 版本的最低操作系统内部版本号，从版本14310或更高版本开始。

内部版本号假定为相对于某些特定操作系统主要/次要版本，并且可能会在将来的某个操作系统主要/次要版本中重置。

仅当 *TargetOSVersion* 的操作系统主要/次要版本与当前 os (或 AltPlatformInfo) 版本完全匹配时，才计算由 *TargetOSVersion* 修饰指定的任何生成号。  如果当前操作系统版本高于 *TargetOSVersion* 修饰指定的 os 版本 (OSMajorVersion，OSMinorVersion) ，无论指定的内部版本号如何，都将此部分视为适用。 同样，如果当前操作系统版本低于 TargetOSVersion 修饰指定的操作系统版本，则该部分不适用。

如果提供了生成号，则 *TargetOSVersion* 修饰的 os 版本和 BuildNumber 必须都大于 Windows 10 build 14310 的操作系统版本和生成号，这一修饰首次引入。  不带这些更改的早期版本的操作系统 (例如，Windows 10 build 10240) 将不会分析未知的修饰，因此，对这些较早版本的尝试将实际上会阻止该操作系统考虑修饰有效。

### <a name="how-windows-processes-targetosversion-decorations"></a><a href="" id="how-setup-processes-targetosversion-decorations"></a>Windows 如何处理 *TargetOSVersion* 装饰

当你在主机操作系统上安装设备或驱动程序时，Windows 将按照以下步骤处理 INF 文件中的 [**Inf *模型* 部分**](inf-models-section.md) ：

1.  如果一个或多个 [**Inf *模型* 部分**](inf-models-section.md) 具有 *TargetOS* 修饰，则 Windows 将选择与主机操作系统的属性最接近的 "inf *模型* " 部分。

    例如，如果 INF *模型* 部分具有 **Ntx 86.5.1** 的 *TargetOS* 修饰，Windows 将在基于 X86 的系统上运行 windows XP 或更高版本的 windows 时选择该部分。

    同样，如果 [**INF *模型* 部分**](inf-models-section.md) 具有 *TargetOS* 的 **nt**，则 windows 将在任何受支持的硬件平台上的主机操作系统是 windows Vista 或更高版本的 windows 的情况下选择该部分。

    如果 INF *模型* 部分的 *TargetOS* **效果为 .。。14393**，如果主机操作系统在任何受支持的硬件平台上运行的 Windows 10 版本等于或大于14393，则 Windows 将选择此部分。

2.  如果任何 [**INF *模型* 部分**](inf-models-section.md) 都没有与主机操作系统匹配的 *TargetOS* 装饰，Windows 将选择具有匹配平台扩展或没有平台扩展的 *模型* 部分。

    例如，如果 INF *模型* 部分的平台扩展为 **ntx86**，windows 将在基于 x86 的系统上的主机操作系统是 Microsoft windows 2000 或更高版本的 windows 的情况下选择该部分。

    同样，如果 [**INF *型号* 部分**](inf-models-section.md) 没有平台扩展，windows 将在任何受支持的硬件平台上的主机操作系统为 windows 2000 或更高版本的 windows 的情况下选择该部分。

3.  如果 Windows 找不到匹配的 [**Inf *型号* 部分**](inf-models-section.md)，则不会使用 inf 文件来安装设备或驱动程序。

### <a name="sample-inf-models-sections-withtargetosversion-decorations"></a>带有 *TargetOSVersion* 装饰的示例 INF *模型* 部分

以下主题提供有关如何在 [**INF *模型* 部分**](inf-models-section.md)中装饰目标操作系统的平台扩展的示例：

[一个或多个目标操作系统的示例 INF *模型* 部分](sample-inf-models-sections-for-one-or-more-target-operating-system.md)

[仅一个目标操作系统的示例 INF *模型* 部分](sample-inf-models-sections-for-only-one-target-operating-system.md)

[适合在多个 Windows 版本上进行设备安装的示例 INF 文件](sample-inf-file-for-device-installation-on-multiple-versions-of-windows.md)

 

 





