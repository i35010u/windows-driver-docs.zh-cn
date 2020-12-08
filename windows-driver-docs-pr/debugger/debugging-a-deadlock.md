---
title: 调试死锁
description: 调试死锁
keywords:
- 死锁
- 线程，无就绪线程
ms.date: 06/10/2017
ms.localizationpriority: medium
ms.openlocfilehash: d13901df5c53334c2007384a97e66cd5ed9aca84
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96813295"
---
# <a name="debugging-a-deadlock"></a>调试死锁

## <span id="ddk_debugging_deadlocks_no_ready_threads__dbg"></span><span id="DDK_DEBUGGING_DEADLOCKS_NO_READY_THREADS__DBG"></span>

当线程需要独占访问代码或某个其他资源时，它会请求一个 *锁*。 如果可以，Windows 将通过向线程提供此锁来做出响应。 此时，系统中的任何其他内容都无法访问锁定的代码。 这种情况一直发生，并且是任何编写良好的多线程应用程序的正常部分。 尽管特定代码段一次只能有一个锁，但每个代码段都可以有自己的锁。

当两个或多个线程在两个或更多资源上以不兼容的顺序请求锁时，会发生 *死锁* 。 例如，假设线程1已获取资源 A 的锁，然后请求对资源 B 的访问。同时，线程2已获取资源 B 的锁，然后请求对资源 A 的访问权限。在另一个线程的锁为释放的情况下，两个线程都无法继续，因此，这两个线程都不能继续。

当多个线程（通常是单个应用程序）互相阻止访问同一资源时，将出现用户模式死锁。 但是，多个应用程序的多个线程也可以彼此阻止对全局/共享资源的访问，例如全局事件或信号量。

当多个线程 (来自同一进程或不同进程) 彼此阻止彼此访问同一内核资源时，会出现内核模式死锁。

用于调试死锁的过程取决于死锁是在用户模式下还是在内核模式下发生。

### <a name="span-iddebugging_a_user_mode_deadlockspanspan-iddebugging_a_user_mode_deadlockspandebugging-a-user-mode-deadlock"></a><span id="debugging_a_user_mode_deadlock"></span><span id="DEBUGGING_A_USER_MODE_DEADLOCK"></span>调试 User-Mode 死锁

在用户模式下发生死锁时，请使用以下过程对其进行调试：

1. 发出 [**！ ntsdexts**](-locks---ntsdexts-locks-.md) extension。 在用户模式下，只需在调试器提示符下键入 **！锁** 即可;假定 **ntsdexts** 前缀。

2. 此扩展显示与当前进程关联的所有关键部分，以及所属线程的 ID 以及每个关键部分的锁计数。 如果临界区的锁计数为零，则它不会被锁定。 使用 [**~ (Thread Status)**](---thread-status-.md) 命令查看有关拥有其他关键部分的线程的信息。

3. 使用 kb (显示每个线程的 [**Stack Backtrace)**](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md) 命令，以确定它们是否正在等待其他关键部分。

4. 通过使用这些 **kb** 命令的输出，可以找到死锁：两个线程，每个线程都在等待另一个线程持有的锁。 在极少数情况下，死锁可能是由两个线程在循环模式下持有锁引起的，但大多数死锁只涉及两个线程。

下面是此过程的说明。 从 **！ ntdexts** 扩展开始：

```dbgcmd
0:006>  !locks 
CritSec ftpsvc2!g_csServiceEntryLock+0 at 6833dd68
LockCount          0
RecursionCount     1
OwningThread       a7
EntryCount         0
ContentionCount    0
**_ Locked

CritSec isatq!AtqActiveContextList+a8 at 68629100
LockCount          2
RecursionCount     1
OwningThread       a3
EntryCount         2
ContentionCount    2
_*_ Locked

CritSec +24e750 at 24e750
LockCount          6
RecursionCount     1
OwningThread       a9
EntryCount         6
ContentionCount    6
_*_ Locked
```

显示的第一个临界区没有锁定，因此可将其忽略。

