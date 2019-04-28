---
title: rpcexts.eeinfo
description: Rpcexts.eeinfo 扩展显示的扩展的错误的信息链。
ms.assetid: dc842236-bdbf-42aa-911d-6eb5eb1798ee
keywords:
- rpcexts.eeinfo Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- rpcexts.eeinfo
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b407313efbc22b1c1cc60249a9856443679384f7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63338896"
---
# <a name="rpcextseeinfo"></a>!rpcexts.eeinfo


**！ Rpcexts.eeinfo**扩展显示的扩展的错误的信息链。

```dbgcmd
!rpcexts.eeinfo EEInfoAddress
```

## <a name="span-idddkrpcextseeinfodbgspanspan-idddkrpcextseeinfodbgspanparameters"></a><span id="ddk__rpcexts_eeinfo_dbg"></span><span id="DDK__RPCEXTS_EEINFO_DBG"></span>参数


<span id="_______EEInfoAddress______"></span><span id="_______eeinfoaddress______"></span><span id="_______EEINFOADDRESS______"></span> *EEInfoAddress*   
指定的扩展的错误消息的地址。

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

此扩展显示扩展的错误的信息链中的所有记录的内容。

首先按顺序，使用最新的记录显示记录。 记录由一系列短划线分隔。

下面是的示例 （在其中不存在只有一条记录）：

```dbgcmd
0:001> !rpcexts.eeinfo 0xb015f0
Computer Name: (null)
ProcessID: 708 (0x2C4)
System Time is: 3/21/2000 4:3:0:264
Generating component: 8
Status: 14
Detection Location: 311
Flags:
Parameter 0:(Long value) : -30976 (0xFFFF8700)
Parameter 1:(Long value) : 16777343 (0x100007F)
```

如果链是很长，并且你想要看到只有一个记录，使用[ **！ rpcexts.eerecord** ](-rpcexts-eerecord.md)相反。

 

 





