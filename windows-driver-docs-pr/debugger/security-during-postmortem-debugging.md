---
title: 事后调试过程中的安全性
description: 事后调试过程中的安全性
ms.assetid: 59c411c4-d829-4d1c-9820-e58188f0656c
keywords:
- 安全注意事项，事后调试
- 事后调试、 安全注意事项
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7ea002c275df1969aa466579345bb3c543ca95b4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523815"
---
# <a name="security-during-postmortem-debugging"></a>事后调试过程中的安全性


## <span id="ddk_security_during_postmortem_debugging_dbg"></span><span id="DDK_SECURITY_DURING_POSTMORTEM_DEBUGGING_DBG"></span>


只有管理员可以启用[事后调试](enabling-postmortem-debugging.md)。

但是，事后调试可用于整个系统，而不仅仅是为一个用户。 因此，已启用后，任何应用程序故障，都将激活的调试程序已被选-即使当前用户不具有管理权限。

此外，事后调试器继承相同的权限的应用程序的崩溃。 因此，如果发生故障，如 CSRSS 和 LSASS 的 Windows 服务，调试器将具有极高级别权限。

选择要启用事后调试时，应考虑到帐户这种情况。

 

 