显示的第二个关键部分的锁计数为2，因此可能导致死锁。 拥有线程的线程 ID 为0xA3。

可以通过以下方式找到此线程：列出具有 [_ *~ (线程状态)* *](---thread-status-.md)命令的所有线程，并查找具有此 ID 的线程：

```dbgcmd
0:006>  ~
   0  Id: 1364.1330 Suspend: 1 Teb: 7ffdf000 Unfrozen
   1  Id: 1364.17e0 Suspend: 1 Teb: 7ffde000 Unfrozen
   2  Id: 1364.135c Suspend: 1 Teb: 7ffdd000 Unfrozen
   3  Id: 1364.1790 Suspend: 1 Teb: 7ffdc000 Unfrozen
   4  Id: 1364.a3 Suspend: 1 Teb: 7ffdb000 Unfrozen
   5  Id: 1364.1278 Suspend: 1 Teb: 7ffda000 Unfrozen
.  6  Id: 1364.a9 Suspend: 1 Teb: 7ffd9000 Unfrozen
   7  Id: 1364.111c Suspend: 1 Teb: 7ffd8000 Unfrozen
   8  Id: 1364.1588 Suspend: 1 Teb: 7ffd7000 Unfrozen
```

在此显示中，第一项是调试器的内部线程号。 第二项 (`Id` 字段) 包含两个用小数点分隔的十六进制数字。 小数点前的数字是进程 ID;小数点后的数字是线程 ID。 在此示例中，你将看到线程 ID 0xA3 对应于线程号4。

然后，使用 [**kb (显示 Stack Backtrace)**](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md) 命令显示与线程号4相对应的堆栈：

```dbgcmd
0:006>  ~4 kb
  4  id: 97.a3   Suspend: 0 Teb 7ffd9000 Unfrozen
ChildEBP RetAddr  Args to Child
014cfe64 77f6cc7b 00000460 00000000 00000000 ntdll!NtWaitForSingleObject+0xb
014cfed8 77f67456 0024e750 6833adb8 0024e750 ntdll!RtlpWaitForCriticalSection+0xaa 
014cfee0 6833adb8 0024e750 80000000 01f21cb8 ntdll!RtlEnterCriticalSection+0x46
014cfef4 6833ad8f 01f21cb8 000a41f0 014cff20 ftpsvc2!DereferenceUserDataAndKill+0x24
014cff04 6833324a 01f21cb8 00000000 00000079 ftpsvc2!ProcessUserAsyncIoCompletion+0x2a
014cff20 68627260 01f21e0c 00000000 00000079 ftpsvc2!ProcessAtqCompletion+0x32
014cff40 686249a5 000a41f0 00000001 686290e8 isatq!I_TimeOutContext+0x87
014cff5c 68621ea7 00000000 00000001 0000001e isatq!AtqProcessTimeoutOfRequests_33+0x4f
014cff70 68621e66 68629148 000ad1b8 686230c0 isatq!I_AtqTimeOutWorker+0x30
014cff7c 686230c0 00000000 00000001 000c000a isatq!I_AtqTimeoutCompletion+0x38
014cffb8 77f04f2c 00000000 00000001 000c000a isatq!SchedulerThread_297+0x2f
00000001 000003e6 00000000 00000001 000c000a kernel32!BaseThreadStart+0x51
```

请注意，此线程有一个对 **WaitForCriticalSection** 函数的调用，这意味着不仅会有一个锁，还会等待其他内容锁定的代码。 通过查看调用 **WaitForCriticalSection** 的第一个参数，可以找出正在等待的关键部分。 这是 " **参数到子元素**：" 24e750 "下的第一个地址。 因此，此线程正在等待地址0x24E750 的关键部分。 这是前面使用的 **！锁** 扩展列出的第三个关键部分。

换句话说，线程4（拥有第二个关键部分）正在等待第三个关键部分。 现在，请注意第三个关键部分（也被锁定）。 拥有线程的线程 ID 为0xA9。 返回到 **~** 前面看到的命令的输出，请注意，具有此 ID 的线程为线程编号6。 显示此线程的堆栈 backtrace：

