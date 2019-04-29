---
title: 获取 RPC 客户端调用信息
description: 获取 RPC 客户端调用信息
ms.assetid: 8b23428d-50e7-4613-a0ce-d1da5fa96ddf
keywords:
- RPC 客户端调用信息
- CCALL （客户端调用）
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3b2e89636c8be390a045341ea94de9ca4d43fd55
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380197"
---
# <a name="get-rpc-client-call-information"></a>获取 RPC 客户端调用信息


## <span id="ddk_get_rpc_client_call_information_dbg"></span><span id="DDK_GET_RPC_CLIENT_CALL_INFORMATION_DBG"></span>


通过显示客户端调用 (CCALL) 的调用信息 **！ rpcexts.getclientcallinfo**扩展，或通过 DbgRpc 时 **-a**使用开关。

允许使用四个可选参数。 这三个- *CallID*， *IfStart*，并*ProcNum* -确定使用的 RPC 来跟踪其调用信息。 第四个参数， *ProcessID*，是拥有该调用的进程的 PID。 应提供您知道要缩小搜索任何参数。

如果未不提供任何参数，将显示在系统中的所有已知的 CCALLs。 下面是此 （可能很长） 显示的示例：

```console
D:\wmsg>dbgrpc -a
Searching for call info ...
## PID  CELL ID   PNO  IFSTART  TIDNUMBER CALLID   LASTTIME PS CLTNUMBER ENDPOINT
------------------------------------------------------------------------------
0390 0000.0001 0000 19bb5061 0000.0000 00000001 00072bff 07 0000.0002 1120
```

可选参数的详细信息，请参阅[ **DbgRpc 命令行选项**](dbgrpc-command-line-options.md)。

有关使用 RPC 的类似示例调试器扩展，请参阅[ **！ rpcexts.getclientcallinfo**](-rpcexts-getclientcallinfo.md)。

**请注意**  如果只收集有关客户端调用对象的信息**完整**正在收集状态信息。 请参阅[启用 RPC 状态信息](enabling-rpc-state-information.md)有关详细信息。

 

 

 





