---
title: rpcexts
description: Rpcexts 扩展显示每个线程的 RPC 信息。不应将此扩展命令与 thread 命令混淆。
keywords:
- rpcexts Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- rpcexts.thread
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1f3fb7dc82549a813598cf30e482052608ca45c2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837019"
---
# <a name="rpcextsthread"></a>!rpcexts.thread


**！ Rpcexts** 扩展显示每个线程的 RPC 信息。

不应将此扩展命令与 [**. thread (设置 Register Context)**](-thread--set-register-context-.md) 命令或 [**！ thread**](-thread.md) (！ kdexts) 扩展。

```dbgcmd
!rpcexts.thread TEB
```

## <a name="span-idddk__rpcexts_thread_dbgspanspan-idddk__rpcexts_thread_dbgspanparameters"></a><span id="ddk__rpcexts_thread_dbg"></span><span id="DDK__RPCEXTS_THREAD_DBG"></span>参数


<span id="_______TEB______"></span><span id="_______teb______"></span>*TEB*   
指定线程环境块 (TEB) 的地址。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Rpcexts.dll</p></td>
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

此扩展显示每个线程的 RPC 信息。 每个线程的 RPC 信息中的字段是此线程的扩展错误信息。

以下是示例：

```dbgcmd
0:001> !rpcexts.thread 7ffdd000
RPC TLS at 692e70

HandleToThread - 0x6c
SavedProcedure - 0x0
SavedParameter - 0x0
ActiveCall - 0x0
Context - 0x0
CancelTimeout - 0xffffffff
SecurityContext - 0x0
ExtendedStatus - 0x0
ThreadEEInfo - 0xb015f0
ThreadEvent at - 0x00692E78
fCallCancelled - 0x0
buffer cache array at - 0x00692E84
fAsync - 0x0
```

 

 





