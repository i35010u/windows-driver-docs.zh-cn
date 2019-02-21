---
title: 设置调试会话 AML
description: 设置调试会话 AML
ms.assetid: 04a44b92-215c-4735-9724-2b9f173f76a2
keywords:
- AMLI 调试器，安装程序
- acpi.sys 已检验的版本 （调试版本）
- acpi.sys
ms.date: 11/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: effab9f82549908bf58ea6e563888bb37baf1bc9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524000"
---
# <a name="setting-up-an-aml-debugging-session"></a>设置调试会话 AML


## <span id="ddk_setting_up_an_aml_debugging_session_dbg"></span><span id="DDK_SETTING_UP_AN_AML_DEBUGGING_SESSION_DBG"></span>


AMLI 调试器代码包含在 Acpi.sys。 若要完全执行 AML 调试，必须它通常是在目标计算机上安装此驱动程序。

若要激活中断到调试器在免费版本，请使用 **！ amli 设置 dbgbrkon** AMLI 调试器扩展的一部分的命令。 有关详细信息，请参阅[ **！ amli 集**](-amli-set.md)。

 
## <a name="see-also"></a>另请参阅

[AMLI 调试器](the-amli-debugger.md)

