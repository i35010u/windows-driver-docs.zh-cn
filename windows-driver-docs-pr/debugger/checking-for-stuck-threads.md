---
title: 检查线程阻塞问题
description: 检查线程阻塞问题
keywords:
- RPC 调试，阻塞的线程
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: f6626545fb8ee4c6f8ca74ab544abc40f74ff5fd
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96821611"
---
# <a name="checking-for-stuck-threads"></a>检查线程阻塞问题


## <span id="ddk_checking_for_stuck_threads_dbg"></span><span id="DDK_CHECKING_FOR_STUCK_THREADS_DBG"></span>


RPC 需要其工作线程可用才能正常执行。 一个常见的问题是，同一进程中的某些组件会死锁，同时保存其中一个全局关键部分 (例如，加载程序锁或堆锁定) 。 这会导致很多线程挂起-很可能包括一些 RPC 工作线程。

如果出现这种情况，RPC 服务器将不会响应外界。 RPC 对它的调用将返回 RPC \_ s \_ 服务器 \_ 不可用或 rpc \_ s \_ 服务器 \_ 过于 \_ 繁忙。

如果出现故障的驱动程序阻止 Irp 完成并到达 RPC 服务器，则可能会产生类似的问题。

如果怀疑可能会出现这些问题之一，请将 DbgRpc 与 **-t** 开关一起使用 (或使用 [**！ rpcexts getthreadinfo**](-rpcexts-getthreadinfo.md) 扩展) 。 进程 ID 应用作参数。 在下面的示例中，假定进程 ID 为0xC4：

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

TID 列提供每个线程的线程 ID。 LASTTIME 列包含每个线程的上次状态更改的时间戳。

每当服务器收到请求时，至少一个线程将更改状态，并且将更新其时间戳。 因此，如果对服务器发出 RPC 请求，但请求失败但没有时间戳发生更改，则表示该请求实际上不会到达 RPC 运行时。 应调查此问题的原因。

 

 





