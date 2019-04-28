---
title: 静态和动态验证工具
description: 静态和动态验证工具
ms.assetid: 8bdf1f11-5deb-427b-b058-b9173e167f8d
keywords:
- 动态验证工具 WDK
- 静态验证工具 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 11eeac7e65b669d0d4fc9828f4478a678c561b6b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351160"
---
# <a name="static-and-dynamic-verification-tools"></a>静态和动态验证工具


有两种基本类型的验证工具：

-   **静态验证工具**检查驱动程序代码而无需运行该驱动程序。 这些工具不依赖演练代码的测试，因为它们可以是极其全面。 理论上讲，静态验证工具可以检查所有驱动程序代码，包括在实践中很少执行的代码路径。 但是，实际上未运行驱动程序，因为它们可能产生误报的结果。 也就是说，它们可能会报告可能不会在实践中的代码路径中的错误。

-   **动态验证工具**检查驱动程序代码，该驱动程序运行时，通常通过截获调用，以常用[驱动程序支持例程](https://msdn.microsoft.com/library/windows/hardware/ff544200)和替换调用到其自己的错误检查版本相同例程。 驱动程序实际运行时动态工具将执行验证，因为很少误报结果。 但是，由于动态工具检测到它们正在监视该驱动程序时出现的操作，这些工具可能会遗漏某些驱动程序缺陷如果驱动程序测试覆盖范围是不够的。 在同一时间，通过使用提供的信息在运行时，例如，很难从源代码，以静态方式提取的信息动态验证工具可以检测特定类别的驱动程序的错误更难检测具有静态分析工具。

最佳做法是使用静态和动态验证工具的组合。 静态工具，可检查难以同时动态工具查找驱动程序中发生的严重错误，在实践中，执行的代码路径。

 

 





