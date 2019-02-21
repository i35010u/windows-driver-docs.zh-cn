---
title: 驱动程序的代码分析
description: 驱动程序的代码分析是一个编译时静态验证工具，检测 C 和 c + + 程序中的基本编码错误。
ms.assetid: 2F3549EF-B50F-455A-BDC7-1F67782B8DCA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 37d0b2a0df11e04523564c0e633d83482e424fb5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555665"
---
# <a name="code-analysis-for-drivers"></a>驱动程序的代码分析


驱动程序的代码分析是编译时使用的静态验证工具，其检测 C 和 C++ 程序中的基本编码错误，并包括专门检测（主要）内核模式驱动程序代码中的错误的专用模块。

**请注意**在以前版本的 WDK 中，代码分析的特定于驱动程序的模块是名为 PREfast for Drivers (PFD) 的独立工具的一部分。 PREfast for Drivers 也集成到了 WDK 生成环境中，是 Microsoft 自动代码审查 (OACR) 的一部分。 从开始使用 Windows Driver Kit (WDK) 8，特定于驱动程序的功能已集成与[Visual Studio 中的代码分析工具](https://go.microsoft.com/fwlink/p/?linkid=226836)。

 

## <a name="span-idinthissectionspanin-this-section"></a><span id="in_this_section"></span>在本部分中


-   [代码分析驱动程序概述](code-analysis-for-drivers-overview.md)
-   [如何运行代码分析的驱动程序](how-to-run-code-analysis-for-drivers.md)
-   [SAL 2 注释 Windows 驱动程序](sal-2-annotations-for-windows-drivers.md)
-   [代码分析驱动程序警告](prefast-for-drivers-warnings.md)

 

 





