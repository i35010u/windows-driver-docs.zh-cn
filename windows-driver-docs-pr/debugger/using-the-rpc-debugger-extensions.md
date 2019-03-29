---
title: 使用 RPC 调试器扩展
description: 使用 RPC 调试器扩展
ms.assetid: 55303052-c5b3-4fe7-96ce-6f41a45a2358
keywords:
- RPC 扩展 (rpcexts.dll)
- RPC 调试扩展 (rpcexts.dll)
- rpcexts.dll （RPC 扩展）
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: a84f5da0e299935045e4b029f3441e743763dc71
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564797"
---
# <a name="using-the-rpc-debugger-extensions"></a>使用 RPC 调试器扩展


## <span id="ddk_using_the_rpc_debugger_extensions_dbg"></span><span id="DDK_USING_THE_RPC_DEBUGGER_EXTENSIONS_DBG"></span>


RPC 调试器扩展的各种从 Rpcexts.dll 导出。

用于显示 RPC 状态信息的 RPC 扩展才会在用户模式下运行。 从 CDB （或 NTSD） 或用户模式下 WinDbg 可以使用它们。

用户模式下调试程序必须具有目标应用程序，但目标无关的 RPC 扩展。 如果已在不运行调试器，您可以只需启动它与不相关的目标 (例如， **windbg 记事本**或**cdb winmine**)。 然后，使用[ **CTRL + C** ](ctrl-c--break-.md) CDB 中或[调试 |中断](debug---break.md)在 WinDbg 停止目标和访问调试器命令窗口中。

如果你需要分析 RPC 从远程计算机的状态信息，您应需要进行分析，以及如何将在计算机上启动用户模式调试器[远程调试](remote-debugging.md)。

通过在调试器中访问 RPC 状态信息是在压力环境中，或一个调试器已发生运行时特别有用。

 

 





