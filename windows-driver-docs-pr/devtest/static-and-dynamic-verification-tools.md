---
title: 静态和动态验证工具
description: 静态和动态验证工具
ms.assetid: 8bdf1f11-5deb-427b-b058-b9173e167f8d
keywords:
- 动态验证工具 WDK
- 静态验证工具 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7d3c40b83bb5b08c142b3ad628a04f91d0c801bd
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839320"
---
# <a name="static-and-dynamic-verification-tools"></a>静态和动态验证工具


有两种基本类型的验证工具：

-   **静态验证工具**会检查驱动程序代码，而不会运行该驱动程序。 由于这些工具不依赖于执行代码的测试，因此它们可能非常彻底。 从理论上讲，静态验证工具可以检查所有驱动程序代码，包括实践中很少执行的代码路径。 但是，由于该驱动程序并未实际运行，因此它们可能会产生误报结果。 也就是说，它们可能会在可能不会发生的代码路径中报告错误。

-   **动态验证工具**在运行驱动程序时检查驱动程序代码，这通常是通过截获对常用[驱动程序支持例程](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)的调用并将调用替换为同一例程的错误检查版本。 由于驱动程序实际上是在动态工具执行验证时运行的，因此不太常见。 但是，由于动态工具仅检测到监视驱动程序时所发生的操作，因此，如果驱动程序测试覆盖范围不够，这些工具可能会遗漏某些驱动程序缺陷。 同时，通过使用在运行时可用的信息（例如，从源代码中进行静态提取更难进行的信息），动态验证工具可以检测更难使用静态分析来检测的某些驱动程序错误类工具包.

最佳做法是使用静态和动态验证工具的组合。 静态工具使您能够检查在实践中难以练习的代码路径，而动态工具则查找驱动程序中发生的严重错误。

 

 





