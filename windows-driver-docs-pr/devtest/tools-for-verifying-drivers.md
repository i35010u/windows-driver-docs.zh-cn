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
ms.openlocfilehash: b1f541cd66d37cb0a582dacad75dd44ab061fcf6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839997"
---
# <a name="tools-for-verifying-drivers"></a>用于验证驱动程序的工具

Windows 驱动程序工具包（WDK）包含几个非常全面的工具，旨在帮助你在开发过程中检测和更正驱动程序代码中的错误。 其中的许多工具可以早早地用于开发过程，这个时候它们最重要，可以为你节省最多的时间和精力。

这些验证工具在 WDK 文档中进行了介绍，建议你使用，因为每个工具都以不同的方式检测不同类型的驱动程序错误。 与手动检查相比，这些工具的效率要高得多。 这些工具可以检测通常在标准驱动程序测试中找不到的错误，并体现经验丰富的驱动程序开发人员和 Windows 驱动程序接口设计人员的专业技能。

为了获得最佳结果，请使用可以在你的驱动程序上运行的所有工具。 如果省略这些工具中的任何一种，可能会错过驱动程序中的严重错误。

本部分首先简要介绍了代码验证工具的特性，以及在 Windows 中或从 Microsoft 提供的工具的调查。

本部分包括：

[静态和动态验证工具](static-and-dynamic-verification-tools.md)

[验证工具的调查](survey-of-verification-tools.md)

[DDI 符合性规则](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)

[已检查 Windows 内部版本](checked-build-of-windows.md)

[应用程序验证工具](application-verifier.md)

[驱动程序的代码分析](code-analysis-for-drivers.md)

[驱动程序验证程序](driver-verifier.md)

[静态驱动程序验证程序](static-driver-verifier.md)

[WDF 验证程序控件应用程序](wdf-verifier-control-application.md)

[WdfTester： WDF 驱动程序测试工具集](wdftester--wdf-driver-testing-toolset.md)

### <a name="span-idother_toolsspanspan-idother_toolsspanother-tools"></a><span id="other_tools"></span><span id="OTHER_TOOLS"></span>其他工具

如果你有权访问其他代码或驱动程序验证工具（来自其他源），则我们建议你除了使用 WDK 中的工具以外，还可以使用这些工具。 请确保对驱动程序、[静态驱动程序验证](static-driver-verifier.md)程序和[驱动程序验证](driver-verifier.md)程序使用[代码分析](code-analysis-for-drivers.md)，因为它们特定于 Windows 驱动程序的知识，但每个工具都以不同的方式查看代码，从而帮助你查找和修复不同类型的问题。
