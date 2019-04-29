---
title: 关键节超时
description: 关键节超时
ms.assetid: 736ec6e9-e822-49aa-8f1c-7e5e43779dbd
keywords:
- 关键部分中，调试临界区的超时
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 90563b4284a138aae520e14b6da72bf2e82d90a2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374439"
---
# <a name="critical-section-time-outs"></a>关键节超时


## <span id="ddk_critical_section_time_outs_dbg"></span><span id="DDK_CRITICAL_SECTION_TIME_OUTS_DBG"></span>


可以通过显示例程的堆栈跟踪标识关键部分的超时**RtlpWaitForCriticalSection**堆栈顶部附近。 另一个不同的关键部分超时是可能的死锁的应用程序错误。 若要正确地调试临界区的超时，CDB 或 WinDbg 是必需的。

与资源的超时，一样 **！ ntsdexts.locks**扩展将提供当前持有的锁和他们自己的线程的列表。 与不同资源的超时，给定的线程 Id 不是立即有用的。 这些是系统不会映射到使用 CDB 的线程号直接的 Id。

正如使用<strong>ExpWaitForResource * Xxx</strong><em>，锁定标识符是第一个参数 **RtlpWaitForCriticalSection</em>*。 继续跟踪在一系列等待，直到找到一个循环或最后一个线程不会等待关键节超时。

### <a name="span-idexampleofdebuggingacriticaltimeoutspanspan-idexampleofdebuggingacriticaltimeoutspanexample-of-debugging-a-critical-time-out"></a><span id="example_of_debugging_a_critical_time_out"></span><span id="EXAMPLE_OF_DEBUGGING_A_CRITICAL_TIME_OUT"></span>示例中的调试关键超时

首先显示的堆栈：

```dbgcmd
0:024> kb

ChildEBP RetAddr  Args to Child
0569fca4 77f79c78 77f71000 002a6b88 7fffffff ntdll!_DbgBreakPoint
0569fd04 77f71048 5ffa9f9c 5fef0b4b 5ffa9f9c ntdll!_RtlpWaitForCriticalSection+0x89
0569fd0c 5fef0b4b 5ffa9f9c 002a6b88 002a0019 ntdll!_RtlEnterCriticalSection+0x48
0569fd70 5fedf83f 002a6b88 0569fdc0 0000003e winsrv!_StreamScrollRegion+0x1f0
0569fd8c 5fedfa5b 002a6b88 00190000 00000000 winsrv!_AdjustCursorPosition+0x8e
0569fdc0 5fedf678 0569ff18 0031c200 0335ee88 winsrv!_DoWriteConsole+0x104

0569fefc 5fe6311b 0569ff18 0569ffd0 00000005 winsrv!_SrvWriteConsole+0x96
0569fff4 00000000 00000000 00000024 00000024 csrsrv!_CsrApiRequestThread+0x4ff 
```

现在，使用[ **！ ntsdexts.locks** ](-locks---ntsdexts-locks-.md)要查找的关键部分的扩展名：

```dbgcmd
0:024> !locks 
CritSec winsrv!_ScrollBufferLock at 5ffa9f9c        5ffa9f9c is the first one 
LockCount          5
RecursionCount     1
OwningThread       88         // here's the owning thread ID 
EntryCount         11c
ContentionCount    135
*** Locked

CritSec winsrv!_gcsUserSrv+0 at 5ffa91b4     //second critical section found below 

LockCount          8
RecursionCount     1
OwningThread       6d         // second owning thread 
EntryCount         1d6c
ContentionCount    1d47
*** Locked 
```

现在搜索具有的 ID 号 0x6D 的线程：

