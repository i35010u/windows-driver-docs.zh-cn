---
title: rpcexts.getdbgcell
description: Rpcexts.getdbgcell 扩展显示指定的单元格的 RPC 状态信息。
ms.assetid: 28be074f-6756-4610-aa86-1162b83fd0a7
keywords:
- rpcexts.getdbgcell Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- rpcexts.getdbgcell
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 2e95847021c0f8c860a3c55e875be357e9e3b3cf
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56540961"
---
# <a name="rpcextsgetdbgcell"></a>!rpcexts.getdbgcell


**！ Rpcexts.getdbgcell**扩展显示指定的单元格的 RPC 状态信息。

```dbgcmd
!rpcexts.getdbgcell ProcessID CellID1.CellID2 
!rpcexts.getdbgcell -?
```

## <a name="span-idddkrpcextsgetdbgcelldbgspanspan-idddkrpcextsgetdbgcelldbgspanparameters"></a><span id="ddk__rpcexts_getdbgcell_dbg"></span><span id="DDK__RPCEXTS_GETDBGCELL_DBG"></span>参数


<span id="_______ProcessID______"></span><span id="_______processid______"></span><span id="_______PROCESSID______"></span> *ProcessID*   
指定的进程 ID (PID) 的服务器包含所需单元格的过程。

<span id="_______cellid1.cellid2______"></span><span id="_______CELLID1.CELLID2______"></span> *CellID1*.*CellID2*   
指定要显示的单元格的数量。

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
0:002> !rpcexts.getdbgcell c4 0.19
Getting cell info ...
Call
Status: Active
Procedure Number: 11
Interface UUID start (first DWORD only): 82273FDC
Call ID: 0x0 (0)
Servicing thread identifier: 0x0.3E
Call Flags: cached, LRPC
Last update time (in seconds since boot):1453.459 (0x5AD.1CB)
Caller (PID/TID) is: d0.1ac (208.428)
```

有关使用 DbgRpc 工具的类似示例，请参阅[获取 RPC 单元格信息](get-rpc-cell-information.md)。

 

 





