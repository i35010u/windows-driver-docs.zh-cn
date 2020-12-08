---
title: 事后调试期间的安全性
description: 事后调试期间的安全性
keywords:
- 安全注意事项，事后调试
- 事后调试，安全注意事项
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: fd93d8ee97c1b47d3768c9e94e05a857c787d6c9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96829725"
---
# <a name="security-during-postmortem-debugging"></a>事后调试期间的安全性


## <span id="ddk_security_during_postmortem_debugging_dbg"></span><span id="DDK_SECURITY_DURING_POSTMORTEM_DEBUGGING_DBG"></span>


只有管理员才能启用 [事后调试](enabling-postmortem-debugging.md)。

但是，会对整个系统启用事后调试，而不只是为一个用户启用。 因此，在启用后，任何应用程序崩溃都将激活已选择的调试器（即使当前用户没有管理权限）。

此外，事后调试器继承与崩溃的应用程序相同的特权。 因此，如果 Windows 服务（如 CSRSS 和 LSASS）崩溃，则调试器将具有非常高的权限。

选择启用事后调试时，应考虑到这一点。

 

 