```dbgcmd
0:024> ~ 
  0  id: 16.15   Teb 7ffdd000 Unfrozen
  1  id: 16.13   Teb 7ffdb000 Unfrozen
  2  id: 16.30   Teb 7ffda000 Unfrozen
  3  id: 16.2f   Teb 7ffd9000 Unfrozen
  4  id: 16.2e   Teb 7ffd8000 Unfrozen
  5  id: 16.6c   Teb 7ff6c000 Unfrozen
  6  id: 16.6d   Teb 7ff68000 Unfrozen    // this thread owns the second critical section
  7  id: 16.2d   Teb 7ffd7000 Unfrozen
  8  id: 16.33   Teb 7ffd6000 Unfrozen
  9  id: 16.42   Teb 7ff6f000 Unfrozen
 10  id: 16.6f   Teb 7ff6e000 Unfrozen
 11  id: 16.6e   Teb 7ffd5000 Unfrozen
 12  id: 16.52   Teb 7ff6b000 Unfrozen
 13  id: 16.61   Teb 7ff6a000 Unfrozen
 14  id: 16.7e   Teb 7ff69000 Unfrozen
 15  id: 16.43   Teb 7ff67000 Unfrozen
 16  id: 16.89   Teb 7ff50000 Unfrozen
 17  id: 16.95   Teb 7ff65000 Unfrozen
 18  id: 16.90   Teb 7ff64000 Unfrozen
 19  id: 16.71   Teb 7ff63000 Unfrozen
 20  id: 16.bb   Teb 7ff62000 Unfrozen
 21  id: 16.88   Teb 7ff61000 Unfrozen    // this thread owns the first critical section
 22  id: 16.cd   Teb 7ff5e000 Unfrozen
 23  id: 16.c1   Teb 7ff5f000 Unfrozen
 24  id: 16.bd   Teb 7ff5d000 Unfrozen 
```

线程 21 拥有第一个关键部分。 确保在活动线程，并获取堆栈跟踪：

```dbgcmd
0:024> ~21s
ntdll!_ZwWaitForSingleObject+0xb:
77f71bfb c20c00           ret     0xc

0:021> kb

ChildEBP RetAddr  Args to Child
0556fc44 77f79c20 00000110 00000000 77fa4700 ntdll!_ZwWaitForSingleObject+0xb
0556fcb0 77f71048 5ffa91b4 5feb4f7e 5ffa91b4 ntdll!_RtlpWaitForCriticalSection+0x31
0556fcb8 5feb4f7e 5ffa91b4 0556fd70 77f71000 ntdll!_RtlEnterCriticalSection+0x48
0556fcf4 5fef0b76 01302005 00000000 fffffff4 winsrv!__ScrollDC+0x14
0556fd70 5fedf83f 002bd880 0556fdc0 00000025 winsrv!_StreamScrollRegion+0x21b
0556fd8c 5fedfa5b 002bd880 00190000 00000000 winsrv!_AdjustCursorPosition+0x8e

0556fdc0 5fedf678 0556ff18 002bdf70 002a4d58 winsrv!_DoWriteConsole+0x104
0556fefc 5fe6311b 0556ff18 0556ffd0 00000005 winsrv!_SrvWriteConsole+0x96
0556fff4 00000000 00000000 00000024 00000024 csrsrv!_CsrApiRequestThread+0x4ff 
```

线程 6 拥有第二个关键部分。 检查以及其堆栈：

```dbgcmd
0:021> ~6s
winsrv!_PtiFromThreadId+0xd:
5fe8429a 394858           cmp     [eax+0x58],ecx    ds:0023:7f504da8=000000f8

0:006> kb

ChildEBP RetAddr  Args to Child
01ecfeb4 5fecd0d7 00000086 00000000 7f5738e0 winsrv!_PtiFromThreadId+0xd
01ecfed0 5feccf62 00000086 01ecfff4 00000113 winsrv!__GetThreadDesktop+0x12
01ecfefc 5fe6311b 01ecff18 01ecffd0 00000005 winsrv!___GetThreadDesktop+0x8b
01ecfff4 00000000 00000000 00000024 00000024 csrsrv!_CsrApiRequestThread+0x4ff 
```

线程 21 **RtlpWaitForCriticalSection**其堆栈顶部附近。 线程 6 却没有。 使线程 21 是问题所在。

 

 





