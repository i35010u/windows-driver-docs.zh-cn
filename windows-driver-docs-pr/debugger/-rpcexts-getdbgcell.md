---
title: rpcexts.getdbgcell
description: Rpcexts. getdbgcell 扩展显示指定单元的 RPC 状态信息。
keywords:
- rpcexts getdbgcell Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- rpcexts.getdbgcell
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1bdc33470af22ebc35d5931a2f012fe87ca4f127
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96795181"
---
# <a name="rpcextsgetdbgcell"></a>!rpcexts.getdbgcell


**！ Rpcexts getdbgcell** 扩展显示指定单元的 RPC 状态信息。

```dbgcmd
!rpcexts.getdbgcell ProcessID CellID1.CellID2 
!rpcexts.getdbgcell -?
```

## <a name="span-idddk__rpcexts_getdbgcell_dbgspanspan-idddk__rpcexts_getdbgcell_dbgspanparameters"></a><span id="ddk__rpcexts_getdbgcell_dbg"></span><span id="DDK__RPCEXTS_GETDBGCELL_DBG"></span>参数


<span id="_______ProcessID______"></span><span id="_______processid______"></span><span id="_______PROCESSID______"></span>*ProcessID*   
指定进程的进程 ID (PID) ，其服务器包含所需的单元格。

<span id="_______cellid1.cellid2______"></span><span id="_______CELLID1.CELLID2______"></span>*CellID1*。*CellID2*   
指定要显示的单元格的编号。

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

有关使用 DbgRpc 工具的类似示例，请参阅 [获取 RPC 单元信息](get-rpc-cell-information.md)。

 

 





