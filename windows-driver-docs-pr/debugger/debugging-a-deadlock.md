---
title: 调试死锁
description: 调试死锁
ms.assetid: ee7990d9-2d4e-4e48-9214-539eebd1d8db
keywords:
- 死锁
- 线程，没有准备就绪的线程
ms.date: 06/10/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1235f31ca6a62c6028ddd17fc239a9d4e2ecf06e
ms.sourcegitcommit: 85b989c149403210f2c7b892e045d037580432e5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/10/2019
ms.locfileid: "66825050"
---
# <a name="debugging-a-deadlock"></a>调试死锁

## <span id="ddk_debugging_deadlocks_no_ready_threads__dbg"></span><span id="DDK_DEBUGGING_DEADLOCKS_NO_READY_THREADS__DBG"></span>

当一个线程需要独占访问代码或其他一些资源时，它请求*锁*。 如果可以 Windows 做出响应，从而此锁定线程。 此时，没有其他系统中可以访问锁定的代码。 这种情况一直存在，任何编写良好的多线程应用程序的正常部分。 尽管特定代码段只能有一个锁在其上一次，多个代码段可以每个具有其自己的锁。

一个*死锁*当两个或多个线程已请求在两个或多个资源，不兼容的序列中的锁时出现。 例如，假设一个线程已获取资源的锁，且然后请求访问资源 b。同时，两个线程已获取了锁资源 B 上的，然后请求访问资源 a。既不线程可以继续执行，直到释放其他线程的锁，并因此，两个线程可以继续执行。

当多个线程，通常的单个应用程序，已阻止对方的访问相同资源时，会出现用户模式下死锁。 但是，多个线程的多个应用程序还可以阻止对方的访问全局/共享资源，如全局事件或信号量。

多个线程 （来自同一个进程或从不同的进程） 具有阻止其他用户访问相同的内核资源时，会出现内核模式死锁。

用于调试死锁的过程取决于在用户模式或内核模式下是否发生死锁。

### <a name="span-iddebuggingausermodedeadlockspanspan-iddebuggingausermodedeadlockspandebugging-a-user-mode-deadlock"></a><span id="debugging_a_user_mode_deadlock"></span><span id="DEBUGGING_A_USER_MODE_DEADLOCK"></span>调试用户模式下死锁

死锁时出现在用户模式下，使用以下过程来对其进行调试：

1. 问题[ **！ ntsdexts.locks** ](-locks---ntsdexts-locks-.md)扩展。 在用户模式下，您只需键入 **！ 锁**调试器提示符; **ntsdexts**假定前缀。

2. 此扩展显示当前进程，以及拥有线程的 ID 和每个关键节的锁计数与相关联的所有关键部分。 如果关键节锁计数为零，未锁定。 使用[ **~ （线程状态）** ](---thread-status-.md)命令以查看线程拥有其他关键部分的相关信息。

3. 使用[ **kb （显示堆栈回溯）** ](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)命令为每个线程来确定是否它们正在等待其他关键部分。

4. 使用这些输出**kb**命令，可以查找死锁： 两个线程的每个等待锁持有的另一个线程。 在极少数情况下，可能由两个以上的线程在循环模式中，持有锁引起死锁，但大多数死锁涉及只有两个线程。

下面是举例说明了此过程。 以开头 **！ ntdexts.locks**扩展：

```dbgcmd
0:006>  !locks 
CritSec ftpsvc2!g_csServiceEntryLock+0 at 6833dd68
LockCount          0
RecursionCount     1
OwningThread       a7
EntryCount         0
ContentionCount    0
*** Locked

CritSec isatq!AtqActiveContextList+a8 at 68629100
LockCount          2
RecursionCount     1
OwningThread       a3
EntryCount         2
ContentionCount    2
*** Locked

CritSec +24e750 at 24e750
LockCount          6
RecursionCount     1
OwningThread       a9
EntryCount         6
ContentionCount    6
*** Locked
```

第一个关键节显示没有锁，因此，可以忽略。

显示的第二个关键部分锁计数为 2，因此，因此，死锁的可能的原因。 拥有线程具有 0xA3 的线程 ID。

可以通过列出所有的线程查找此线程[ **~ （线程状态）** ](---thread-status-.md)命令，并查找具有此 ID 的线程：

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

在此显示中的第一项是调试器的内部线程数。 第二项 (`Id`字段) 包含两个十六进制数字，由小数点分隔。 小数点前的数是进程 ID;数字的小数点后线程 id。 在此示例中，可以看到，线程 ID 0xA3 对应的线程数为 4。

然后，使用[ **kb （显示堆栈回溯）** ](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)命令以显示线程号 4 到对应的堆栈：

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

请注意，此线程已调用**WaitForCriticalSection**函数，这意味着不仅没有锁，它正在等待的其他内容锁定的代码。 我们可以了解我们正在等待通过查看调用的第一个参数的关键部分**WaitForCriticalSection**。 这是下的第一个地址**子参数**:"24e750"。 使此线程正在等待在地址 0x24E750 的关键部分。 这是按列出的第三个关键部分 **！ 锁**先前使用的扩展。

换而言之，线程 4，拥有第二个关键部分，正在等待第三个关键部分。 现在将注意力转到第三个关键部分，会被锁定。 拥有线程有线程 ID 0xA9。 返回到的输出 **~** 命令，您之前看到的那样，请注意，此 ID 的线程是线程编号为 6。 显示此线程的堆栈反向跟踪：

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

此线程太，正在等待要释放的关键部分。 在这种情况下，它正在等待在 0x68629100 的关键部分。 这是之前由生成的列表中的第二个关键部分 **！ 锁**扩展。

这是死锁。 线程 4，拥有第二个关键部分，正在等待第三个关键部分。 线程 6，拥有第三个关键部分，正在等待第二个关键部分。

在确认这种死锁的性质，可以使用常用的调试技术来分析线程 4 和 6。

### <a name="span-iddebuggingakernelmodedeadlockspanspan-iddebuggingakernelmodedeadlockspandebugging-a-kernel-mode-deadlock"></a><span id="debugging_a_kernel_mode_deadlock"></span><span id="DEBUGGING_A_KERNEL_MODE_DEADLOCK"></span>调试内核模式死锁

有几个可用于在内核模式下调试死锁的调试器扩展：

- [ **！ Kdexts.locks** ](-locks---kdext--locks-.md)扩展显示有关所有内核的资源和控制这些锁的线程上持有的锁的信息。 (在内核模式下，您只需键入 **！ 锁**调试器提示符; **kdexts**假定前缀。)

- [ **！ Qlocks** ](-qlocks.md)扩展显示的所有排队的自旋锁的状态。

- [ **！ Wdfkd.wdfspinlock** ](-deadlock.md)扩展显示内核模式驱动程序框架 (KMDF) 旋转锁对象有关的信息。

- [ **！ 死锁**](-deadlock.md)扩展使用与 Driver Verifier 一起用于在代码中的有可能会导致死锁检测不一致的锁。

死锁发生时在内核模式下，使用 **！ kdexts.locks**扩展以列出所有当前线程获取的锁。

通常可以通过查找对资源所需的执行线程持有排他锁的一个非执行线程来查明死锁。 共享锁的大多数。
