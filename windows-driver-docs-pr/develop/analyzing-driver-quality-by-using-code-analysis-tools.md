---
ms.assetid: 0FEF982B-7FEE-47C8-A906-F881E9D8F3D7
title: 使用代码分析和验证工具分析驱动程序
description: 代码分析和验证工具可以系统地分析源代码，从而帮助提高驱动程序的稳定性和可靠性。
ms.date: 07/02/2018
ms.localizationpriority: medium
ms.openlocfilehash: 3b5de3389a80e5b9bd7c445164d519360fc7f424
ms.sourcegitcommit: dabd74b55ce26f2e1c99c440cea2da9ea7d8b62c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/13/2019
ms.locfileid: "64368657"
---
# <a name="analyzing-a-driver-using-code-analysis-and-verification-tools"></a>使用代码分析和验证工具分析驱动程序

代码分析和验证工具可以系统地分析源代码，从而帮助提高驱动程序的稳定性和可靠性。 代码分析和验证工具可以检测到编译器和常规运行时测试遗漏的错误。 此外，它们还可以确定驱动程序是否与 Windows 操作系统内核正确交互。 利用 Microsoft Visual Studio 和 Windows 驱动程序工具包 (WDK)，你可以将代码分析和验证工具配置为在生成过程中运行，或者可以安排工具在预定时间分析驱动程序。

## <a name="span-idcccodeanalysistoolforwindowsdriversspanspan-idcccodeanalysistoolforwindowsdriversspanspan-idcccodeanalysistoolforwindowsdriversspancc-code-analysis-tool-for-windows-drivers"></a><span id="C_C___Code_Analysis_Tool_for_Windows_Drivers"></span><span id="c_c___code_analysis_tool_for_windows_drivers"></span><span id="C_C___CODE_ANALYSIS_TOOL_FOR_WINDOWS_DRIVERS"></span>适用于 Windows 驱动程序的 C/C++ 代码分析工具


WDK 的 Windows 8 版本为 Visual Studio 附带的 C/C++ 代码分析工具提供增强功能。 具体来说，WDK 提供专门检测内核模式驱动程序代码中的错误的专用驱动程序模块。 此驱动程序模块已集成到 C/C++ 代码分析工具中。

**何时使用：** 你可以在代码正确编译后尽早地在开发周期中运行适用于驱动程序的 C/C++ 代码分析工具。

有关 Visual Studio 中代码分析工具的信息，请参阅：

-   [使用“代码分析”分析应用程序质量](https://go.microsoft.com/fwlink/p/?linkid=226836)
-   [驱动程序的代码分析](https://msdn.microsoft.com/Library/Windows/Hardware/Hh454182)
-   [如何为驱动程序运行“代码分析”](https://msdn.microsoft.com/Library/Windows/Hardware/Hh454219)
-   [使用 SAL 注释减少 C/C++ 代码缺陷](https://go.microsoft.com/fwlink/p/?linkid=247283)
-   [Windows 驱动程序的 SAL 2.0 注释](https://msdn.microsoft.com/Library/Windows/Hardware/Hh454237)

**注意**  在 WDK 的以前版本中，代码分析的驱动程序特定模块是称为 PREfast for Drivers (PFD) 的独立工具的一部分。 PREfast for Drivers 也已集成到 WDK 生成环境中，是 Microsoft 自动代码审查 (OACR) 的一部分。

 

## <a name="span-idstaticdriververifierspanspan-idstaticdriververifierspanspan-idstaticdriververifierspanstatic-driver-verifier"></a><span id="Static_Driver_Verifier"></span><span id="static_driver_verifier"></span><span id="STATIC_DRIVER_VERIFIER"></span>静态驱动程序验证程序


静态驱动程序验证程序 (SDV) 是系统地分析 Windows 内核模式驱动程序的源代码的静态验证工具。 SDV 确定驱动程序是否与 Windows 操作系统内核正确交互。 SDV 可以从 Visual Studio 中的“驱动程序”  菜单或从“Visual Studio 命令提示”  窗口启动。

**何时使用：** 在开发周期的早期阶段对正确编译的驱动程序运行静态驱动程序验证程序。 在开始测试周期之前，请先运行静态驱动程序验证程序。

有关静态驱动程序验证程序的信息，请参阅：

-   概述：[静态驱动程序验证程序](https://msdn.microsoft.com/Library/Windows/Hardware/Ff552808)
-   如何执行此操作：[使用静态驱动程序验证程序查找驱动程序中的缺陷](https://msdn.microsoft.com/Library/Windows/Hardware/Hh454281)


 

 

 





