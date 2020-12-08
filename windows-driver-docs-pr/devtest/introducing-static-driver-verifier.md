---
title: 静态驱动程序验证程序简介
description: 静态驱动程序验证程序简介
keywords:
- 静态驱动程序验证程序 WDK，关于静态驱动程序验证程序
- StaticDV WDK，关于静态驱动程序验证程序
- SDV WDK，关于静态驱动程序验证程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 00f055d4bd0bd839d7697a884bfcdd0b1c029b02
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96813853"
---
# <a name="introducing-static-driver-verifier"></a>静态驱动程序验证程序简介


静态驱动程序验证器 (SDV) 是在编译时运行的静态验证工具。 它通过符号执行源代码来探究驱动程序代码中的路径，从而尽可能少地假设操作系统状态和驱动程序的初始状态。 因此，SDV 可以在传统测试中缺少的路径中使用代码。

SDV 包含一组规则，这些规则定义驱动程序和操作系统内核之间的适当交互。 在验证过程中，SDV 将检查驱动程序代码的每个适用分支及其使用的库代码，并尝试证明驱动程序违反了规则。 如果 SDV 无法证明冲突，它会报告驱动程序符合规则并通过验证。

本节包括：

[了解静态驱动程序验证程序](understanding-static-driver-verifier.md)

[静态驱动程序验证程序的概念](static-driver-verifier-concepts.md)

[支持的驱动程序](supported-drivers.md)

[静态驱动程序验证程序的限制](static-driver-verifier-limitations.md)

 

 





