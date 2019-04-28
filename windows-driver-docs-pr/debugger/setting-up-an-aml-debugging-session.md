---
title: 设置 AML 调试会话
description: 设置 AML 调试会话
ms.assetid: 04a44b92-215c-4735-9724-2b9f173f76a2
keywords:
- AMLI 调试器，安装程序
- acpi.sys 已检验的版本 （调试版本）
- acpi.sys
ms.date: 11/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: effab9f82549908bf58ea6e563888bb37baf1bc9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342517"
---
# <a name="setting-up-an-aml-debugging-session"></a>设置 AML 调试会话


## <span id="ddk_setting_up_an_aml_debugging_session_dbg"></span><span id="DDK_SETTING_UP_AN_AML_DEBUGGING_SESSION_DBG"></span>


AMLI 调试器代码包含在 Acpi.sys。 若要完全执行 AML 调试，必须它通常是在目标计算机上安装此驱动程序。

若要激活中断到调试器在免费版本，请使用 **！ amli 设置 dbgbrkon** AMLI 调试器扩展的一部分的命令。 有关详细信息，请参阅[ **！ amli 集**](-amli-set.md)。

 
## <a name="see-also"></a>请参阅

[AMLI 调试器](the-amli-debugger.md)

