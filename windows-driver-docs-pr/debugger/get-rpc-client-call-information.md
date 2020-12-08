---
title: 获取 RPC 客户端调用信息
description: 获取 RPC 客户端调用信息
keywords:
- RPC 客户端调用信息
- 'CCALL (客户端调用) '
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: d23d9ba42e3a35f5f39741f1b8403390209c24b5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96816335"
---
# <a name="get-rpc-client-call-information"></a>获取 RPC 客户端调用信息


## <span id="ddk_get_rpc_client_call_information_dbg"></span><span id="DDK_GET_RPC_CLIENT_CALL_INFORMATION_DBG"></span>


当使用 **-a** 开关时，客户端调用 (CCALL) 调用信息由 **！ Rpcexts getclientcallinfo** 或 DbgRpc 显示。

允许使用四个可选参数。 其中三个-- *CallID*、 *IfStart* 和 *ProcNum* --标识 RPC 用于跟踪其调用的信息。 第四个参数 *ProcessID* 是拥有调用的进程的 PID。 你应提供知道的任何参数以缩小搜索范围。

如果未提供任何参数，则将显示系统中的所有已知 CCALLs。 下面是此 (可能很长) 显示的示例：

```console
D:\wmsg>dbgrpc -a
Searching for call info ...
## PID  CELL ID   PNO  IFSTART  TIDNUMBER CALLID   LASTTIME PS CLTNUMBER ENDPOINT
------------------------------------------------------------------------------
0390 0000.0001 0000 19bb5061 0000.0000 00000001 00072bff 07 0000.0002 1120
```

有关可选参数的详细信息，请参阅 [**DbgRpc Command-Line Options**](dbgrpc-command-line-options.md)。

有关使用 RPC 调试器扩展的类似示例，请参阅 [**！ rpcexts. getclientcallinfo**](-rpcexts-getclientcallinfo.md)。

**注意**   仅当收集 **完整** 状态信息时，才会收集有关客户端调用对象的信息。 有关详细信息，请参阅 [启用 RPC 状态信息](enabling-rpc-state-information.md) 。

 

 

 





