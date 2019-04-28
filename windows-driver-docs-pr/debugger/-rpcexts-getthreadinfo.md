---
title: rpcexts.getthreadinfo
description: Rpcexts.getthreadinfo 扩展搜索线程信息的系统的 RPC 状态信息。
ms.assetid: 904605e7-c53b-4e29-874f-7a055fc7a02b
keywords:
- rpcexts.getthreadinfo Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- rpcexts.getthreadinfo
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ff41bcd6c0440acac8105aeea45fcc5c63a4026f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63338851"
---
# <a name="rpcextsgetthreadinfo"></a>!rpcexts.getthreadinfo


**！ Rpcexts.getthreadinfo**扩展搜索线程信息的系统的 RPC 状态信息。

```dbgcmd
!rpcexts.getthreadinfo ProcessID [ThreadID] 
!rpcexts.getthreadinfo -? 
```

## <a name="span-idddkrpcextsgetthreadinfodbgspanspan-idddkrpcextsgetthreadinfodbgspanparameters"></a><span id="ddk__rpcexts_getthreadinfo_dbg"></span><span id="DDK__RPCEXTS_GETTHREADINFO_DBG"></span>参数


<span id="_______ProcessID______"></span><span id="_______processid______"></span><span id="_______PROCESSID______"></span> *ProcessID*   
指定的进程 ID (PID) 包含所需的线程的进程。

<span id="_______ThreadID______"></span><span id="_______threadid______"></span><span id="_______THREADID______"></span> *ThreadID*   
指定要显示线程的线程 ID。 如果省略，将显示指定的进程中的所有线程。

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
0:002> !rpcexts.getthreadinfo 26c
Searching for thread info ...
## PID  CELL ID   ST TID      LASTTIME
-----------------------------------
026c 0000.0002 01 000003c4 0004caa5
026c 0000.0005 03 00000254 0004ca9b
```

有关使用 DbgRpc 工具的类似示例，请参阅[获取 RPC 线程信息](get-rpc-thread-information.md)。

 

 





