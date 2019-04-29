---
title: 操作系统模型
description: 操作系统模型
ms.assetid: a7200472-24e1-4ecf-86c7-a1b72c5661fc
keywords:
- 静态驱动程序验证程序 WDK，操作系统模型
- StaticDV WDK，操作系统模型
- SDV WDK，操作系统模型
- 操作系统模型 WDK Static Driver Verifier
- 利用 WDK Static Driver Verifier
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8fd5a9cb970bf8689caac966296453de3a5641e0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63356352"
---
# <a name="operating-system-model"></a>操作系统模型


SDV*操作系统模型*或*工具*包含部分和抽象代码段的 Windows 操作系统作为验证过程。 SDV 包括默认操作系统模型和用于验证特定的多个专用化的模型[规则](static-driver-verifier-rule.md)。 SDV 组装期间验证操作系统模型**检查**的步骤[验证过程](verification-process.md)。

此外，还有的驱动程序中的入口点调用在相同的方式为在 Windows 操作系统中执行您的驱动程序的部分的工具。

 

 





