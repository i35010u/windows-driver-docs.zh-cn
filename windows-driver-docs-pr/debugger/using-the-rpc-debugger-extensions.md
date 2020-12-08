---
title: 使用 RPC 调试器扩展
description: 使用 RPC 调试器扩展
keywords:
- 'RPC 扩展 ( # A0) '
- 'RPC 调试，扩展 ( # A0) '
- 'rpcexts.dll (RPC 扩展) '
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: f32016edd60f7b498b5f8907ba6112b8ed51cf08
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803019"
---
# <a name="using-the-rpc-debugger-extensions"></a>使用 RPC 调试器扩展


## <span id="ddk_using_the_rpc_debugger_extensions_dbg"></span><span id="DDK_USING_THE_RPC_DEBUGGER_EXTENSIONS_DBG"></span>


从 Rpcexts.dll 导出各种 RPC 调试器扩展。

用于显示 RPC 状态信息的 RPC 扩展将仅在用户模式下运行。 它们可从 CDB (或 NTSD) 或用户模式 WinDbg 使用。

用户模式调试器必须有目标应用程序，但目标与 RPC 扩展无关。 如果尚未运行调试器，只需使用一个不相关的目标 (（例如， **windbg 记事本** 或 **cdb winmine**) ）即可启动调试器。 然后，在 CDB 或 Debug 中使用 [**CTRL + C**](ctrl-c--break-.md) [|](debug---break.md) 在 WinDbg 中中断以停止目标并访问调试器命令窗口。

如果需要分析远程计算机中的 RPC 状态信息，应在需要分析的计算机上启动用户模式调试器，然后使用 [远程调试](remote-debugging.md)。

通过调试器访问 RPC 状态信息在压力环境中尤其有用，或者当调试器已在运行时使用。

 

 





