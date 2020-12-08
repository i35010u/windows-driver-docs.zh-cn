---
title: 操作系统模型
description: 操作系统模型
keywords:
- 静态驱动程序验证程序 WDK，操作系统型号
- StaticDV WDK，操作系统型号
- SDV WDK，操作系统型号
- 操作系统模型 WDK 静态驱动程序验证程序
- 利用 WDK 静态驱动程序验证程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f62e09a2f2976bf2de4e4f9db6f3c4521ac93cf6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840795"
---
# <a name="operating-system-model"></a>操作系统模型


SDV *操作系统模型* 或 *工具* 包含在验证过程中充当操作系统的 Windows 代码的部分和抽象段。 SDV 包括一个默认操作系统模型和几个专用模型，用于验证特定的 [规则](static-driver-verifier-rule.md)。 在 [验证过程](verification-process.md)的 **检查** 步骤中，SDV 汇编操作系统模型进行验证。

还可以通过调用驱动程序中的入口点，以与 Windows 操作系统相同的方式执行驱动程序的某些部分。

 

 





