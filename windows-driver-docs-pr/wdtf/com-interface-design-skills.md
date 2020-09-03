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
ms.openlocfilehash: f51ad489f63d80466bf670fee16617b4a0079cc9
ms.sourcegitcommit: 7ca2d3e360a4ae1d4d3c3092bd34492a2645ef74
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89403510"
---
# <a name="com-interface-design-skills"></a>COM 接口设计技能


创建新的操作接口时，应考虑以下功能，设计对象模型：

1.  **直观**的。 以单词表示手动手动测试。

2.  **易于学习和使用。** 使其足够简单，使手动测试人员可以编写顶级方案脚本。 这些测试人员可以了解如何中断应用程序，让他们将这些知识分解为自动 [方案脚本](creating-wdtf-scenarios.md)。

3.  **面向对象**。 使接口面向对象，以提高工作效率。 幸运的是， [WDTF 方案模型](extending-the-framework.md) 使这一规则变得很困难。

4.  **可靠**。 操作接口旨在实现可重用性，因此，只需针对简单用例做好准备。

5.  **Diagnosable**。 请确保在设计中包括诊断。 尝试考虑用户使用您的界面时如何调试问题。 它有助于通过 [WPP 软件跟踪](../devtest/wpp-software-tracing.md)来检测代码。

 

