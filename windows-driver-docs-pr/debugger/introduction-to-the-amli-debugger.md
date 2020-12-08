---
title: AMLI 调试器简介
description: AMLI 调试器简介
keywords:
- AMLI 调试器，概述
- ACPI 调试，计算机语言
- AML 解释器
ms.date: 11/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: 3cd6e28768294774408fa4695d89fe3b38553c48
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96801947"
---
# <a name="introduction-to-the-amli-debugger"></a>AMLI 调试器简介


## <span id="ddk_introduction_to_the_amli_debugger_dbg"></span><span id="DDK_INTRODUCTION_TO_THE_AMLI_DEBUGGER_DBG"></span>


调试标准内核模式代码与调试 ACPI (高级配置和电源接口) BIOS 之间存在明显差异。

Windows 及其驱动程序由针对特定处理器编译的二进制计算机代码组成，但 ACPI BIOS 的核心不在计算机代码中。 相反，它存储为 ACPI 计算机语言 (AML) 并由 Microsoft AML 解释器在运行时进行处理。

Microsoft AMLI 调试器是一组可调试 AML 代码的特殊调试工具。 

在 Windows 10 之前的 Windows 版本中，版本1803已使用 Windows ACPI 驱动程序 ( # A0) 的已检查版本。 在不再提供已检查的生成时，这将不再是这样。

AMLI 调试器完全能识别64位。 无论目标计算机或主计算机使用哪种处理器，AMLI 调试器都将正常工作。

 

 





