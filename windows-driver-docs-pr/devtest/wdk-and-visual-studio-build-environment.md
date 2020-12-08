---
title: WDK 和 Visual Studio 生成环境
description: Windows 驱动程序工具包 (WDK) 8.1 和 WDK 8 导致了用于构建驱动程序的环境发生了重大更改。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ad521f47d2deb921707dc8ad78b7f20797f54584
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823303"
---
# <a name="wdk-and-visual-studio-build-environment"></a>WDK 和 Visual Studio 生成环境


Windows 驱动程序工具包 (WDK) 8.1 和 WDK 8 导致了用于构建驱动程序的环境发生了重大更改。 WDK 不再使用 Build.exe。 用于驱动程序的 WDK 构建环境使用 MSBuild.exe，并与 Visual Studio 开发环境完全集成。 这意味着，将不再使用在前一版本的 WDK 中提供的源文件和其他相关生成文件。 WDK 现在使你能够通过 Visual Studio 创建、编辑、生成、测试和部署驱动程序。 本文档的目的是提供一些信息，以帮助熟悉在 WDK 8.1 和 WDK 8 入门中熟悉以前的 WDKs 的用户。

**注意**  使用 WDK 8 创建的项目和解决方案必须升级，才能与 WDK 8.1 和 Microsoft Visual Studio 2013 一起使用。 在打开项目或解决方案之前，请运行 [ProjectUpgradeTool](projectupgradetool.md)。 ProjectUpgradeTool 转换项目和解决方案，以便可以使用 WDK 8.1 生成它们。

 

## <a name="span-idin_this_sectionspanin-this-section"></a><span id="in_this_section"></span>本部分中的内容


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">主题</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="msbuild-primer-for-wdk-developers.md" data-raw-source="[MSBuild primer for WDK developers](msbuild-primer-for-wdk-developers.md)">面向 WDK 开发人员的 MSBuild 入门教程</a></p></td>
<td align="left"><p>本部分介绍了一些基本的 MSBuild 术语，适用于 WDK 开发人员，熟悉 Build.exe 和 NMake.exe。 本部分展示了简单的 MSBuild 项目的构造。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdk-and-msbuild-overview.md" data-raw-source="[WDK and MSBuild overview](wdk-and-msbuild-overview.md)">WDK 和 MSBuild 概述</a></p></td>
<td align="left"><p>Visual Studio 可以管理多个项目。 本部分介绍了 WDK 生成环境。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="platform-toolset.md" data-raw-source="[Platform Toolset](platform-toolset.md)">平台工具集</a></p></td>
<td align="left"><p>Windows 驱动程序工具包 (WDK) 利用 MSBuild 平台工具集功能提供特定于驱动程序开发的工具和库。 MSBuild 平台工具集功能是可扩展的。 要使用的平台工具集的特定版本由名为 <strong>PlatformToolset</strong>的 MSBuild 属性控制。 项目可通过设置项目文件中的 <strong>PlatformToolset</strong> 属性在工具和库之间切换。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="windows-driver-specific-property-files.md" data-raw-source="[Windows driver-specific property files](windows-driver-specific-property-files.md)">Windows 驱动程序特定的属性文件</a></p></td>
<td align="left"><p>"驱动程序" 属性表具有 MSBuild 用于生成任何驱动程序项目的所有工具的默认设置。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="windows-driver-targets.md" data-raw-source="[Windows driver targets](windows-driver-targets.md)">Windows 驱动程序目标</a></p></td>
<td align="left"><p>WindowsDriver、WindowsDriver 和 WindowsDriver 文件提供了构建驱动程序所必需的目标目标文件，这些文件。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdk-build-output.md" data-raw-source="[WDK build output](wdk-build-output.md)">WDK 生成输出</a></p></td>
<td align="left"><p>默认情况下，WDK 使用中间目录 <strong>$ (IntDir) </strong> 宏来指定默认的生成输出目录。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdk-tasks-for-msbuild.md" data-raw-source="[WDK tasks for MSBuild](wdk-tasks-for-msbuild.md)">MSBuild 的 WDK 任务</a></p></td>
<td align="left"><p>Windows 驱动程序工具包 (WDK) 包含通常在生成过程中使用的工具，但通常不会与 Visual Studio 一起分发。 这些工具用于签署驱动程序或驱动程序包，实现软件跟踪，或者处理和编译资源或消息文件 ( # A0、mc.exe、tracewpp.exe、binplace.exe 等 ) 。 需要将这些命令行工具公开给 MSBuild，作为 (包含在目标) 中的任务，使其可以在生成过程中运行。 WDK 提供必要的组件，以便在构建驱动程序时可以将这些工具作为 MSBuild 任务运行。</p></td>
</tr>
</tbody>
</table>

 

 

 





