---
title: rpcexts.thread
description: Rpcexts.thread 扩展显示的每个线程 RPC 信息。此扩展命令不应与.thread 命令混淆。
ms.assetid: eecc4eb6-7789-47ed-8b3f-5ec21cc6117c
keywords:
- rpcexts.thread Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- rpcexts.thread
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: fe1b069d044f2e5c518c7d3d91fe47613ffa94fe
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63338849"
---
# <a name="rpcextsthread"></a>!rpcexts.thread


**！ Rpcexts.thread**扩展显示的每个线程 RPC 信息。

不要将此扩展命令与相混淆[ **.thread （设置注册上下文）** ](-thread--set-register-context-.md)命令或[ **！ 线程**](-thread.md) （！kdextx86.thread 和 ！ kdexts.thread) 扩展。

```dbgcmd
!rpcexts.thread TEB
```

## <a name="span-idddkrpcextsthreaddbgspanspan-idddkrpcextsthreaddbgspanparameters"></a><span id="ddk__rpcexts_thread_dbg"></span><span id="DDK__RPCEXTS_THREAD_DBG"></span>参数


<span id="_______TEB______"></span><span id="_______teb______"></span> *TEB*   
指定的线程环境块 (TEB) 的地址。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

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

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关调试 Microsoft 远程过程调用 (RPC) 的详细信息，请参阅[RPC 调试](rpc-debugging.md)。

<a name="remarks"></a>备注
-------

此扩展显示的每个线程 RPC 信息。 中的每个线程 RPC 信息的字段是此线程的扩展的错误信息。

下面是一个示例：

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

 

 





