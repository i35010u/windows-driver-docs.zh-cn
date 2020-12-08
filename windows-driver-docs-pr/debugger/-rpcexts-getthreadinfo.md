---
title: rpcexts. getthreadinfo
description: Rpcexts. getthreadinfo 扩展会在系统的 RPC 状态信息中搜索线程信息。
keywords:
- rpcexts getthreadinfo Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- rpcexts.getthreadinfo
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 98bd8ef537b39993ada81127dcc8e3e78cde57f6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96787031"
---
# <a name="rpcextsgetthreadinfo"></a>!rpcexts.getthreadinfo


**！ Rpcexts getthreadinfo** 扩展会在系统的 RPC 状态信息中搜索线程信息。

```dbgcmd
!rpcexts.getthreadinfo ProcessID [ThreadID] 
!rpcexts.getthreadinfo -? 
```

## <a name="span-idddk__rpcexts_getthreadinfo_dbgspanspan-idddk__rpcexts_getthreadinfo_dbgspanparameters"></a><span id="ddk__rpcexts_getthreadinfo_dbg"></span><span id="DDK__RPCEXTS_GETTHREADINFO_DBG"></span>参数


<span id="_______ProcessID______"></span><span id="_______processid______"></span><span id="_______PROCESSID______"></span>*ProcessID*   
指定包含所需线程的进程的进程 ID (PID) 。

<span id="_______ThreadID______"></span><span id="_______threadid______"></span><span id="_______THREADID______"></span>*ThreadID*   
指定要显示的线程的线程 ID。 如果省略，则将显示指定进程中的所有线程。

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

此扩展只能与 CDB 一起使用，也可与用户模式 WinDbg 一起使用。

以下是示例：

```dbgcmd
0:002> !rpcexts.getthreadinfo 26c
Searching for thread info ...
## PID  CELL ID   ST TID      LASTTIME
-----------------------------------
026c 0000.0002 01 000003c4 0004caa5
026c 0000.0005 03 00000254 0004ca9b
```

有关使用 DbgRpc 工具的类似示例，请参阅 [获取 RPC 线程信息](get-rpc-thread-information.md)。

 

 





