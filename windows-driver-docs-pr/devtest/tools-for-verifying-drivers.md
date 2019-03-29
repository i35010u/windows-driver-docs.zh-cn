---
title: 用于验证驱动程序的工具
description: 用于验证驱动程序的工具
ms.assetid: 1d878be6-8730-4452-a35a-0635ebed9091
keywords:
- 工具 WDK，验证驱动程序
- 驱动程序开发工具 WDK，验证驱动程序
- 验证驱动程序 WDK
- 驱动程序验证 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 25afa7c27fc60ff7ddb7ac9aba00461c71213cb8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564034"
---
# <a name="tools-for-verifying-drivers"></a>用于验证驱动程序的工具


Windows Driver Kit (WDK) 包括几个非常全面的工具，旨在帮助您检测并解决在开发过程中的驱动程序代码中的错误。 其中的许多工具可以早早地用于开发过程，这个时候它们最重要，可以为你节省最多的时间和精力。

这些验证工具是 WDK 文档中所述，建议以供使用，因为每个工具以不同的方式检测不同类型的驱动程序错误。 这些工具是比手动检查高效得多。 这些工具可以检测到通常不在标准驱动程序测试中，找到的错误和它们包含了经验丰富的驱动程序开发人员和 Windows 驱动程序界面设计器的专业技能。

为获得最佳结果，使用所有可在您的驱动程序运行的工具。 如果省略任何一种工具，你可能会严重 bug 看驱动程序中。

本部分将首先简要讨论的代码验证工具的特征和包含在 WDK 中和在 Windows 或 Microsoft 提供的工具的调查。

本部分包括：

[静态和动态验证工具](static-and-dynamic-verification-tools.md)

[验证工具的调查](survey-of-verification-tools.md)

[DDI 符合性规则](https://msdn.microsoft.com/library/windows/hardware/ff552840)

[已检验的版本的 Windows](checked-build-of-windows.md)

[应用程序验证工具](application-verifier.md)

[驱动程序的代码分析](code-analysis-for-drivers.md)

[驱动程序验证程序](driver-verifier.md)

[静态驱动程序验证程序](static-driver-verifier.md)

[WDF 验证程序控件应用程序](wdf-verifier-control-application.md)

[WdfTester:WDF 驱动程序测试工具集](wdftester--wdf-driver-testing-toolset.md)

### <a name="span-idothertoolsspanspan-idothertoolsspanother-tools"></a><span id="other_tools"></span><span id="OTHER_TOOLS"></span>其他工具

如果可以访问与其他代码或驱动程序验证工具 （从其他源），我们建议你使用这些除了 WDK 中的工具。 请务必使用[Code Analysis for Drivers](code-analysis-for-drivers.md)， [Static Driver Verifier](static-driver-verifier.md)，并[Driver Verifier](driver-verifier.md)由于他们的 Windows 驱动程序，但每个工具的特定知识看起来在不同的方式中的代码，因此可帮助你查找并修复不同类型的问题。

 

 





