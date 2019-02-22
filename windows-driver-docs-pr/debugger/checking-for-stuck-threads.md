---
title: 检查卡滞线程
description: 检查卡滞线程
ms.assetid: ffb1ff13-fc4c-4aaf-a8fe-b473b51b9db0
keywords:
- RPC 调试，受阻的线程
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 39db2ef7eb8143fd4d44a7ea384403bea7302eb6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544021"
---
# <a name="checking-for-stuck-threads"></a>检查卡滞线程


## <span id="ddk_checking_for_stuck_threads_dbg"></span><span id="DDK_CHECKING_FOR_STUCK_THREADS_DBG"></span>


RPC 必须可用才能正常执行其工作线程。 一个常见问题是在同一进程中的某个组件将死锁时包含一个全局临界区 （例如，加载程序锁或锁定的堆）。 这将导致多个线程处于挂起状态-很可能包括一些 RPC 工作线程。

如果发生这种情况，不会向外界响应 RPC 服务器。 RPC 调用将返回 RPC\_S\_服务器\_不可用或 RPC\_S\_SERVER\_过\_忙。

如果发生故障的驱动程序，使 Irp 无法完成，并且达到 RPC 服务器可能会导致类似问题。

如果你怀疑可能出现这些问题之一，使用与 DbgRpc **-t**切换 (或使用[ **！ rpcexts.getthreadinfo** ](-rpcexts-getthreadinfo.md)扩展)。 应作为参数使用的进程 ID。 在以下示例中，假定的进程 ID 是 0xC4:

```dbgcmd
D:\wmsg>dbgrpc -t -P c4
Searching for thread info ...
## PID  CELL ID   ST TID      LASTTIME
-----------------------------------
00c4 0000.0004 03 0000011c 000f164f
00c4 0000.0007 03 00000120 008a6290
00c4 0000.0015 03 0000018c 008a6236
00c4 0000.0026 03 00000264 0005c443
00c4 0000.002d 03 00000268 000265bb
00c4 0000.0030 03 0000026c 000f1d32
00c4 0000.0034 03 00000388 007251e9
```

TID 列给出每个线程的线程 ID。 LASTTIME 列包含每个线程的状态的最后一个更改的时间戳。

每当在服务器收到请求时，至少一个线程将更改状态，并将更新其时间戳。 因此，如果对服务器进行 RPC 请求和请求失败，但无时间戳更改，则表明该请求实际上达不到 RPC 运行时。 应调查的原因。

 

 





