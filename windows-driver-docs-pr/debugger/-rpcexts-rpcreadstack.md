---
title: rpcexts.rpcreadstack
description: Rpcexts. rpcreadstack 扩展读取 RPC 客户端堆栈并检索调用信息。
keywords:
- rpcexts rpcreadstack Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- rpcexts.rpcreadstack
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 053e0575cbdd8e5da9a8910cedebf586165b0eba
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96821001"
---
# <a name="rpcextsrpcreadstack"></a>!rpcexts.rpcreadstack


**！ Rpcexts rpcreadstack** 扩展读取 RPC 客户端堆栈并检索调用信息。

```dbgcmd
!rpcexts.rpcreadstack ThreadStackPointer
```

## <a name="span-idddk__rpcexts_rpcreadstack_dbgspanspan-idddk__rpcexts_rpcreadstack_dbgspanparameters"></a><span id="ddk__rpcexts_rpcreadstack_dbg"></span><span id="DDK__RPCEXTS_RPCREADSTACK_DBG"></span>参数


<span id="_______ThreadStackPointer______"></span><span id="_______threadstackpointer______"></span><span id="_______THREADSTACKPOINTER______"></span>*ThreadStackPointer*   
指定指向线程堆栈的指针。

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

有关此扩展的常见用法，请参阅 [分析停滞调用问题](analyzing-a-stuck-call-problem.md)。

以下是示例：

```dbgcmd
0:001> !rpcexts.rpcreadstack 68fba4
CallID: 1
IfStart: 19bb5061
ProcNum: 0
        Protocol Sequence:      "ncacn_ip_tcp"  (Address: 00692ED8)
        NetworkAddress: ""      (Address: 00692F38)
        Endpoint:       "1120"  (Address: 00693988)
```

 

 





