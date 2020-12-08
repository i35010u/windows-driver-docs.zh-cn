---
title: 何时使用此方法
description: 何时使用此方法
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9a9c259b94945fd6960f18f04d979ab771b80657
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96802841"
---
# <a name="when-to-use-this-technique"></a>何时使用此方法


## <span id="ddk_opening_a_crash_dump_dbg"></span><span id="DDK_OPENING_A_CRASH_DUMP_DBG"></span>


在以下几种情况下，它非常有用，甚至需要 [从内核调试器中控制用户模式调试](controlling-the-user-mode-debugger-from-the-kernel-debugger.md)：

-   当您需要执行用户模式调试时，还需要控制用户模式目标正在运行的 Windows 内核，或者需要使用某些内核模式调试功能来分析问题。

-   用户模式目标为 Windows 进程（如 CSRSS 或 WinLogon）时。 有关如何调试这些目标的详细说明，请参阅 [调试 CSRSS](debugging-csrss.md) 和 [调试 WinLogon](debugging-winlogon.md)。

-   用户模式目标为服务应用程序时。 有关如何调试这些目标的详细说明，请参阅 [调试服务应用程序](debugging-a-service-application.md)。

 

 





