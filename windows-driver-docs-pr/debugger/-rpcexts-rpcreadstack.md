---
title: rpcexts.rpcreadstack
description: Rpcexts.rpcreadstack 扩展读取 RPC 客户端的堆栈，并检索调用信息。
ms.assetid: e0988ac9-dc6e-4a4f-9096-6af2e70dcd42
keywords:
- rpcexts.rpcreadstack Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- rpcexts.rpcreadstack
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b0f586e84621a94a5472151c447b115307869fd4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562481"
---
# <a name="rpcextsrpcreadstack"></a>!rpcexts.rpcreadstack


**！ Rpcexts.rpcreadstack**扩展读取 RPC 客户端的堆栈，并检索调用信息。

```dbgcmd
!rpcexts.rpcreadstack ThreadStackPointer
```

## <a name="span-idddkrpcextsrpcreadstackdbgspanspan-idddkrpcextsrpcreadstackdbgspanparameters"></a><span id="ddk__rpcexts_rpcreadstack_dbg"></span><span id="DDK__RPCEXTS_RPCREADSTACK_DBG"></span>参数


<span id="_______ThreadStackPointer______"></span><span id="_______threadstackpointer______"></span><span id="_______THREADSTACKPOINTER______"></span> *ThreadStackPointer*   
指定指向线程堆栈指针。

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

此扩展的一个常见用途，请参阅[分析停滞调用问题](analyzing-a-stuck-call-problem.md)。

下面是一个示例：

```dbgcmd
0:001> !rpcexts.rpcreadstack 68fba4
CallID: 1
IfStart: 19bb5061
ProcNum: 0
        Protocol Sequence:      "ncacn_ip_tcp"  (Address: 00692ED8)
        NetworkAddress: ""      (Address: 00692F38)
        Endpoint:       "1120"  (Address: 00693988)
```

 

 





