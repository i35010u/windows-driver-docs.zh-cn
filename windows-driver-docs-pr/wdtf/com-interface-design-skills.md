---
title: COM 接口设计技能
description: COM 接口设计技能
ms.assetid: 3a3adbc2-af6f-4495-8993-fd25d56ffad6
keywords:
- Windows 设备测试框架 WDK，操作接口
- WDTF WDK，操作接口
- 操作接口 WDK WDTF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c17a5a68d3ef84b708fccca5405febb9066e7f61
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568780"
---
# <a name="com-interface-design-skills"></a>COM 接口设计技能


创建新的操作接口时，应设计您的对象模型中考虑到了以下功能：

1.  **直观**。 表示在单词中的手动测试。

2.  **易于学习和使用。** 使其容易使用，以便手动测试人员可以编写的顶级方案脚本。 这些测试人员具有有价值的见解如何中断应用程序，因此请让它们到自动巩固这一知识[方案脚本](creating-wdtf-scenarios.md)。

3.  **面向对象的**。 使你的接口的面向对象，来提高工作效率。 幸运的是， [WDTF 方案模型](extending-the-framework.md)就很难为中断此规则。

4.  **可靠**。 操作接口应以可重用性，因此试着不只简单用例准备。

5.  **套**。 请确保在设计中包含诊断性。 试着考虑在使用您的界面时，人员调试问题的方式。 若要检测代码可帮助[WPP 软件跟踪](https://msdn.microsoft.com/library/windows/hardware/ff556204)。

 

 




