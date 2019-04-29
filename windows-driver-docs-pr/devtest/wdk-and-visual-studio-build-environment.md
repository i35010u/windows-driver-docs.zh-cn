---
title: WDK 和 Visual Studio 生成环境
description: Windows Driver Kit (WDK) 8.1 和 WDK 8 引入了重大更改到的环境，用于生成驱动程序。
ms.assetid: B964CF3F-ACDB-41ED-8962-B7DDB957D7D3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e01ecc15c40dd9d9e6eeca1fd6cbc3f259026cc2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63371533"
---
# <a name="wdk-and-visual-studio-build-environment"></a>WDK 和 Visual Studio 生成环境


Windows Driver Kit (WDK) 8.1 和 WDK 8 引入了重大更改到的环境，用于生成驱动程序。 WDK 不能再使用 Build.exe。 驱动程序 WDK 构建环境使用 MSBuild.exe，并与 Visual Studio 开发环境完全集成。 这意味着，源文件、 makefile.inc、 makefile.new 和其他相关的生成不再使用以前版本的 WDK 中存在的文件。 WDK 现在可以创建、 编辑、 生成、 测试和部署驱动程序通过 Visual Studio。 本文档的目的是提供信息以帮助用户如果熟悉以前 Wdk，WDK 8，WDK 8.1 入门指南中。

**请注意**  必须升级项目和解决方案使用 WDK 8 创建为使用 WDK 8.1 和 Microsoft Visual Studio 2013。 在打开项目或解决方案之前，先运行 [ProjectUpgradeTool](projectupgradetool.md)。 ProjectUpgradeTool 将转换的项目和解决方案，以便它们可以建立使用 WDK 8.1。

 

## <a name="span-idinthissectionspanin-this-section"></a><span id="in_this_section"></span>本部分中的内容


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
<td align="left"><p><a href="msbuild-primer-for-wdk-developers.md" data-raw-source="[MSBuild primer for WDK developers](msbuild-primer-for-wdk-developers.md)">MSBuild WDK 开发人员的入门读物</a></p></td>
<td align="left"><p>本部分介绍到 WDK 开发人员，他们熟悉 Build.exe 和 NMake.exe 的一些基本的 MSBuild 术语。 本部分显示了简单的 MSBuild 项目中的构造。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdk-and-msbuild-overview.md" data-raw-source="[WDK and MSBuild overview](wdk-and-msbuild-overview.md)">WDK 和 MSBuild 概述</a></p></td>
<td align="left"><p>Visual Studio 可以管理多个项目。 本部分介绍 WDK 构建环境。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="platform-toolset.md" data-raw-source="[Platform Toolset](platform-toolset.md)">平台工具集</a></p></td>
<td align="left"><p>Windows Driver Kit (WDK) 利用 MSBuild 平台工具集功能提供的工具和特定于驱动程序开发的库。 MSBuild 平台工具集功能进行扩展。 由 MSBuild 属性名为控制你想要使用的平台工具集的特定版本<strong>PlatformToolset</strong>。 项目可以通过设置工具和库之间切换<strong>PlatformToolset</strong>项目文件中的属性。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="windows-driver-specific-property-files.md" data-raw-source="[Windows driver-specific property files](windows-driver-specific-property-files.md)">Windows 驱动程序特定属性文件</a></p></td>
<td align="left"><p>驱动程序属性页将 MSBuild 用于生成任何驱动程序项目的工具的所有默认设置。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="windows-driver-targets.md" data-raw-source="[Windows driver targets](windows-driver-targets.md)">Windows 驱动程序目标</a></p></td>
<td align="left"><p>WindowsDriver.Common.targets、 WindowsDriver.masm.targets 和 WindowsDriver.arm.targets 文件提供构建一个驱动程序所需的目标。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdk-build-output.md" data-raw-source="[WDK build output](wdk-build-output.md)">WDK 生成输出</a></p></td>
<td align="left"><p>默认情况下使用的中间目录 WDK <strong>$ （intdir)</strong>宏指定默认的生成输出目录。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdk-tasks-for-msbuild.md" data-raw-source="[WDK tasks for MSBuild](wdk-tasks-for-msbuild.md)">WDK MSBuild 任务</a></p></td>
<td align="left"><p>Windows Driver Kit (WDK) 包括在生成过程中通常使用，但通过 Visual Studio 通常不分发的工具。 使用这些工具登录驱动程序或驱动程序包，实现软件跟踪，或者如何处理和编译的资源或消息文件 （stampinf.exe、 mc.exe、 tracewpp.exe、 binplace.exe 等）。 这些命令行工具需要公开为 MSBuild 作为任务 （包含在目标），以便它们可以在生成过程中运行。 WDK 提供了必要的组件，以便在生成您的驱动程序时，可以作为 MSBuild 任务运行这些工具。</p></td>
</tr>
</tbody>
</table>

 

 

 





