---
title: 通过和未通过验证
description: 通过和未通过验证
ms.assetid: 2639358b-eb6a-49b7-b23a-877a452917dc
keywords:
- 静态驱动程序验证程序 WDK，验证结果
- StaticDV WDK，验证结果
- SDV WDK，验证结果
- 结果 WDK Static Driver Verifier
- 已通过的验证 WDK Static Driver Verifier
- 验证失败的 WDK Static Driver Verifier
- 无结论验证 WDK Static Driver Verifier
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a840d3ddf31d7fa1ee33a997ce09e196eb6d9d3a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63356344"
---
# <a name="passing-and-failing-a-verification"></a>通过和未通过验证


SDV 验证规则的具有三个基本的结果：

-   该驱动程序*传递*验证。

-   该驱动程序*失败*验证。

-   结果是*无结论*。

之前得出任何结论根据这些结果，应了解每个结果，并注意它们所需要的许多限制。 不应判断为驱动程序的最终还是已完成评估任何结果。

### <a name="span-idverificationresultsspanspan-idverificationresultsspanverification-results"></a><span id="verification_results"></span><span id="VERIFICATION_RESULTS"></span>验证结果

驱动程序*传递*SDV 验证时，浏览在驱动程序中的所有相关的执行路径之后的代码，SDV[验证引擎](verification-engine.md)不能证明该驱动程序违反了所选的规则以进行验证。

驱动程序*失败*SDV 验证引擎证明该驱动程序至少一次违反规则时验证。 冲突被称为*脱离*。 如果该驱动程序不止一次违反规则，SDV 报告*多个缺陷*。

验证是*无结论*如果因超时而在完成之前终止 (**超时**结果) 或内存不足 ( **Spaceout**结果)，或当 SDV无法访问一个通过或失败的结论 (**不确定**结果)。 此外，SDV 可能遇到了阻止其完成其任务的内部工具错误。 (有关结果的详细信息，请参阅[解释静态驱动程序验证工具结果](interpreting-static-driver-verifier-results.md)。)

当规则不适用于该驱动程序，例如，如果该驱动程序不会使验证规则的设备驱动程序接口的使用，SDV 报告的规则是**不适用**。

 

 





