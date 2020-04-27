---
title: Windows 调试工具（WinDbg、KD、CDB、NTSD）
description: 从这里开始大致了解 Windows 调试工具。 此工具集包括 WinDbg 和其他调试程序。
ms.assetid: 938ef180-84de-442f-9b6c-1138c2fc8d5a
keywords:
- Windows 调试工具
- Windows 调试
- Windows 调试器
- 内核调试
- 内核调试程序
- WinDbg
ms.date: 02/22/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
ms.openlocfilehash: 982379cd73e2949bdcd7d0bc46ff53e1fce55f2d
ms.sourcegitcommit: 988d100e4d3b218a59fdac034d39a1816d145c85
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/24/2020
ms.locfileid: "74861423"
---
# <a name="debugging-tools-for-windows-windbg-kd-cdb-ntsd"></a>Windows 调试工具（WinDbg、KD、CDB、NTSD）

从这里开始大致了解 Windows 调试工具。 此工具集包括 WinDbg 和其他调试程序。


## <a name="span-id3_ways_to_get_debugging_tools_for_windowsspanspan-id3_ways_to_get_debugging_tools_for_windowsspanspan-id3_ways_to_get_debugging_tools_for_windowsspaninstall-debugging-tools-for-windows"></a><span id="3_ways_to_get_Debugging_Tools_for_Windows"></span><span id="3_ways_to_get_debugging_tools_for_windows"></span><span id="3_WAYS_TO_GET_DEBUGGING_TOOLS_FOR_WINDOWS"></span>安装 Windows 调试工具

可以将 Windows 调试工具作为开发工具包的一部分或作为独立的工具集进行获取：

