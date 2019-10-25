---
title: .endsrv（结束调试服务器）
description: Endsrv 命令使调试器取消活动的调试服务器。
ms.assetid: 6be6c774-fe6b-4bd4-8174-55ef207db3e6
keywords:
- 。 endsrv （最终调试服务器） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .endsrv (End Debugging Server)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 4f88bed3079c61ca88edb5f8beab9b0bb9ece48e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837604"
---
# <a name="endsrv-end-debugging-server"></a>.endsrv（结束调试服务器）


**Endsrv**命令使调试器取消活动的调试服务器。

```dbgcmd
.endsrv ServerID 
```

## <a name="span-idddk_meta_end_debugging_server_dbgspanspan-idddk_meta_end_debugging_server_dbgspanparameters"></a><span id="ddk_meta_end_debugging_server_dbg"></span><span id="DDK_META_END_DEBUGGING_SERVER_DBG"></span>Parameters


<span id="_______ServerID______"></span><span id="_______serverid______"></span><span id="_______SERVERID______"></span>*ServerID*   
指定调试服务器的 ID。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

仅当通过调试器执行远程调试时，才能使用此命令。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>交货</strong></p></td>
<td align="left"><p>仅用户模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>实时，故障转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>适用</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关远程调试的详细信息，请参阅[通过调试器进行远程调试](remote-debugging-through-the-debugger.md)。

<a name="remarks"></a>备注
-------

必须从调试服务器或连接到调试服务器的某个调试客户端发出**endsrv**命令。

若要确定调试服务器的 ID，请使用 "[**服务器（列表调试服务器）** ](-servers--list-debugging-servers-.md) " 命令。

**Endsrv**命令可以终止调试服务器，但不能终止进程服务器或 KD 连接服务器。 有关如何结束这些服务器的信息，请参阅[控制进程服务器会话](controlling-a-process-server-session.md)和[控制 KD 连接服务器会话](controlling-a-kd-connection-server-session.md)。 （但是，在这种情况下， **endsrv**可以结束以编程方式启动的进程服务器; 有关详细信息，请参阅[**IDebugClient：： StartProcessServer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-startprocessserver)。）

如果取消调试服务器，则会阻止任何将来的调试客户端附加到服务器。 但是，如果取消调试服务器，则不会分离当前通过该服务器连接的任何客户端。

请考虑以下情况。 假设您开始一些调试服务器，如以下示例所示。

```dbgcmd
0:000> .server npipe:pipe=rabbit
Server started with 'npipe:pipe=rabbit'
0:000> .server tcp:port=7
Server started with 'tcp:port=7'
```

然后，你决定使用密码，如下面的示例所示。

```dbgcmd
0:000> .server npipe:pipe=tiger,password=hardtoguess
Server started with 'npipe:pipe=tiger,password=hardtoguess'
```

但以前的服务器仍在运行，因此应将其取消，如以下示例所示。

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

最后，为了确保在较早的服务器处于活动状态时，未将任何内容附加到计算机，请使用 "[**客户端（列表调试客户端）** ](-clients--list-debugging-clients-.md) " 命令。

```dbgcmd
0:000> .clients
HotMachine\HostUser, last active Mon Mar 04 16:05:21 2002
```

**警告**   使用带有 TCP、NPIPE 或 COM 协议的密码仅提供少量保护，因为密码未加密。 将密码与 SSL 或 SPIPE 协议一起使用时，会对密码进行加密。 如果要建立安全远程会话，则必须使用 SSL 或 SPIPE 协议。

 

 

 





