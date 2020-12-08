---
title: 设置 AML 调试会话
description: 设置 AML 调试会话
keywords:
- AMLI 调试器，安装程序
- acpi.sys 的调试版本
- acpi.sys
ms.date: 11/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: aa99c62029afd761ea2d6ba4aa07ab1eb4bf6a3e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96801883"
---
# <a name="setting-up-an-aml-debugging-session"></a>设置 AML 调试会话


## <span id="ddk_setting_up_an_aml_debugging_session_dbg"></span><span id="DDK_SETTING_UP_AN_AML_DEBUGGING_SESSION_DBG"></span>


AMLI 调试器代码包含在 Acpi.sys 中。 为了完全执行 AML 调试，必须在目标计算机上安装此驱动程序，这通常是这样。

若要激活在免费生成时中断到调试器，请使用 **dbgbrkon** 命令，该命令是 amli 调试器扩展的一部分。 有关详细信息，请参阅 [**！ amli set**](-amli-set.md)。

 
## <a name="see-also"></a>另请参阅

[AMLI 调试器](the-amli-debugger.md)
