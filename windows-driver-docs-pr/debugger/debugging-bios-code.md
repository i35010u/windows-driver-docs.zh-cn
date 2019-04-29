---
title: 调试 BIOS 代码
description: 调试 BIOS 代码
ms.assetid: 98f0381b-4f9d-4cf2-9860-8da20f6fbd38
keywords:
- BIOS 调试
- BIOS 调试概述
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2fe03c8240da0461ae35cc0be39f02750f110dd5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63377191"
---
# <a name="debugging-bios-code"></a>调试 BIOS 代码


## <span id="ddk_debugging_bios_code_dbg"></span><span id="DDK_DEBUGGING_BIOS_CODE_DBG"></span>


BIOS 代码并未内建从标准程序集代码，因此它需要不同的调试技术。

在基于 x86 的处理器上，在 BIOS 使用 16 位代码。 若要分解此代码，请使用[ **ux (反汇编 x86 BIOS)** ](ux--unassemble-x86-bios-.md)命令。 若要显示有关 Intel 包含多个处理器规范 (MP) 的信息，请使用[ **！ mp** ](-mps.md)扩展。

如果正在调试 ACPI BIOS 代码，在以上命令无效，因为 ACPI BIOS 编写在 ACPI 机器语言 (AML)。 若要分解此代码，应使用[ **！ amli u**](-amli-u.md)。 有关调试此类的详细信息，请参阅[ACPI 调试](acpi-debugging.md)。

 

 





