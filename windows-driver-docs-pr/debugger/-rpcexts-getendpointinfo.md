---
title: rpcexts.getendpointinfo
description: Rpcexts.getendpointinfo 扩展搜索终结点信息的系统的 RPC 状态信息。
ms.assetid: 3efd0cd1-bcdd-4785-aa00-a32a7578219c
keywords:
- rpcexts.getendpointinfo Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- rpcexts.getendpointinfo
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 732c769f3c9636269576edb88f64762864b8f6c6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335724"
---
# <a name="rpcextsgetendpointinfo"></a>!rpcexts.getendpointinfo


**！ Rpcexts.getendpointinfo**扩展搜索终结点信息的系统的 RPC 状态信息。

```dbgcmd
    !rpcexts.getendpointinfo [EndpointName] 
!rpcexts.getendpointinfo -? 
```

## <a name="span-idddkrpcextsgetendpointinfodbgspanspan-idddkrpcextsgetendpointinfodbgspanparameters"></a><span id="ddk__rpcexts_getendpointinfo_dbg"></span><span id="DDK__RPCEXTS_GETENDPOINTINFO_DBG"></span>参数


<span id="_______EndpointName______"></span><span id="_______endpointname______"></span><span id="_______ENDPOINTNAME______"></span> *EndpointName*   
指定要显示的终结点的数量。 如果省略，将显示在系统上的所有进程的终结点。

<span id="_______-_______"></span> **-?**   
在命令提示符窗口中显示此扩展的一些简要帮助文本。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>不可用</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Rpcexts.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关调试 Microsoft 远程过程调用 (RPC) 的详细信息，请参阅[RPC 调试](rpc-debugging.md)。

<a name="remarks"></a>备注
-------

与 CDB 或用户模式下 WinDbg，则仅可以使用此扩展。

下面是一个示例：

```dbgcmd
0:002> !rpcexts.getendpointinfo
Searching for endpoint info ...
## PID  CELL ID   ST PROTSEQ        ENDPOINT
-------------------------------------------------------------
00a8 0000.0001 01            NMP \PIPE\InitShutdown
00a8 0000.0003 01            NMP \PIPE\SfcApi
00a8 0000.0004 01            NMP \PIPE\ProfMapApi
00a8 0000.0005 01           LRPC OLE5
00a8 0000.0007 01            NMP \pipe\winlogonrpc
00c4 0000.0001 01           LRPC ntsvcs
00c4 0000.0003 01            NMP \PIPE\ntsvcs
00c4 0000.0008 01            NMP \PIPE\scerpc
00d0 0000.0001 01            NMP \PIPE\lsass
00d0 0000.0003 01            NMP \pipe\WMIEP_d0
00d0 0000.0006 01           LRPC policyagent
00d0 0000.0007 01            NMP \PIPE\POLICYAGENT
0170 0000.0001 01           LRPC epmapper
0170 0000.0003 01            TCP 135
0170 0000.0005 01            SPX 34280
0170 0000.0006 01             NB 135
0170 0000.0007 01             NB 135
0170 0000.000b 01            NMP \pipe\epmapper
01c0 0000.0001 01            NMP \pipe\spoolss
01c0 0000.0003 01           LRPC spoolss
01c0 0000.0007 01           LRPC OLE7
020c 0000.0001 01           LRPC OLE2
020c 0000.0005 01           LRPC senssvc
020c 0000.0007 01            NMP \pipe\tapsrv
020c 0000.0009 01           LRPC tapsrvlpc
020c 0000.000c 01            NMP \PIPE\ROUTER
020c 0000.0016 01            NMP \pipe\WMIEP_20c
0218 0000.0001 01            NMP \PIPE\winreg
022c 0000.0001 01           LRPC LRPC0000022c.00000001
022c 0000.0003 01            TCP 1041
022c 0000.0005 01            SPX 24576
022c 0000.0006 01            NMP \PIPE\atsvc
0294 0000.0001 01           LRPC OLE3
0378 0000.0001 01           LRPC OLE9
026c 0000.0001 01            TCP 1118
0344 0000.0001 01           LRPC OLE12
```

有关使用 DbgRpc 工具的类似示例，请参阅[获取的 RPC 终结点信息](get-rpc-endpoint-information.md)。

 

 





