---
title: 设置 AML 调试会话
description: 设置 AML 调试会话
ms.assetid: 04a44b92-215c-4735-9724-2b9f173f76a2
keywords:
- AMLI 调试器，安装程序
- acpi .sys 的调试版本
- acpi .sys
ms.date: 11/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: f63b976e3866f9a284636651e6722b52d62f4fdc
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2019
ms.locfileid: "75209787"
---
# <a name="setting-up-an-aml-debugging-session"></a>设置 AML 调试会话


## <span id="ddk_setting_up_an_aml_debugging_session_dbg"></span><span id="DDK_SETTING_UP_AN_AML_DEBUGGING_SESSION_DBG"></span>


AMLI 调试器代码包含在中。 为了完全执行 AML 调试，必须在目标计算机上安装此驱动程序，这通常是这样。

若要激活在免费生成时中断到调试器，请使用**dbgbrkon**命令，该命令是 amli 调试器扩展的一部分。 有关详细信息，请参阅[**！ amli set**](-amli-set.md)。

 
## <a name="see-also"></a>另请参阅

[AMLI 调试器](the-amli-debugger.md)
