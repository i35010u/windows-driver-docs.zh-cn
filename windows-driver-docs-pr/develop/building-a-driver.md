---
ms.assetid: f5676c9c-b582-47d0-9b7c-02b6443103ad
title: 使用 WDK 生成驱动程序
description: 本主题介绍了如何使用 Windows 驱动程序工具包 (WDK) 生成驱动程序。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 977515761197e62145ab4104275ad36ca948e028
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91733427"
---
# <a name="using-visual-studio-or-msbuild-to-build-a-driver"></a>使用 Visual Studio 或 MSBuild 生成驱动程序


本主题介绍了如何使用 Visual Studio 开发环境来生成驱动程序，或使用 Microsoft 生成引擎 ([MSBuild](/visualstudio/msbuild/msbuild)) 通过命令行来生成驱动程序。

**重要提示**  从 Windows 驱动程序工具包 (WDK) 8 开始，MSBuild 取代 Windows 生成实用程序 (Build.exe)。 WDK 现在使用的编译器和生成工具与你用于生成 Visual Studio 项目的工具相同。 使用以前版本的 WDK 生成的驱动程序项目必须转换为在 Visual Studio 环境中工作。 你可以从命令行运行转换实用程序，也可以通过从现有源创建新 Visual Studio 项目来转换现有驱动程序。 有关详细信息，请参阅[从现有源文件创建驱动程序](creating-a-driver-from-existing-source-files.md)和 [WDK 和 Visual Studio 生成环境](../devtest/wdk-and-visual-studio-build-environment.md)。

 

## <a name="span-idbuilding_a_driver_using_visual_studiospanspan-idbuilding_a_driver_using_visual_studiospanbuilding-a-driver-using-visual-studio"></a><span id="building_a_driver_using_visual_studio"></span><span id="BUILDING_A_DRIVER_USING_VISUAL_STUDIO"></span>使用 Visual Studio 生成驱动程序


在 Visual Studio 中生成驱动程序与生成任何项目或解决方案的方法相同。 在使用 Windows 驱动程序模板创建新驱动程序项目时，模板定义默认（有效）的项目配置和默认（有效）的解决方案生成配置。

注意  可以将使用 WDK 8 或 Windows 驱动程序工具包 (WDK) 8.1 创建的项目和解决方案转换为使用 Windows 驱动程序工具包 (WDK) 10 和 Visual Studio 2019。 在打开项目或解决方案之前，请运行 [ProjectUpgradeTool](../devtest/projectupgradetool.md)。 ProjectUpgradeTool 可以转换项目和解决方案，以便使用 WDK 10 进行生成。

 

有关管理和编辑生成配置的信息，请参阅[在 Visual Studio 中生成](/previous-versions/visualstudio/visual-studio-2012/cyz1h6zd(v=vs.110))。

默认的解决方案生成配置为**调试**和 **Win32**。 

**如何选择配置并生成驱动程序**

