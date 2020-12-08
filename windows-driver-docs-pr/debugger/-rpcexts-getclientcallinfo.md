---
title: rpcexts.getclientcallinfo
description: Rpcexts getclientcallinfo 扩展在系统的 RPC 状态信息中搜索客户端调用 (CCALL) 信息。
keywords:
- rpcexts getclientcallinfo Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- rpcexts.getclientcallinfo
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: fe82bdff13fe5f396e2d750fa002696e1e9a41ad
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96795187"
---
# <a name="rpcextsgetclientcallinfo"></a>!rpcexts.getclientcallinfo


**！ Rpcexts getclientcallinfo** 扩展在系统的 RPC 状态信息中搜索客户端调用 (CCALL) 信息。

```dbgcmd
!rpcexts.getclientcallinfo [ CallID | 0 [ IfStart | 0 [ ProcNum | 0xFFFF [ProcessID|0] ] ] ] 
!rpcexts.getclientcallinfo -? 
```

## <a name="span-idddk__rpcexts_getclientcallinfo_dbgspanspan-idddk__rpcexts_getclientcallinfo_dbgspanparameters"></a><span id="ddk__rpcexts_getclientcallinfo_dbg"></span><span id="DDK__RPCEXTS_GETCLIENTCALLINFO_DBG"></span>参数


<span id="_______CallID______"></span><span id="_______callid______"></span><span id="_______CALLID______"></span>*CallID*   
指定呼叫 ID。 此参数是可选的;如果只想显示与特定 *CallID* 值匹配的调用，请将其包含在内。

<span id="_______IfStart______"></span><span id="_______ifstart______"></span><span id="_______IFSTART______"></span>*IfStart*   
指定在其上进行调用的接口 UUID 的第一个 DWORD。 此参数是可选的;如果只想显示与特定 *IfStart* 值匹配的调用，请将其包含在内。

<span id="_______ProcNum______"></span><span id="_______procnum______"></span><span id="_______PROCNUM______"></span>*ProcNum*   
指定此调用的过程号。 RPC Run-Time (RPC 通过在 IDL 文件中的位置对其进行编号来标识接口中的各个例程，接口中的第一个例程为0，第二个例程为1，依此类推。 ) 此参数是可选的;如果只想显示与特定 *ProcNum* 值匹配的调用，请将其包含在内。

<span id="_______ProcessID______"></span><span id="_______processid______"></span><span id="_______PROCESSID______"></span>*ProcessID*   
指定拥有要显示的调用的客户端进程 (PID) 的进程 ID。 此参数是可选的;如果要显示多个进程所拥有的调用，则省略它。

<span id="_______-_______"></span> **-?**   
在命令提示符窗口中显示此扩展的一些简短帮助文本。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

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

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关调试 Microsoft 远程过程调用 (RPC) 的详细信息，请参阅 [Rpc 调试](rpc-debugging.md)。

<a name="remarks"></a>备注
-------

此扩展只能与 CDB 一起使用，也可与用户模式 WinDbg 一起使用。 仅当收集完整的 RPC 状态信息时，它才可用。

以下是示例：

```dbgcmd
0:002> !rpcexts.getclientcallinfo
Searching for call info ...
## PID  CELL ID   PNO  IFSTART  TIDNUMBER CALLID   LASTTIME PS CLTNUMBER ENDPOINT
------------------------------------------------------------------------------
03d4 0000.0001 0000 19bb5061 0000.0000 00000001 0004ca9b 07 0000.0002 1118
```

有关使用 DbgRpc 工具的类似示例，请参阅 [获取 RPC 客户端调用信息](get-rpc-client-call-information.md)。

 

 





