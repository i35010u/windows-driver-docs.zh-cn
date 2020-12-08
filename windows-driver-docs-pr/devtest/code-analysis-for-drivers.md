---
title: 驱动程序的代码分析
description: 驱动程序的代码分析是一种编译时静态验证工具，用于检测 C 和 c + + 程序中的基本编码错误。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b4aed03d23891310122e39e28e1c186dc5638535
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96841349"
---
# <a name="code-analysis-for-drivers"></a>驱动程序的代码分析


驱动程序的代码分析是编译时使用的静态验证工具，它检测 C 和 C++ 程序中的基本编码错误，并包括专门检测（主要）内核模式驱动程序代码中的错误的专用模块。

**注意**  在以前版本的 WDK 中，代码分析的特定于驱动程序的模块是名为 PREfast 的独立工具的一部分，用于驱动程序 (PFD) 。 PREfast for Drivers 也已集成到 WDK 生成环境中，是 Microsoft 自动代码审查 (OACR) 的一部分。 从使用 Windows 驱动程序工具包 (WDK) 8 开始，驱动程序特定的功能已与 [使用代码分析工具分析应用程序质量](/previous-versions/visualstudio/visual-studio-2013/dd264897(v=vs.120))相集成。

 

## <a name="span-idin_this_sectionspanin-this-section"></a><span id="in_this_section"></span>本部分中的内容


-   [驱动程序的代码分析概述](code-analysis-for-drivers-overview.md)
-   [如何为驱动程序运行“代码分析”](how-to-run-code-analysis-for-drivers.md)
-   [Windows 驱动程序的 SAL 2 注释](sal-2-annotations-for-windows-drivers.md)
-   [驱动程序的代码分析警告](prefast-for-drivers-warnings.md)

 

