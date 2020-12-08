---
title: 调试 BIOS 代码
description: 调试 BIOS 代码
keywords:
- BIOS 调试
- BIOS 调试，概述
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: ced1fa50d3b2e7064b331a112c69579e54c442a7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96817537"
---
# <a name="debugging-bios-code"></a>调试 BIOS 代码


## <span id="ddk_debugging_bios_code_dbg"></span><span id="DDK_DEBUGGING_BIOS_CODE_DBG"></span>


BIOS 代码不是从标准程序集代码生成的，因此需要不同的调试技术。

在基于 x86 的处理器上，BIOS 使用16位代码。 若要反汇编此代码，请使用 [**ux (Unassemble X86 BIOS)**](ux--unassemble-x86-bios-.md) 命令。 若要显示有关 (MPS) 的 Intel 多处理器规范的信息，请使用 [**！ MPS**](-mps.md) 扩展。

如果正在调试 ACPI BIOS 代码，则上述命令不起作用，因为 ACPI BIOS 是使用 ACPI 计算机语言 (AML) 编写的。 若要反汇编此代码，应使用 [**！ amli u**](-amli-u.md)。 有关此类调试的详细信息，请参阅 [ACPI 调试](acpi-debugging.md)。

 

 





