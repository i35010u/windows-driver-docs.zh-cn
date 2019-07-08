---
title: 将平台扩展与操作系统版本相结合
description: 将平台扩展与操作系统版本相结合
ms.assetid: ef3b7138-b68a-4dba-b011-fcb93e3072a3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 827d79100eae252ec08dca93ac455f8dc1371fd7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63357027"
---
# <a name="combining-platform-extensions-with-operating-system-versions"></a>将平台扩展与操作系统版本相结合


内[ **INF 制造商部分**](inf-manufacturer-section.md) INF 文件，你可以提供[ **INF*模型*部分**](inf-models-section.md)特定于各种版本的 Windows 操作系统。 这些特定于版本的*模型*各节标识使用*TargetOSVersion*修饰。

在同一个 INF 文件中，不同[ **INF*模型*各节**](inf-models-section.md)可以指定针对不同版本的操作系统。 指定的版本指示用于目标操作系统版本 INF*模型*将使用部分。 如果未不指定任何版本，Windows 将使用*模型*而无需部分*TargetOSVersion*修饰的所有操作系统的所有版本。

### <a name="targetosversion-decoration-format"></a>*TargetOSVersion*修饰格式

下面的示例显示了正确的格式*TargetOSVersion*适用于 Windows XP 到 Windows 10，版本 1511年的修饰：

**nt**\[*体系结构*\]\[ **。** \[ *OSMajorVersion*\]\[ **。** \[ *OSMinorVersion*\]\[ **。** \[ *ProductType*\]\[ **。** \[ *SuiteMask*\]\]\]\]\]

从 Windows 10，版本 1607 （内部 14310 及更高版本） 的正确格式的开始*TargetOSVersion*修饰包括*BuildNumber*:

**nt**\[*体系结构*\]\[ **。** \[ *OSMajorVersion*\]\[ **。** \[ *OSMinorVersion*\]\[ **。** \[ *ProductType*\]\[ **。** \[ *SuiteMask*\]\]\[ **。** \[ *BuildNumber*\]\]\]\]\]

每个字段定义，如下所示：

<a href="" id="nt"></a>**nt**  
指定目标操作系统是基于 NT 的。 Windows 2000 和更高版本的 Windows 是所有基于 NT 的。

<a href="" id="architecture"></a>*体系结构*  
标识的硬件平台。 如果指定，这必须是**x86**， **ia64**，或**amd64**。 如果未指定关联的 INF*模型*部分可与任何硬件平台。

<a href="" id="osmajorversion"></a>*OSMajorVersion*  
一个数字表示操作系统的主版本号。 下表定义的 Windows 操作系统的主版本。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Windows 版本</th>
<th align="left">主要版本</th>
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
一个数字表示操作系统的次版本号。 下表定义的 Windows 操作系统的次版本。

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

一个数字，表示*一个*的 VER_NT_*xxxx*中定义的标志*Winnt.h*，如下所示：

**0x0000001** (VER_NT_WORKSTATION)

**0x0000002** (VER_NT_DOMAIN_CONTROLLER)

**0x0000003** (VER_NT_SERVER)

如果指定的产品类型，则仅当操作系统与指定的产品类型匹配，将使用 INF 文件。 如果 INF 文件有关的一个操作系统版本，支持多个产品类型多个*TargetOSVersion*为必需项。

*SuiteMask*

一个数字，表示*的组合*一个或多个 VER_SUITE_*xxxx*中定义的标志*Winnt.h*。 这些标记包括：

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

如果指定了一个或多个套件掩码值，仅当操作系统匹配所有指定的产品套件，将使用 INF 文件。 如果 INF 文件有关的一个操作系统版本，支持多个产品套件组合多个*TargetOSVersion*为必需项。

*BuildNumber*

指定的最低 OS 内部版本号部分应用于，从生成 14310 或更高版本的 Windows 10 版本。

生成号被假定为相对于某些特定的操作系统主要/次要版本，并可能会重置为某一将来 OS 主要/次要版本。

任何生成指定的数字*TargetOSVersion*仅当操作系统主要/次要版本的计算修饰*TargetOSVersion*完全匹配的当前 OS （或 AltPlatformInfo） 版本。  如果当前 OS 版本高于指定的 OS 版本*TargetOSVersion*修饰 （OSMajorVersion，OSMinorVersion） 部分被视为适用而不考虑指定的生成号。 同样，如果当前 OS 版本低于指定 TargetOSVersion 修饰的 OS 版本，部分不适用。

如果提供的内部版本号，则操作系统版本和的 BuildNumber *TargetOSVersion*修饰必须同时大于 OS 版本和 Windows 10 生成 14310 首次引入此修饰的生成号。  早期版本的操作系统 (例如，Windows 10 生成 10240) 这些更改不会将分析未知的修饰，因此尝试这些前面生成的目标实际上将阻止该 OS 考虑修饰根本有效。

### <a href="" id="how-setup-processes-targetosversion-decorations"></a>Windows 如何处理*TargetOSVersion*修饰

Windows 时在主机操作系统上安装的设备或驱动程序，请按照下列步骤来处理[ **INF*模型*各节**](inf-models-section.md) INF 文件中：

1.  如果一个或多个[ **INF*模型*各节**](inf-models-section.md)具有*目标 Os*修饰，Windows 选择 INF*模型*主机操作系统的特性与最接近的部分。

    例如，如果 INF*模型*部分有*目标 Os*修饰**ntx86.5.1**，Windows 将选择该部分，如果主机操作系统正在运行 Windows XP 或在基于 x86 的系统上的 Windows 的更高版本。

    同样，如果[ **INF*模型*部分**](inf-models-section.md)具有*目标 Os*修饰**nt.6.0**，Windows如果主机操作系统是 Windows Vista 或更高版本 Windows 的任何受支持的硬件平台上，请选择该部分。

    如果 INF*模型*部分有*目标 Os*修饰的**nt.10.0...14393**，Windows 将选择该部分，如果主机操作系统的 Windows 10 版本等于或大于 14393 上运行任何受支持的硬件平台。

2.  如果没有[ **INF*模型*各节**](inf-models-section.md)具有*目标 Os* Windows 选择与主机操作系统匹配的修饰，*模型*节，其中包含匹配的平台扩展或任何平台扩展。

    例如，如果 INF*模型*部分包含的平台扩展**ntx86**，如果主机操作系统为 Microsoft Windows 2000 或更高版本的 Windows 上基于 x86 的 Windows 中选择该部分系统。

    同样，如果[ **INF*模型*各节**](inf-models-section.md)没有平台扩展，如果主机操作系统是 Windows 2000 或更高版本的部分 Windows 选择在任何支持的硬件平台上的 Windows。

3.  如果 Windows 找不到匹配[ **INF*模型*部分**](inf-models-section.md)，它不会使用 INF 文件来安装该设备或驱动程序。

### <a name="sample-inf-models-sections-withtargetosversion-decorations"></a>示例 INF*模型*与部分*TargetOSVersion*修饰

以下主题提供如何修饰内的目标操作系统的平台扩展的示例[ **INF*模型*部分**](inf-models-section.md):

[示例 INF*模型*部分的一个或多针对操作系统](sample-inf-models-sections-for-one-or-more-target-operating-system.md)

[示例 INF*模型*部分，只有一个用于目标操作系统](sample-inf-models-sections-for-only-one-target-operating-system.md)

[示例 INF 文件用于在多个版本的 Windows 上的设备安装](sample-inf-file-for-device-installation-on-multiple-versions-of-windows.md)

 

 





