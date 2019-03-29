---
title: 获取 RPC 终结点信息
description: 获取 RPC 终结点信息
ms.assetid: 8e852855-896c-4553-8a58-8ca49c7b2e0a
keywords:
- RPC 终结点信息
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: e1d37305e12f731a46178ce9b919ecc8482ec8ed
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565940"
---
# <a name="get-rpc-endpoint-information"></a>获取 RPC 终结点信息


## <span id="ddk_get_rpc_endpoint_information_dbg"></span><span id="DDK_GET_RPC_ENDPOINT_INFORMATION_DBG"></span>


通过显示终结点信息 **！ rpcexts.getendpointinfo**扩展，或通过 DbgRpc 时 **-e**使用开关。

如果指定终结点号，则会显示有关该终结点的信息。 如果省略，将显示在系统上的所有进程的终结点。

以下示例显示的所有终结点。 这通常是有用的方式来获取进程 Id 和单元格可用作其他命令的参数的数字：

```console
D:\wmsg>dbgrpc -e
Searching for endpoint info ...
## PID  CELL ID   ST PROTSEQ        ENDPOINT
-------------------------------------------------------
00a8 0000.0001 01            NMP \PIPE\InitShutdown
00a8 0000.0003 01            NMP \PIPE\SfcApi
00a8 0000.0004 01            NMP \PIPE\ProfMapApi
00a8 0000.0007 01            NMP \pipe\winlogonrpc
00a8 0000.0008 01           LRPC OLE5
00c4 0000.0001 01           LRPC ntsvcs
00c4 0000.0003 01            NMP \PIPE\ntsvcs
00c4 0000.0008 01            NMP \PIPE\scerpc
00d0 0000.0001 01            NMP \PIPE\lsass
00d0 0000.0004 01            NMP \pipe\WMIEP_d0
00d0 0000.000b 01            NMP \PIPE\POLICYAGENT
00d0 0000.000c 01           LRPC policyagent
0170 0000.0001 01           LRPC epmapper
0170 0000.0003 01            TCP 135
0170 0000.0005 01            SPX 34280
0170 0000.0006 01             NB 135
0170 0000.0007 01             NB 135
0170 0000.000b 01            NMP \pipe\epmapper
01b8 0000.0001 01            NMP \pipe\spoolss
01b8 0000.0003 01           LRPC spoolss
01b8 0000.0007 01           LRPC OLE7
00ec 0000.0001 01           LRPC OLE2
00ec 0000.0003 01           LRPC senssvc
00ec 0000.0007 01            NMP \pipe\tapsrv
00ec 0000.0008 01           LRPC tapsrvlpc
00ec 0000.000c 01            NMP \PIPE\ROUTER
00ec 0000.0010 01            NMP \pipe\WMIEP_ec
0214 0000.0001 01            NMP \PIPE\winreg
022c 0000.0001 01           LRPC LRPC0000022c.00000001
022c 0000.0003 01            TCP 1058
022c 0000.0005 01            SPX 24576
022c 0000.0006 01            NMP \PIPE\atsvc
02a8 0000.0001 01           LRPC OLE3
0370 0000.0001 01           LRPC OLE9
0278 0000.0001 01            TCP 1120
030c 0000.0001 01           LRPC OLE12
```

可选参数的详细信息，请参阅[ **DbgRpc 命令行选项**](dbgrpc-command-line-options.md)。

有关使用 RPC 的类似示例调试器扩展，请参阅[ **！ rpcexts.getendpointinfo**](-rpcexts-getendpointinfo.md)。

 

 





