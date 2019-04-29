---
title: 何时使用此方法
description: 何时使用此方法
ms.assetid: 40c9e2aa-35a3-4169-8305-bddc199a5c98
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: cd9db617441839193c6421a604adadd7795f3d9d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325849"
---
# <a name="when-to-use-this-technique"></a>何时使用此方法


## <span id="ddk_opening_a_crash_dump_dbg"></span><span id="DDK_OPENING_A_CRASH_DUMP_DBG"></span>


有几种情况下，它是非常有用，或甚至有必要，请向[控制用户模式下从内核调试程序调试](controlling-the-user-mode-debugger-from-the-kernel-debugger.md):

-   当您需要执行用户模式下调试，但还需要控制用户模式目标运行的 Windows 内核，或使用某些内核模式调试功能来分析此问题。

-   当你用户模式下的目标是如 CSRSS 或 WinLogon 的 Windows 进程。 有关如何调试这些目标的详细说明，请参阅[调试 CSRSS](debugging-csrss.md)并[调试 WinLogon](debugging-winlogon.md)。

-   当你的用户模式的目标是服务应用程序。 有关如何调试这些目标的详细说明，请参阅[调试服务应用程序](debugging-a-service-application.md)。

 

 





