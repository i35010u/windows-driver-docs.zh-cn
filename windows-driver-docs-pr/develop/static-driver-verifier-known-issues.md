---
title: 静态驱动程序验证程序已知问题
description: 详细了解：静态驱动程序验证程序的已知问题 - Windows 10 版本1809
ms.date: 11/07/2018
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
ms.openlocfilehash: 70ee5d9e13ac420c6a6ac8b38bd1e86e53e0e3ec
ms.sourcegitcommit: f47c072e88dce59daba1231027b60eb56bd2cde9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/27/2020
ms.locfileid: "92689415"
---
# <a name="static-driver-verifier-known-issues---windows-10-version-1809"></a>静态驱动程序验证程序的已知问题 - Windows 10 版本1809

本页描述在 Windows 驱动程序工具包 (WDK) 中使用静态驱动程序验证程序 (SDV) 工具时可能遇到的常见问题。 以下信息特定于 Windows 10 2018 年 10 月更新版随附的工具版本（版本 1809）。

有关最新官方 WDK 的已知 SDV 问题，请参阅 [WDK 已知问题](https://social.msdn.microsoft.com/Forums/en-US/96c770a9-19a3-42d0-8d0e-bd200285d980/hardware-development-kits-for-windows-10-version-2004?forum=wdk)。

## <a name="interceptedbuild-failures"></a>InterceptedBuild 失败

主要症状：SDV 失败并出现 `FATAL ERROR: Unrecoverable error in InterceptedBuild stage`。  

检查 DVL 文件时，看到 `AssessmentScore` 值以及 `ScoreName="[driverName].[architecture].SDV.NA.Reason"` 和 `ScoreUnit="Unrecoverable error in InterceptedBuild stage."`

发生 InterceptedBuild 失败时，请执行以下步骤来诊断问题。

1. 在 Visual Studio 2017 本机工具命令行中结合 /debug 标志重新运行 SDV。  有关命令选项的详细信息，请参阅[静态驱动程序验证程序命令](../devtest/-static-driver-verifier-commands--msbuild-.md)。

    a. 首先，针对任何依赖库项目运行 SDV 的库函数。  例如： `msbuild /p:Configuration=Release /p:Platform=x64 /t:sdv /p:inputs="/lib /debug"`。

    b. 然后针对驱动程序项目本身运行 SDV。  例如：`msbuild /p:Configuration=Release /p:Platform=x64 /t:sdv /p:inputs="/check /debug"`

2. 确认在 InterceptedBuild 阶段是否再次发生失败。

3. 导航到运行 SDV 时在 driver 文件夹中生成的 `sdv` 文件夹。

4. 打开 `smvcl.log` 并搜索短语“internal compiler error”。

    a. 如果存在包含 **internal compiler error** 的错误消息和类似于 **fatal error C1001:An internal error has occurred in the compiler.  (compiler file 'msc1.cpp', line 1511)** 的短语，则表示出现了一个需要纠正的已知问题（错误纠正 ID 40705）。 如需进一步的帮助，请向 <stlogohelp@microsoft.com> 发送电子邮件。

    b. 如果存在包含 **internal compiler error** 的错误消息，但具体消息与上述内容不同，则可能表示需要纠正错误，但此问题不一定是现有的已知问题。  请向 <stlogohelp@microsoft.com> 发送电子邮件。

    c. 如果未看到任何包含 **internal compiler error** 的行，请搜索以 **error** 开头的任何行。  这些问题不一定需要纠正。  请向 <stlogohelp@microsoft.com> 发送电子邮件。

5. 打开 smvlink1.log 并搜索短语 **internal compiler error** 。

    a. 如果存在包含 **internal compiler error** 和 **slamcl: error: at phase 2: out of memory** 的错误消息，则表示出现了需要纠正的已知问题。

    b. 如果未看到任何包含 **internal compiler error** 的行，请搜索以 **error** 开头的任何行。  这些问题不一定需要纠正。  请向 <stlogohelp@microsoft.com> 发送电子邮件。

    c. 如果未看到上述任一错误，请联系 MSFT 获得支持。

若要联系 MSFT 以获得支持，请运行以下命令，以确保不会共享源代码：

1. 在启用 /debug 标志的情况下运行 SDV，并通过管道将输出传送到某个文本文件。

2. 导航到 driver 目录中的 `sdv` 文件夹，运行以下命令以清除可能会透露源代码的生成结果：

    ```cmd
    del /s *.obj
    del /s *.rawcfg*
    del /s *.li
    del /s *.pdb
    del /s *.sys
    ```

3. 将以下文件发送到 <stlogohelp@microsoft.com>：

    a. 包含运行 SDV 后的输出结果的文本文件

    b. **smexecute-NormalBuild.log** 文件

    c. **smvexecute-InterceptedBuild.log** 文件

    d. “sdv”子文件夹

## <a name="visual-studio-c-2013-runtimes-not-present"></a>Visual Studio C++ 2013 运行时不存在

主要症状：在不包含 Visual Studio C++ 2012 和 2013 运行时的系统上运行 SDV 时，用户可能会在弹出框中看到错误，例如，“由于找不到 \[MSVCR110.dll 或 VCOMP110.dll\]，代码执行无法继续”。  重新安装程序可能会解决此问题。

在这种情况下，解决方法是安装适用于 Visual Studio 2012 和 2013 的 x86 与 x64 Visual C++ Redistributable。

## <a name="best-practice-use-visual-studio-2017-version-158"></a>最佳做法：使用 Visual Studio 2017 版本 15.8 

默认情况下，代码分析不会自动在 Visual Studio 15.7 中生成驱动程序。  如果驱动程序依赖于所要生成的二进制文件，则可能会导致“输出”窗格中出现失败。  我们建议改用版本 15.8。

## <a name="dvl-generation-failure-after-removing-configuration-from-a-project"></a>从项目中删除配置后 DVL 生成失败

主要症状：通过“配置管理器”窗口从项目中删除某个配置后，用户在选择“创建驱动程序验证日志”时看到以下消息：`Please select a driver project. Driver Verification Log cannot be created for the selected platform tool set: 'v100'"`

解决方法： 

1. 备份项目文件，然后在文本编辑器中打开项目文件。

2. 在 `\<PropertyGroup Label="Globals"\>` 节下找到两个 XML 标记：一个标记的格式为 `\<Configuration\>\[Configuration type\]\</Configuration\>`，另一个标记的格式为 `\<Platform Condition="'$(Platform)' == ''"\>\[Architecture\]\</Platform\>`，其中，`\[Configuration type\]` 和 `\[Architecture\]` 是此类项目的默认配置和发布。

3. 将 `\[Configuration type\]` 和 `\[Architecture\]` 更新为项目适用的值。  例如，如果删除了 Win32 平台，则可将 `\[Architecture\]` 更新为 x64。

备选解决方法：

1. 打开 Visual Studio 2017 本机工具命令提示符。

2. 导航到 driver 文件夹。

3. 运行 `msbuild [Your Project] /p:Configuration=[Configuration type]  /p:Platform=[Architecture] /t:dvl`，其中，`\[Your Project\]` 是 vcxproj 文件，`\[Configuration type\]` 是有效的配置（例如 Release），`\[Architecture\]` 是有效的体系结构（例如 x64）。

## <a name="dvl-generation-does-not-work-on-servercore-use-server-gui"></a>在 ServerCore 上无法运行 DVL 生成，请使用 Server GUI

静态工具徽标测试在运行时将会失败。  测试日志显示类似于 `Failed to load 'C:\hlk\JobsWorkingDir\Tasks\WTTJobRun4749E809-0166-E811-8368-F4521454FFE1\Devfund_DvlTest.dll'. (Could not load managed test module because RoMetadata.dll could not be found)` 的失败

确保 TAEF 包已部署，或者 RoMetadata.dll 已部署到 PATH 环境变量中的某个位置。  

关键症状是无法加载 RoMetadata.dll。

如果 Server GUI 安装中的体系结构和 Windows 版本与 ServerCore 安装中相同，请将 Server GUI 中的 RoMetadata.dll 文件复制到 ServerCore。  可在 System32 文件夹（例如 `C:\Windows\System32`）中找到 DLL，应将它放在 ServerCore 计算机上的相同文件夹中。  这样，应该就可以在 ServerCore 上运行测试。  如果仍然遇到问题，请参考下一种解决方法。

第二种解决方法是在 Server GUI 上运行，然后将包与包含 Server Core 中的结果的包合并。 有关合并包的信息，请参阅[合并包](/windows-hardware/test/hlk/user/merge-packages)。

## <a name="static-driver-verifier-fails-with-exiting-libexeiwrapexe-with-0xc0000142-error"></a>静态驱动程序验证程序失败，lib.exe/iwrap.exe 退出并出现 0xc0000142 错误

smvbuild.log 文件包含类似于以下错误的消息：

```
c:\Program Files\Microsoft Visual Studio\2017\BuildTools\Common7\IDE\VC\VCTargets\Microsoft.CppCommon.targets(1144,5): error MSB6006: "Lib.exe" exited with code -1073741502.

Done executing task "LIB" -- FAILED.
```

这是已知问题。 如果此问题阻碍了 WHCP 认证，请使用勘误表 41600。