-   **作为 WDK 的一部分**

    Windows 调试工具包含在 Windows 驱动程序工具包 (WDK) 中。 若要获取 WDK，请参阅[下载 Windows 驱动程序工具包 (WDK)](https://docs.microsoft.com/windows-hardware/drivers/download-the-wdk)。


-   **作为 Windows SDK 的一部分**

    Windows 调试工具包含在 Windows 软件开发工具包 (SDK) 中。 若要下载安装程序或 ISO 映像，请参阅 Windows 开发人员中心上的 [Windows 10 SDK](https://developer.microsoft.com/windows/downloads/windows-10-sdk)。


-   **作为独立工具集**

    可以单独安装 Windows 调试工具而不安装 Windows SDK 或 WDK，方法是启动 Windows SDK 的安装，然后在要安装的功能列表中仅选择“Windows 调试工具”  （并清除所有其他功能的选择）。 若要下载安装程序或 ISO 映像，请参阅 Windows 开发人员中心上的 [Windows 10 SDK](https://developer.microsoft.com/windows/downloads/windows-10-sdk)。


## <a name="span-idgetting_started_with_windows_debuggingspanspan-idgetting_started_with_windows_debuggingspanspan-idgetting_started_with_windows_debuggingspanget-started-with-windows-debugging"></a><span id="Getting_Started_with_Windows_Debugging"></span><span id="getting_started_with_windows_debugging"></span><span id="GETTING_STARTED_WITH_WINDOWS_DEBUGGING"></span>Windows 调试入门

若要开始使用 Windows 调试，请参阅 [Windows 调试入门](getting-started-with-windows-debugging.md)。

若要开始调试内核模式驱动程序，请参阅[调试通用驱动程序 -“逐步操作”实验室（Echo 内核模式）](debug-universal-drivers---step-by-step-lab--echo-kernel-mode-.md)。 这是一个“逐步操作”实验室，演示了如何使用 WinDbg 调试 Echo（一个使用内核模式驱动程序框架 (KMDF) 的示例驱动程序）。


## <a name="span-iddebugging_environmentsspanspan-iddebugging_environmentsspanspan-iddebugging_environmentsspandebugging-environments"></a><span id="Debugging_environments"></span><span id="debugging_environments"></span><span id="DEBUGGING_ENVIRONMENTS"></span>调试环境

如果计算机安装了 Visual Studio 和 WDK，就会有六个可用的调试环境。 有关这些环境的说明，请参阅[调试环境](debuggers-in-the-debugging-tools-for-windows-package.md)。

所有这些调试环境都提供适用于同一基础调试引擎（在 Windows 符号调试程序引擎 (Dbgeng.dll) 中实现）的用户界面。 该调试引擎也称为  “Windows 调试程序”，这六个调试环境统称为  “Windows 调试程序”。

> [!NOTE]
>  Visual Studio 包含自己的调试环境和调试引擎，它们统称为“Visual Studio 调试程序”。 若要了解如何在 Visual Studio 中进行调试，请参阅[在 Visual Studio 中调试](https://docs.microsoft.com/visualstudio/debugger/)。 对于调试托管代码（例如 C#）而言，使用 Visual Studio 调试程序通常是最容易的入门方法。


## <a name="span-idwindows_debuggersspanspan-idwindows_debuggersspanspan-idwindows_debuggersspanwindows-debuggers"></a><span id="Windows_debuggers"></span><span id="windows_debuggers"></span><span id="WINDOWS_DEBUGGERS"></span>Windows 调试程序

Windows 调试程序可以在基于 x86、x64 或 ARM 的处理器上运行，并且可以调试在那些相同体系结构上运行的代码。 有时候，调试程序和要调试的代码运行在同一计算机上，但另外一些时候，调试程序和要调试的代码则运行在不同的计算机上。 不管哪一种情况，运行调试程序的计算机均称为“主计算机”  ，被调试的计算机均称为“目标计算机”  。 不管是主机计算机还是目标计算机，Windows 调试程序都支持以下 Windows 版本。

-   Windows 10 和 Windows Server 2016
-   Windows 8.1 和 Windows Server 2012 R2
-   Windows 8 和 Windows Server 2012
-   Windows 7 和 Windows Server 2008 R2


## <a name="span-idsymbols_and_symbol_filesspanspan-idsymbols_and_symbol_filesspanspan-idsymbols_and_symbol_filesspansymbols-and-symbol-files"></a><span id="Symbols_and_Symbol_Files"></span><span id="symbols_and_symbol_files"></span><span id="SYMBOLS_AND_SYMBOL_FILES"></span>符号和符号文件

符号文件存储了在运行可执行二进制文件时不需要的各种数据，但在调试代码时，符号文件非常有用。 若要详细了解如何创建和使用符号文件，请参阅 [Windows 调试符号（WinDbg、KD、CDB、NTSD）](symbols.md)。


## <a name="span-idblue_screens_and_crash_dump_filesspanspan-idblue_screens_and_crash_dump_filesspanspan-idblue_screens_and_crash_dump_filesspanblue-screens-and-crash-dump-files"></a><span id="Blue_Screens_and_crash_dump_files"></span><span id="blue_screens_and_crash_dump_files"></span><span id="BLUE_SCREENS_AND_CRASH_DUMP_FILES"></span>蓝屏和崩溃转储文件

如果 Windows 停止工作并显示一个蓝屏，则表示为防止数据丢失，计算机已突然关闭，并显示一个 Bug 检查代码。 有关详细信息，请参阅 [Bug 检查（蓝屏）](bug-checks--blue-screens-.md)。 可以使用 WinDbg 和其他 Windows 调试程序来分析 Windows 关闭时创建的故障转储文件。 有关详细信息，请参阅[使用 Windows 调试程序 (WinDbg) 进行故障转储分析](crash-dump-files.md)。


## <a name="span-idtools_and_utilitiesspanspan-idtools_and_utilitiesspanspan-idtools_and_utilitiesspantools-and-utilities"></a><span id="Tools_and_utilities"></span><span id="tools_and_utilities"></span><span id="TOOLS_AND_UTILITIES"></span>工具和实用程序

除了调试程序，Windows 调试工具还包括一系列适用于调试的工具。 如需这些工具的完整列表，请参阅 [Windows 调试工具中包含的工具](extra-tools.md)。


## <a name="span-idadditional_documentationspanspan-idadditional_documentationspanspan-idadditional_documentationspanadditional-documentation"></a><span id="Additional_documentation"></span><span id="additional_documentation"></span><span id="ADDITIONAL_DOCUMENTATION"></span>其他文档

如需与 Windows 调试工具相关的其他信息，请参阅[调试资源](debugging-resources.md)。 若要了解 Windows 10 的新增功能，请参阅 [Windows 调试工具：Windows 10 的新增功能](debugging-tools-for-windows--new-for-windows-10.md)。
