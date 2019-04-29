---
title: AMLI 调试器简介
description: AMLI 调试器简介
ms.assetid: f210171c-2226-4bd6-bbb4-aee4b087e575
keywords:
- AMLI 调试器概述
- ACPI 调试机器语言
- AML 解释器
ms.date: 11/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: 5334a3161e53046fa48f8020bf03d90bdfe9213f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374345"
---
# <a name="introduction-to-the-amli-debugger"></a>AMLI 调试器简介


## <span id="ddk_introduction_to_the_amli_debugger_dbg"></span><span id="DDK_INTRODUCTION_TO_THE_AMLI_DEBUGGER_DBG"></span>


有明显的区别调试标准内核模式代码和调试 （高级配置和电源接口） 的 ACPI BIOS。

而 Windows，其驱动程序组成二进制编译具有特定处理器的机器码，核心的 ACPI BIOS 不在计算机代码。 相反，它存储为 ACPI 机器语言 (AML)，并为在其运行时由 Microsoft AML 解释器进行处理。

Microsoft AMLI 调试器是一组特殊的调试工具，可以调试 AML 代码。 

在 Windows 10 之前的 Windows 版本，使用了版本 1803 检查生成的 Windows ACPI 驱动程序 (Acpi.sys)。 此不能再用例。

AMLI 调试器是完全 64-bit 注意。 哪些处理器正由目标计算机或主机计算机，无论 AMLI 调试器将正常工作。

 

 