```dbgcmd
0:006>  ~6 kb 
ChildEBP RetAddr  Args to Child
0155fe38 77f6cc7b 00000414 00000000 00000000 ntdll!NtWaitForSingleObject+0xb
0155feac 77f67456 68629100 6862142e 68629100 ntdll!RtlpWaitForCriticalSection+0xaa 
0155feb4 6862142e 68629100 0009f238 686222e1 ntdll!RtlEnterCriticalSection+0x46
0155fec0 686222e1 0009f25c 00000001 0009f238 isatq!ATQ_CONTEXT_LISTHEAD__RemoveFromList
0155fed0 68621412 0009f238 686213d1 0009f238 isatq!ATQ_CONTEXT__CleanupAndRelease+0x30
0155fed8 686213d1 0009f238 00000001 01f26bcc isatq!AtqpReuseOrFreeContext+0x3f
0155fee8 683331f7 0009f238 00000001 01f26bf0 isatq!AtqFreeContext+0x36
0155fefc 6833984b ffffffff 00000000 00000000 ftpsvc2!ASYNC_IO_CONNECTION__SetNewSocket
0155ff18 6833adcd 77f05154 01f26a58 00000000 ftpsvc2!USER_DATA__Cleanup+0x47
0155ff28 6833ad8f 01f26a58 000a3410 0155ff54 ftpsvc2!DereferenceUserDataAndKill+0x39
0155ff38 6833324a 01f26a58 00000000 00000040 ftpsvc2!ProcessUserAsyncIoCompletion+0x2a
0155ff54 686211eb 01f26bac 00000000 00000040 ftpsvc2!ProcessAtqCompletion+0x32
0155ff88 68622676 000a3464 00000000 000a3414 isatq!AtqpProcessContext+0xa7
0155ffb8 77f04f2c abcdef01 ffffffff 000ad1b0 isatq!AtqPoolThread+0x32
0155ffec 00000000 68622644 abcdef01 00000000 kernel32!BaseThreadStart+0x51
```

此线程也正在等待要释放的关键部分。 在这种情况下，它正在等待0x68629100 的临界部分。 这是之前由 **！锁** 扩展生成的列表中的第二个关键部分。

这是死锁。 线程4（拥有第二个关键部分）正在等待第三个关键部分。 拥有第三个关键部分的线程6正在等待第二个关键部分。

确认此死锁的性质后，可以使用常用的调试技术来分析线程4和6。

### <a name="span-iddebugging_a_kernel_mode_deadlockspanspan-iddebugging_a_kernel_mode_deadlockspandebugging-a-kernel-mode-deadlock"></a><span id="debugging_a_kernel_mode_deadlock"></span><span id="DEBUGGING_A_KERNEL_MODE_DEADLOCK"></span>调试 Kernel-Mode 死锁

有几个调试器扩展适用于在内核模式下调试死锁：

- [**！ Kdexts**](-locks---kdext--locks-.md)扩展显示有关内核资源中持有的所有锁以及持有这些锁的线程的信息。 在内核模式下 (，只需在调试器提示符下键入 **！锁** 即可;假定 **kdexts** 前缀。 ) 

- [**！ Qlocks**](-qlocks.md)扩展显示所有排队的自旋锁的状态。

- [**！ Wdfkd; wdfspinlock**](-deadlock.md)扩展显示 Kernel-Mode Driver FRAMEWORK (KMDF) 旋转锁定对象的相关信息。

- [**！死锁**](-deadlock.md)扩展与驱动程序验证器结合使用，以检测你的代码中可能会导致死锁的锁的不一致使用。

当内核模式中发生死锁时，请使用 **！ kdexts** 扩展来列出线程当前获取的所有锁。

通常可以通过查找一个在执行线程所需的资源上持有排他锁的非执行线程，来查明死锁。 大多数锁都是共享的。
