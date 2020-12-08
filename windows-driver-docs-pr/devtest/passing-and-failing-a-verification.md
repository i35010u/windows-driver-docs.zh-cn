---
title: 通过和未通过验证
description: 通过和未通过验证
keywords:
- 静态驱动程序验证程序 WDK，验证结果
- StaticDV WDK，验证结果
- SDV WDK，验证结果
- 结果 WDK 静态驱动程序验证程序
- 已通过验证 WDK 静态驱动程序验证程序
- 验证失败的 WDK 静态驱动程序验证程序
- 无结论验证 WDK 静态驱动程序验证程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 211db7d4794f899cad33849f8d45bf2100fa5727
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96784005"
---
# <a name="passing-and-failing-a-verification"></a>通过和未通过验证


规则的 SDV 验证具有三个基本结果：

-   驱动程序 *通过* 验证。

-   驱动程序 *无法* 验证。

-   结果没有 *结论*。

根据这些结果绘制任何结论之前，您应了解每个结果，并注意它们所需要的众多资格。 不应将任何结果判断为驱动程序的最终或完整的计算结果。

### <a name="span-idverification_resultsspanspan-idverification_resultsspanverification-results"></a><span id="verification_results"></span><span id="VERIFICATION_RESULTS"></span>验证结果

当探索驱动程序代码中的所有相关执行路径之后，驱动程序将 *传递* SDV 验证，SDV [验证引擎](verification-engine.md) 无法证明驱动程序违反了所选的验证规则。

当 SDV 验证引擎证实驱动程序违反规则至少一次时，驱动程序将 *无法* 验证。 冲突称为 " *缺陷*"。 如果驱动程序多次违反了规则，SDV 会报告 *多个缺陷*。

如果验证在完成前终止，因为超时 (**超时** 结果) 或内存不足 (**Spaceout** 结果) ，或 SDV 未能达到不 **确定** 的结果 (，则验证没有 *结论*。 此外，SDV 可能遇到了阻止其完成其任务的内部工具错误。  (有关结果的详细信息，请参阅 [解释静态驱动程序验证程序结果](interpreting-static-driver-verifier-results.md)。 ) 

当规则不适用于驱动程序时，例如，如果驱动程序未使用该规则验证的设备驱动程序接口，则 SDV 将报告该规则 **不适用**。

 

 