1.  确保你的计算机上安装了相同版本的 SDK 和 WDK。
2.  在 Visual Studio 中，打开驱动程序项目或解决方案。
3.  在“解决方案资源管理器”中选择并按住（或右键单击）解决方案，然后选择“配置管理器”。
4.  在“配置管理器”中，选择与你感兴趣的生成类型对应的**活动解决方案配置**（例如，**调试**或**发布**）和**活动解决方案平台**（例如，**Win32**）。
5.  选择并按住（或右键单击）Avshws 项目，然后选择“属性”。  导航到“驱动程序设置”>“常规”，设置“目标操作系统版本”和“目标平台”。
6.  配置驱动程序或驱动程序包的项目属性。 你可以为部署、驱动程序签名或其他任务设置属性。 有关详细信息，请参阅[配置驱动程序和驱动程序包的项目属性](#configure_project_props)。
7.  从“生成”菜单中，选择“生成解决方案”(Ctrl+Shift+B)。

## <a name="span-idbuilding_a_driver_using_the_command_line__msbuild_spanspan-idbuilding_a_driver_using_the_command_line__msbuild_spanbuilding-a-driver-using-the-command-line-msbuild"></a><span id="building_a_driver_using_the_command_line__msbuild_"></span><span id="BUILDING_A_DRIVER_USING_THE_COMMAND_LINE__MSBUILD_"></span>使用命令行 (MSBuild) 生成驱动程序


你可以使用 **Visual Studio 命令提示**窗口和 Microsoft 生成引擎 ([MSBuild](/visualstudio/msbuild/msbuild)) 从命令行生成驱动程序

**如何使用“Visual Studio 命令提示”窗口生成驱动程序**

1.  打开“适用于 VS2019 的开发人员命令提示符”窗口。

    在此窗口中，你可以通过指定项目 (.VcxProj) 或解决方案 (.Sln) 文件使用 MSBuild.exe 生成任何 Visual Studio 项目。

2.  导航到项目目录，然后为你的目标输入 **MSbuild** 命令。

    例如，若要使用默认的平台和配置执行名为 MyDriver.vcxproj 的 Visual Studio 驱动程序项目的洁净生成，导航到项目目录并输入以下 MSBuild 命令：

    ```cpp
    msbuild /t:clean /t:build .\MyDriver.vcxproj
    ```

    **语法** - 若要指定特定配置和平台，请使用以下命令语法：

    ```cpp
    msbuild /t:clean /t:build ProjectFile /p:Configuration=<Debug|Release> /p:Platform=architecture /p:TargetPlatformVersion=a.b.c.d /p:TargetVersion=OS    
    ```

    例如，以下命令针对“调试”配置和“Win32”平台为 Windows 10 生成驱动程序。

    ```cpp
    msbuild /t:clean /t:build .\MyDriver.vcxproj /p:Configuration="Debug" /p:Platform=Win32 /p:TargetVersion=”Windows10” /p:TargetPlatformVersion=”10.0.10010.0”
    ```

    **TargetPlatformVersion** 设置是可选的，你可以指定进行生成时要使用的工具包版本。 默认使用最新工具包。

## <a name="span-idconfigure_project_propsspanspan-idconfigure_project_propsspanconfiguring-project-properties-for-your-driver-and-driver-package"></a><span id="configure_project_props"></span><span id="CONFIGURE_PROJECT_PROPS"></span>配置驱动程序和驱动程序包的项目属性


你使用**属性页**配置和设置驱动程序和驱动程序包的选项。 你可以选择配置驱动程序，以便在生成解决方案时令其自动签名或自动部署到远程测试计算机。

WDK 提供了大量的命令行工具，如 [Stampinf](../devtest/stampinf.md) 和 [WPP 预处理器（WPP 跟踪）](../devtest/wpp-preprocessor.md)，通常包含在生成过程内。 这些工具不是通过 Visual Studio 分发的。 为了将这些工具与 Visual Studio 生成环境整合，它们被包装为 [MSBuild 的 WDK 任务](../devtest/wdk-tasks-for-msbuild.md)。 如果你使用驱动程序模板之一或有已转换的现有驱动程序，你的项目可能已经存在这些属性页。 如果不是上述情况，在你将相关文件类型添加到项目或解决方案（例如，消息编译器的 .mc 或 .man 文件）时，属性页将自动添加到你的项目。 有关详细信息，请参阅 [WDK 和 Visual Studio 生成环境](../devtest/wdk-and-visual-studio-build-environment.md)。

你可以为单个驱动程序或整个驱动程序包设置属性。 下表显示了一些可专门为驱动程序和驱动程序包配置的可用属性。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">驱动程序项目属性</th>
<th align="left">驱动程序包属性</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>单个驱动程序文件的签名属性（请参阅<a href="signing-a-driver.md" data-raw-source="[Signing a Driver](signing-a-driver.md)">为驱动程序签名</a>）</p></td>
<td align="left"><p>驱动程序包的签名属性（请参阅<a href="signing-a-driver.md" data-raw-source="[Signing a Driver](signing-a-driver.md)">为驱动程序签名</a>）</p></td>
</tr>
<tr class="even">
<td align="left"><a href="counters-manifest-preprocessor-properties-for-driver-projects.md" data-raw-source="[Counters Manifest Preprocessor Properties for Driver Projects](counters-manifest-preprocessor-properties-for-driver-projects.md)">驱动程序项目的计数器清单预处理器属性</a>（适用于 <a href="/windows/desktop/PerfCtrs/ctrpp" data-raw-source="[CTRPP](/windows/desktop/PerfCtrs/ctrpp)">CTRPP</a>）</td>
<td align="left"><p><a href="deployment-properties-for-driver-projects.md" data-raw-source="[Deployment Properties for Driver Package Projects](deployment-properties-for-driver-projects.md)">驱动程序包项目的部署属性</a>（请参阅<a href="deploying-a-driver-to-a-test-computer.md" data-raw-source="[Deploying a Driver to a Test Computer](deploying-a-driver-to-a-test-computer.md)">将驱动程序部署到测试计算机</a>）</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="driver-model-settings-properties-for-driver-projects.md" data-raw-source="[Driver Model Settings Properties for Driver Projects](driver-model-settings-properties-for-driver-projects.md)">驱动程序项目的驱动程序模型设置属性</a></td>
<td align="left"><p><a href="driver-verifier-properties-for--driver-projects.md" data-raw-source="[Driver Verifier Properties for Driver Package Projects](driver-verifier-properties-for--driver-projects.md)">驱动程序包项目的驱动程序验证程序属性</a></p></td>
</tr>
<tr class="even">
<td align="left"><a href="message-compiler-properties-for-driver-projects.md" data-raw-source="[Message Compiler Properties for Driver Projects](message-compiler-properties-for-driver-projects.md)">驱动程序项目的消息编译器属性</a></td>
<td align="left"><p><a href="kmdf-verifier-properties-for-driver-package-projects.md" data-raw-source="[KMDF Verifier Properties for Driver Package Projects](kmdf-verifier-properties-for-driver-package-projects.md)">驱动程序包项目的 KMDF 验证程序属性</a></p></td>
</tr>
<tr class="odd">
<td align="left"><a href="stampinf-properties-for-driver-projects.md" data-raw-source="[Stampinf Properties for Driver Projects](stampinf-properties-for-driver-projects.md)">驱动程序项目的 Stampinf 属性</a></td>
<td align="left"><p><a href="umdf-verifier-properties-for-driver-package-projects.md" data-raw-source="[UMDF Verifier Properties for Driver Package Projects](umdf-verifier-properties-for-driver-package-projects.md)">驱动程序包项目的 UMDF 验证程序属性</a></p></td>
</tr>
<tr class="even">
<td align="left"><a href="/windows-hardware/drivers/devtest/wpp-preprocessor" data-raw-source="[WPP Preprocessor (WPP Tracing)](../devtest/wpp-preprocessor.md)">WPP 预处理器（WPP 跟踪）</a></td>
<td align="left"><p><a href="inf2cat-properties-for-driver-package-projects.md" data-raw-source="[Inf2Cat Properties for Driver Package Projects](inf2cat-properties-for-driver-package-projects.md)">驱动程序包项目的 Inf2Cat 属性</a>（请参阅 <a href="../devtest/inf2cat.md" data-raw-source="[&lt;strong&gt;Inf2Cat&lt;/strong&gt;](../devtest/inf2cat.md)"><strong>Inf2Cat</strong></a> 工具）</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idtroubleshootingspanspan-idtroubleshootingspantroubleshooting-tip-for-building-a-driver"></a><span id="troubleshooting"></span><span id="TROUBLESHOOTING"></span>有关驱动程序生成的疑难解答提示


以下提示可以帮助你解决使用 WDK 和 Visual Studio 生成驱动程序时遇到的问题。

**使用 Visual Studio 中的选项提高生成输出的详细级别**

1.  选择“工具”&gt;“选项”。
2.  选择“项目和解决方案”文件夹，然后选择“生成并运行”。
3.  更改“MSBuild 项目生成输出详细级别”和“MSBuild 项目生成日志文件详细级别”选项。 默认情况下，这些选项设置为“最低”。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


* [在 Visual Studio 中生成](/previous-versions/visualstudio/visual-studio-2012/cyz1h6zd(v=vs.110))
* [为不同版本的 Windows 生成驱动程序](building-drivers-for-different-versions-of-windows.md)
* [使用含用户模式驱动程序和桌面应用的 Microsoft C 运行时](using-the-microsoft-c-runtime-with-user-mode-drivers-and-apps.md)
* [ProjectUpgradeTool](../devtest/projectupgradetool.md)
* [MSBuild](/visualstudio/msbuild/msbuild)
* [从现有源文件创建驱动程序](creating-a-driver-from-existing-source-files.md)
* [WDK 和 Visual Studio 生成环境](../devtest/wdk-and-visual-studio-build-environment.md)
* [签署驱动程序](signing-a-driver.md)
* [将驱动程序部署到测试计算机](deploying-a-driver-to-a-test-computer.md)