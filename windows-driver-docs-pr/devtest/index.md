---
title: 驱动程序开发工具
description: 驱动程序开发工具
ms.assetid: 1d384d73-d1d2-445f-8077-40eed1f99a8c
keywords:
  - 工具 WDK
  - 驱动程序开发工具 WDK
  - WsdCodeGen 工具 WDK
  - '工具 WDK, 开发驱动程序'
  - '设备的 Web 服务 WDK WIA, 工具'
ms.date: 06/28/2018
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
---

# <a name="driver-development-tools"></a>驱动程序开发工具


## <span id="ddk_driver_development_tools_tools"></span><span id="DDK_DRIVER_DEVELOPMENT_TOOLS_TOOLS"></span>


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>用途</strong></p>
<p>Windows 驱动程序工具包 (WDK) 提供了一套可用于开发、分析、生成、安装和测试驱动程序的工具。 WDK 包括功能强大的验证工具，用于检测、分析和纠正开发期间驱动程序代码中的错误。 其中的许多工具可以早早地用于开发过程，这个时候它们最重要，可以为你节省最多的时间和精力。</p>
<p><strong>概述</strong></p>
<p>Windows 驱动程序工具包 (WDK)与 Microsoft Visual Studio 2015 完全集成。 WDK 使用的编译器和生成工具与你用于生成 Visual Studio 项目的工具相同。 现在可以轻松地配置代码分析和验证工具并将其从 Visual Studio 开发环境启动，以便在开发周期的早期找到并修复驱动程序源代码中的问题。</p>
<p>WDK 提供了高级的驱动程序测试框架和一组设备基本功能测试，用于在远程测试系统上自动生成、部署和测试驱动程序。 WDK 提供的工具可以使测试和调试驱动程序的过程较之以前更加方便且更有效。</p>
<p><strong>驱动程序开发工具文档</strong></p>
<p>本部分介绍的工具和方法可以在开发过程中为你提供帮助：</p>
<p><a href="tools-for-inf-files.md" data-raw-source="[Tools for INF Files](tools-for-inf-files.md)">用于处理 INF 文件的工具</a></p>
<p><a href="boot-options-for-driver-testing-and-debugging.md" data-raw-source="[Tools for Changing Boot Options for Driver Testing and Debugging](boot-options-for-driver-testing-and-debugging.md)">用于更改驱动程序测试和调试启动选项的工具</a></p>
<p><a href="tools-for-testing-drivers.md" data-raw-source="[Tools for Testing Drivers](tools-for-testing-drivers.md)">用于测试驱动程序的工具</a></p>
<p><a href="tools-for-verifying-drivers.md" data-raw-source="[Tools for Verifying Drivers](tools-for-verifying-drivers.md)">用于验证驱动程序的工具</a></p>
<p><a href="tools-for-software-tracing.md" data-raw-source="[Tools for Software Tracing](tools-for-software-tracing.md)">用于软件跟踪的工具</a></p>
<p><a href="additional-driver-tools.md" data-raw-source="[Additional Driver Tools](additional-driver-tools.md)">其他驱动程序工具</a></p>
<td align="left"><p><strong>资源</strong></p>
<p><a href="https://msdn.microsoft.com/windows-drivers/develop/getting_started_with_universal_drivers" data-raw-source="[Getting Started with Universal Windows Drivers](https://msdn.microsoft.com/windows-drivers/develop/getting_started_with_universal_drivers)">通用 Windows 驱动程序入门</a></p>
<p>通用 Windows 驱动程序使开发人员能够创建可在多种不同设备类型（从嵌入式系统到平板电脑和台式电脑）上运行的单个驱动程序。 硬件开发人员可以在不同的外形规格中使用其现有的组件和设备驱动程序。</p>
<p><a href="https://msdn.microsoft.com/windows-drivers/develop/converting_wdk_8_1_projects_to_wdk_10" data-raw-source="[Converting WDK 8.1 Projects to WDK 10](https://msdn.microsoft.com/windows-drivers/develop/converting_wdk_8_1_projects_to_wdk_10)">将 WDK 8.1 项目转换为 WDK 10</a></p>
<p>可以将使用 WDK 8 或 Windows 驱动程序工具包 (WDK) 8.1 创建的项目和解决方案转换为与 Windows 驱动程序工具包 (WDK) 10 和 Visual Studio 2015 结合使用。 在打开项目或解决方案之前，请运行 ProjectUpgradeTool。 ProjectUpgradeTool 可以转换项目和解决方案，以便使用 Windows 10 版 WDK 进行生成。</p>
<p></p>
<p><a href="https://msdn.microsoft.com/windows-drivers/develop/validating_universal_drivers" data-raw-source="[Validating Universal Windows drivers](https://msdn.microsoft.com/windows-drivers/develop/validating_universal_drivers)">验证通用 Windows 驱动程序</a></p>
<p>可以使用 ApiValidator.exe 工具验证驱动程序调用的 API 是否对通用 Windows 驱动程序有效。 如果驱动程序调用的 API 不是有效的通用 Windows 驱动程序 API，该工具将返回错误。 此工具是 Windows 10 版 WDK 的一部分。</p>
<a href="wdk-and-visual-studio-build-environment.md" data-raw-source="[WDK and Visual Studio build environment](wdk-and-visual-studio-build-environment.md)">WDK 和 Visual Studio 生成环境</a>
<p>有关如何使用 WDK 和 Visual Studio 生成环境的详细信息和提示（针对驱动程序开发人员）。</p>
<a href="https://msdn.microsoft.com/windows-drivers/develop/visual_studio_driver_development_environment" data-raw-source="[Developing, Testing, and Deploying Drivers](https://msdn.microsoft.com/windows-drivers/develop/visual_studio_driver_development_environment)">开发、测试以及部署驱动程序</a>
<p>有关如何在 Visual Studio 开发环境中生成驱动程序并使用验证工具和测试的具体信息。</p></td>
</tr>
</tbody>
</table>

 

 

 





