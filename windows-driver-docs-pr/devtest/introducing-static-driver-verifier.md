---
title: 引入的 Static Driver Verifier
description: 引入的 Static Driver Verifier
ms.assetid: fa6e8b0f-0d0f-4293-87ec-e67decd6acb7
keywords:
- WDK，关于 Static Driver Verifier 的 static Driver Verifier
- StaticDV WDK，关于 Static Driver Verifier
- SDV WDK，关于 Static Driver Verifier
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c6bb44e32f323c409d8f0d8930d2e289ad0210d2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545979"
---
# <a name="introducing-static-driver-verifier"></a>引入的 Static Driver Verifier


Static Driver Verifier (SDV) 是运行在编译时静态验证工具。 它通过种执行源代码，从而使代码有关的状态的操作系统和驱动程序的初始状态的最少可能假设了驱动程序代码中的路径。 因此，SDV 可以运用中传统测试会丢失的路径中的代码。

SDV 包括一套规则，用于定义驱动程序和操作系统内核正确交互。 在验证，SDV 将检查每个适用的驱动程序代码和库代码，它使用，并试图证明该驱动程序违反规则的分支。 如果无法证明违反 SDV，它将报告该驱动程序符合规则，并通过验证。

本部分包括：

[了解的 Static Driver Verifier](understanding-static-driver-verifier.md)

[Static Driver Verifier 概念](static-driver-verifier-concepts.md)

[支持的驱动程序](supported-drivers.md)

[Static Driver Verifier 限制](static-driver-verifier-limitations.md)

 

 





