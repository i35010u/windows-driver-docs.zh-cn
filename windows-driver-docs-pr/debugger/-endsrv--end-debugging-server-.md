---
title: .endsrv（结束调试服务器）
description: .Endsrv 命令会使调试器能够取消活动的调试服务器。
ms.assetid: 6be6c774-fe6b-4bd4-8174-55ef207db3e6
keywords:
- .endsrv （结束调试服务器） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .endsrv (End Debugging Server)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d2dbf56eebfa51b66db806433fdb10a94722ec8a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563127"
---
# <a name="endsrv-end-debugging-server"></a>.endsrv（结束调试服务器）


**.Endsrv**命令将导致调试器取消活动的调试服务器。

```dbgcmd
.endsrv ServerID 
```

## <a name="span-idddkmetaenddebuggingserverdbgspanspan-idddkmetaenddebuggingserverdbgspanparameters"></a><span id="ddk_meta_end_debugging_server_dbg"></span><span id="DDK_META_END_DEBUGGING_SERVER_DBG"></span>参数


<span id="_______ServerID______"></span><span id="_______serverid______"></span><span id="_______SERVERID______"></span> *ServerID*   
指定调试服务器的 ID。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

仅当正在执行通过调试器的远程调试时，可以使用此命令。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>模式</strong></p></td>
<td align="left"><p>仅限用户模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>实时、 崩溃转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关远程调试的详细信息，请参阅[远程调试通过调试器](remote-debugging-through-the-debugger.md)。

<a name="remarks"></a>备注
-------

必须颁发 **.endsrv**命令从调试服务器或从一个已连接到调试服务器的调试客户端。

若要确定调试服务器的 ID，请使用[ **.servers （列表调试服务器）** ](-servers--list-debugging-servers-.md)命令。

**.Endsrv**命令可以终止调试服务器，但它不能终止的进程服务器或 KD 连接服务器。 有关如何结束这些服务器的信息，请参阅[控制进程服务器会话](controlling-a-process-server-session.md)并[控制 KD 连接服务器会话](controlling-a-kd-connection-server-session.md)。 (还有，但是，一个异常情况 **.endsrv**可以结束的进程服务器，以编程方式启动; 有关详细信息，请参阅[ **IDebugClient::StartProcessServer** ](https://msdn.microsoft.com/library/windows/hardware/ff558810).)

如果取消调试服务器，可以防止任何将来的调试客户端将附加到服务器。 但是，如果取消调试服务器，则不分离当前附加到服务器的任何客户端。

请考虑以下这种情况。 假设如下例所示启动某些调试服务器。

```dbgcmd
0:000> .server npipe:pipe=rabbit
Server started with 'npipe:pipe=rabbit'
0:000> .server tcp:port=7
Server started with 'tcp:port=7'
```

然后，您决定使用密码，如以下示例所示。

```dbgcmd
0:000> .server npipe:pipe=tiger,password=hardtoguess
Server started with 'npipe:pipe=tiger,password=hardtoguess'
```

但更早版本的服务器仍在运行，因此应取消它们，如以下示例所示。

```dbgcmd
0:000> .servers
0 - Debugger Server - npipe:Pipe=rabbit
1 - Debugger Server - tcp:Port=7
2 - Debugger Server - npipe:Pipe=tiger,Password=*
0:000> .endsrv 0
Server told to exit.  Actual exit may be delayed until
the next connection attempt.
0:000> .endsrv 1
Server told to exit.  Actual exit may be delayed until
the next connection attempt.
0:000> .servers
0 - <Disabled, exit pending>
1 - <Disabled, exit pending>
2 - Debugger Server - npipe:Pipe=tiger,Password=*
```

最后，若要确保没有任何连接到计算机时更早版本的服务器处于活动状态，请使用[ **.clients （列表调试客户端）** ](-clients--list-debugging-clients-.md)命令。

```dbgcmd
0:000> .clients
HotMachine\HostUser, last active Mon Mar 04 16:05:21 2002
```

**谨慎**  使用 TCP、 NPIPE 或 COM 协议使用密码提供只有少量的保护，因为未加密密码。 当使用密码和 SSL 或 SPIPE 协议时，密码进行加密。 如果你想要建立安全的远程会话，必须使用 SSL 或 SPIPE 协议。

 

 

 





