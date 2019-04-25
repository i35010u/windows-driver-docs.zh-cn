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
ms.openlocfilehash: 418e8ca690b1d41046faa8cdba9f62d252725c05
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63371651"
---
# <a name="debugging-tools-for-windows-windbg-kd-cdb-ntsd"></a>Windows 调试工具（WinDbg、KD、CDB、NTSD）


从这里开始大致了解 Windows 调试工具。 此工具集包括 WinDbg 和其他调试程序。

## <a name="span-id3waystogetdebuggingtoolsforwindowsspanspan-id3waystogetdebuggingtoolsforwindowsspanspan-id3waystogetdebuggingtoolsforwindowsspan3-ways-to-get-debugging-tools-for-windows"></a><span id="3_ways_to_get_Debugging_Tools_for_Windows"></span><span id="3_ways_to_get_debugging_tools_for_windows"></span><span id="3_WAYS_TO_GET_DEBUGGING_TOOLS_FOR_WINDOWS"></span>通过 3 种方式获取 Windows 调试工具

-   **作为 WDK 的一部分**

    Windows 调试工具中包括在 WDK 中。 可以[在此处获取 WDK](https://docs.microsoft.com/windows-hardware/drivers/download-the-wdk)。

   
-   **作为独立工具集**

    如果只需下载 Windows 调试工具，请[安装 Windows SDK](https://developer.microsoft.com/windows/downloads/windows-10-sdk)，然后在安装过程中选择“Windows 调试工具”框并清除所有其他的框。


-   **作为 Windows SDK 的一部分**

    安装完整的 Windows 软件开发工具包 (SDK)。 Windows 调试工具中包括在 Windows WDK 中。 可以[在此处获取 Windows WDK](https://developer.microsoft.com/windows/downloads/windows-10-sdk)。


## <a name="span-idgettingstartedwithwindowsdebuggingspanspan-idgettingstartedwithwindowsdebuggingspanspan-idgettingstartedwithwindowsdebuggingspangetting-started-with-windows-debugging"></a><span id="Getting_Started_with_Windows_Debugging"></span><span id="getting_started_with_windows_debugging"></span><span id="GETTING_STARTED_WITH_WINDOWS_DEBUGGING"></span>Windows 调试入门


若要开始使用 Windows 调试，请参阅 [Windows 调试入门](getting-started-with-windows-debugging.md)。

若要开始调试内核模式驱动程序，请参阅[调试通用驱动程序 - 分步实验（Echo 内核模式）](debug-universal-drivers---step-by-step-lab--echo-kernel-mode-.md)。 这是一个分步实验，演示了如何使用 WinDbg 来调试示例 KMDF echo 驱动程序。

## <a name="span-iddebuggingenvironmentsspanspan-iddebuggingenvironmentsspanspan-iddebuggingenvironmentsspandebugging-environments"></a><span id="Debugging_environments"></span><span id="debugging_environments"></span><span id="DEBUGGING_ENVIRONMENTS"></span>调试环境


安装 Visual Studio 和 WDK 以后，就会有六个可用的[调试环境](debuggers-in-the-debugging-tools-for-windows-package.md)。 所有这些调试环境提供的用户界面适用于同一基础调试引擎，该引擎在 dbgeng.dll 中实现。 该调试引擎称为“Windows 调试程序”，这六个调试环境统称为“Windows 调试程序”。

**注意**  Visual Studio 包含自己的调试环境和调试引擎，统称“Visual Studio 调试程序”。 若要了解如何在 Visual Studio 中进行调试，请参阅 [Visual Studio 调试程序](https://go.microsoft.com/fwlink/p/?LinkID=238333)。 若要调试托管代码（例如 C#），则使用 Visual Studio 调试程序通常是最容易的入门方法。

 

## <a name="span-idwindowsdebuggersspanspan-idwindowsdebuggersspanspan-idwindowsdebuggersspanwindows-debuggers"></a><span id="Windows_debuggers"></span><span id="windows_debuggers"></span><span id="WINDOWS_DEBUGGERS"></span>Windows 调试程序


Windows 调试程序可以运行在基于 x86、x64 或 ARM 的处理器上，可以调试在基于 x86、x64 或 ARM 的处理器上运行的代码。 有时候，调试程序和要调试的代码运行在同一计算机上，但另外一些时候，调试程序和要调试的代码则运行在不同的计算机上。 不管哪一种情况，运行调试程序的计算机称为“主计算机”，被调试的计算机称为“目标计算机”。 不管是主机计算机还是目标计算机，Windows 调试程序都支持以下 Windows 版本。

-   Windows 10 和 Windows Server 2016

-   Windows 8.1 和 Windows Server 2012 R2

-   Windows 8 和 Windows Server 2012

-   Windows 7 和 Windows Server 2008 R2

## <a name="span-idsymbolsandsymbolfilesspanspan-idsymbolsandsymbolfilesspanspan-idsymbolsandsymbolfilesspansymbols-and-symbol-files"></a><span id="Symbols_and_Symbol_Files"></span><span id="symbols_and_symbol_files"></span><span id="SYMBOLS_AND_SYMBOL_FILES"></span>符号和符号文件


符号文件包含大量的数据，这些数据在运行二进制文件时实际上并不需要，但在调试代码时很有用。 若要详细了解如何创建和使用符号文件，请参阅 [Windows 调试符号（WinDbg、KD、CDB、NTSD）](symbols.md)。

## <a name="span-idbluescreensandcrashdumpfilesspanspan-idbluescreensandcrashdumpfilesspanspan-idbluescreensandcrashdumpfilesspanblue-screens-and-crash-dump-files"></a><span id="Blue_Screens_and_crash_dump_files"></span><span id="blue_screens_and_crash_dump_files"></span><span id="BLUE_SCREENS_AND_CRASH_DUMP_FILES"></span>蓝屏和崩溃转储文件


如果 Windows 停止工作并显示一个蓝屏，则表示为防止数据丢失，计算机已突然关闭，并显示一个 Bug 检查代码。 有关详细信息，请参阅 [Bug 检查（蓝屏）](bug-checks--blue-screens-.md)。 可以使用 WinDbg 和其他 Windows 调试程序来分析 Windows 关闭时创建的故障转储文件。 有关详细信息，请参阅[使用 Windows 调试程序 (WinDbg) 进行故障转储分析](crash-dump-files.md)。

## <a name="span-idtoolsandutilitiesspanspan-idtoolsandutilitiesspanspan-idtoolsandutilitiesspantools-and-utilities"></a><span id="Tools_and_utilities"></span><span id="tools_and_utilities"></span><span id="TOOLS_AND_UTILITIES"></span>工具和实用程序


除了调试程序，Windows 调试工具还包括一系列适用于调试的工具。 如需这些工具的完整列表，请参阅 [Windows 调试工具中包含的工具](extra-tools.md)。

## <a name="span-idadditionaldocumentationspanspan-idadditionaldocumentationspanspan-idadditionaldocumentationspanadditional-documentation"></a><span id="Additional_documentation"></span><span id="additional_documentation"></span><span id="ADDITIONAL_DOCUMENTATION"></span>其他文档


如需与 Windows 调试工具相关的其他信息，请参阅[调试资源](debugging-resources.md)。 若要了解 Windows 10 的新增功能，请参阅 [Windows 调试工具：Windows 10 的新增功能](debugging-tools-for-windows--new-for-windows-10.md)。

## <a name="span-idinthissectionspanspan-idinthissectionspanspan-idinthissectionspanin-this-section"></a><span id="In_this_section"></span><span id="in_this_section"></span><span id="IN_THIS_SECTION"></span>本部分中的内容


-   [Windows 调试入门](getting-started-with-windows-debugging.md)
-   [调试资源](debugging-resources.md)
-   [调试程序操作](debugger-operation-win8.md)
-   [调试方法](debugging-techniques.md)
-   [符号](symbols.md)
-   [故障转储分析](crash-dump-files.md)
-   [Bug 检查（蓝屏）](bug-checks--blue-screens-.md)
-   [调试程序参考](debugger-reference.md)

 

 





