---
title: 获取 RPC 终结点信息
description: 获取 RPC 终结点信息
keywords:
- RPC 终结点信息
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 63f3c5802fceb9c01f83addac3e98c1b4221c2a6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96826149"
---
# <a name="get-rpc-endpoint-information"></a>获取 RPC 终结点信息


## <span id="ddk_get_rpc_endpoint_information_dbg"></span><span id="DDK_GET_RPC_ENDPOINT_INFORMATION_DBG"></span>


当使用 **-e** 开关时，终结点信息由 **！ rpcexts; Getendpointinfo** 扩展或 DbgRpc 显示。

如果指定了终结点号，则显示有关该终结点的信息。 如果省略此方法，则显示系统上所有进程的终结点。

下面的示例显示所有终结点。 这通常是获取进程 Id 和单元格编号的有用方法，可用作其他命令的参数：

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

有关可选参数的详细信息，请参阅 [**DbgRpc Command-Line Options**](dbgrpc-command-line-options.md)。

有关使用 RPC 调试器扩展的类似示例，请参阅 [**！ rpcexts. getendpointinfo**](-rpcexts-getendpointinfo.md)。

 

 





