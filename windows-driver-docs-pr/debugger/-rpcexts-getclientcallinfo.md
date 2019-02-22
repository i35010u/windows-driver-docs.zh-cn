---
title: rpcexts.getclientcallinfo
description: Rpcexts.getclientcallinfo 扩展搜索客户端调用 (CCALL) 信息系统的 RPC 状态信息。
ms.assetid: 1b838238-63b3-4618-bc59-6b4d74274b9c
keywords:
- rpcexts.getclientcallinfo Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- rpcexts.getclientcallinfo
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e14d7d01bedc1543b1303f8494324e38e36933da
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544160"
---
# <a name="rpcextsgetclientcallinfo"></a>!rpcexts.getclientcallinfo


**！ Rpcexts.getclientcallinfo**扩展搜索客户端调用 (CCALL) 信息系统的 RPC 状态信息。

```dbgcmd
!rpcexts.getclientcallinfo [ CallID | 0 [ IfStart | 0 [ ProcNum | 0xFFFF [ProcessID|0] ] ] ] 
!rpcexts.getclientcallinfo -? 
```

## <a name="span-idddkrpcextsgetclientcallinfodbgspanspan-idddkrpcextsgetclientcallinfodbgspanparameters"></a><span id="ddk__rpcexts_getclientcallinfo_dbg"></span><span id="DDK__RPCEXTS_GETCLIENTCALLINFO_DBG"></span>参数


<span id="_______CallID______"></span><span id="_______callid______"></span><span id="_______CALLID______"></span> *CallID*   
指定调用 id。 此参数是可选的;如果只想要显示匹配特定的调用将其包含*CallID*值。

<span id="_______IfStart______"></span><span id="_______ifstart______"></span><span id="_______IFSTART______"></span> *IfStart*   
指定接口 UUID 执行调用的第一个 dword 值。 此参数是可选的;如果只想要显示匹配特定的调用将其包含*IfStart*值。

<span id="_______ProcNum______"></span><span id="_______procnum______"></span><span id="_______PROCNUM______"></span> *ProcNum*   
指定此调用的过程数。 （RPC 运行时按编号的 IDL 文件中的位置标识接口中的单个例程--在界面中的第一个例程是 0，第二个 1，依此类推。）此参数是可选的;如果只想要显示匹配特定的调用将其包含*ProcNum*值。

<span id="_______ProcessID______"></span><span id="_______processid______"></span><span id="_______PROCESSID______"></span> *ProcessID*   
指定的进程 ID (PID) 拥有想要显示的调用的客户端过程。 此参数是可选的;如果你想要显示调用所拥有的多个进程，则省略此参数。

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

与 CDB 或用户模式下 WinDbg，则仅可以使用此扩展。 如果在收集完整的 RPC 状态信息，才可用。

下面是一个示例：

```dbgcmd
0:002> !rpcexts.getclientcallinfo
Searching for call info ...
## PID  CELL ID   PNO  IFSTART  TIDNUMBER CALLID   LASTTIME PS CLTNUMBER ENDPOINT
------------------------------------------------------------------------------
03d4 0000.0001 0000 19bb5061 0000.0000 00000001 0004ca9b 07 0000.0002 1118
```

有关使用 DbgRpc 工具的类似示例，请参阅[获取 RPC 客户端调用信息](get-rpc-client-call-information.md)。

 

 





