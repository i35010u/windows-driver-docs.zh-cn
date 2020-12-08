---
title: 调试死锁-DRIVER_VERIFIER_DETECTED_VIOLATION (C4) 0x1001
description: 当驱动程序验证器检测到旋转锁层次结构冲突时，驱动程序 Verifiergenerates Bug 检查 0xC4 DRIVER_VERIFIER_DETECTED_VIOLATION 的参数1值为0x1001。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 80694963438695ac52c6a5ebe1393e2f2656b0ac
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96817839"
---
# <a name="span-iddevtestdebugging_deadlocks_-_driver_verifier_detected_violation__c4___0x1001spandebugging-deadlocks---driver_verifier_detected_violation-c4-0x1001"></a><span id="devtest.debugging_deadlocks_-_driver_verifier_detected_violation__c4___0x1001"></span>调试死锁-驱动程序 \_ 验证器 \_ 检测到 \_ 违反 (C4) ：0x1001


当 [驱动程序验证](driver-verifier.md) 器检测到旋转锁层次结构冲突时，驱动程序 Verifiergenerates [**Bug 检查0XC4：驱动程序 \_ 验证器 \_ 检测到 \_**](../debugger/bug-check-0xc4--driver-verifier-detected-violation.md) 与0x1001 的参数1值冲突。

如果死锁检测选项处于活动状态 (死锁检测是驱动程序验证器标准选项的一部分) ，则 [驱动程序验证](driver-verifier.md) 器会跟踪分配的每个自旋锁以及获取和释放该锁的顺序。 锁层次结构冲突是指驱动程序验证器检测到，其中至少有一种情况下， *LockA* 在获取 *LockB* 之前获得并保存，而另一种情况是在需要 *LockA* 之前获得并保存 *LockB* 。

**重要提示**  当 [驱动程序验证程序](driver-verifier.md) 检测到层次结构冲突，而不是发生实际的死锁情况时，将发生此 bug 检查。 此冲突强制执行强烈强制要求：应始终获取和释放在驱动程序的各个组件之间共享的任何锁，使两个线程的死锁不可能。



**Windows 8.1 中的新增项** 当 [驱动程序验证程序](driver-verifier.md) 遇到此冲突时，如果附加了调试器，调试器会要求输入有关错误的信息。 在 Windows 8 和早期版本的 Windows 中，此冲突将导致立即进行 bug 检查。

```
************ Verifier Detected a Potential Deadlock *************
**
** Type !deadlock in the debugger for more information.
**
*****************************************************************

**_ Verifier assertion failed _*_
(B)reak, (I)gnore, (W)arn only, (R)emove assert?
```

若要在运行 Windows 8.1 的计算机上调试此冲突，请选择 _ *B** (中断) ，然后输入建议的调试器命令 ([**！死锁**](../debugger/-deadlock.md)) ：

```
kd> !deadlock
issue: 00001001 97dd800c 86858ce0 00000000 

Deadlock detected (2 locks in 2 threads):

Thread 0: A B.
Thread 1: B A.

Where:

Thread 0 = TERMINATED.
Thread 1 = c4ae2040.

Lock A =   97dd800c (MyTestDriver!AlphaLock+0x00000000) - Type 'Spinlock'.
Lock B =   97dd8008 (MyTestDriver!BravoLock+0x00000000) - Type 'Spinlock'.
```

[**！死锁**](../debugger/-deadlock.md) **3** 命令也可用于显示详细信息，包括上次获取时的堆栈：

```
kd> !deadlock 3
issue: 00001001 97dd800c 86858ce0 00000000 

Deadlock detected (2 locks in 2 threads):
# 

Thread 0: TERMINATED took locks in the following order:

Lock A =     97dd800c (MyTestDriver!AlphaLock+0x00000000) - Type 'Spinlock'.

    Node:    8685acd8

    Stack:   97dd65b7 MyTestDriver!SystemControlIrpWorker+0x00000027 
             97dd605a MyTestDriver!Dispatch_SystemControl+0x0000001a 
             820c4b4d nt!IovCallDriver+0x000002cc 
             81ca3772 nt!IofCallDriver+0x00000062 
             81eb165e nt!IopSynchronousServiceTail+0x0000016e 
             81eb5518 nt!IopXxxControlFile+0x000003e8 
             81eb4516 nt!NtDeviceIoControlFile+0x0000002a 
             81d27e17 nt!KiSystemServicePostCall+0x00000000 

Lock B =     97dd8008 (MyTestDriver!BravoLock+0x00000000) - Type 'Spinlock'.

    Node:    86833578

    Stack:   97dd65c5 MyTestDriver!SystemControlIrpWorker+0x00000a4a 
             97dd605a MyTestDriver!Dispatch_SystemControl+0x0000001a 
             820c4b4d nt!IovCallDriver+0x000002cc 
             81ca3772 nt!IofCallDriver+0x00000062 
             81eb165e nt!IopSynchronousServiceTail+0x0000016e 
             81eb5518 nt!IopXxxControlFile+0x000003e8 
             81eb4516 nt!NtDeviceIoControlFile+0x0000002a 
             81d27e17 nt!KiSystemServicePostCall+0x00000000
# 

Thread 1: c4ae2040 (ThreadEntry = 86833a08) took locks in the following order:

Lock B =     97dd8008 (MyTestDriver!BravoLock+0x00000000) - Type 'Spinlock'.

    Node:    86858ce0

    Stack:   97dd65ef MyTestDriver!DeviceControlIrpWorker+0x0000005f 
             97dd605a MyTestDriver!Dispatch_DeviceControl+0x0000001a 
             820c4b4d nt!IovCallDriver+0x000002cc 
             81ca3772 nt!IofCallDriver+0x00000062 
             81eb165e nt!IopSynchronousServiceTail+0x0000016e 
             81eb5518 nt!IopXxxControlFile+0x000003e8 
             81eb4516 nt!NtDeviceIoControlFile+0x0000002a 
             81d27e17 nt!KiSystemServicePostCall+0x00000000 

Lock A =     97dd800c (MyTestDriver!AlphaLock+0x00000000) - Type 'Spinlock'.

    Stack:   << Current stack trace - use kb to display it >>
```

调试器建议使用 [**kb (显示 Stack Backtrace)**](../debugger/k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md) 命令显示当前堆栈跟踪。

```
kd> kb
ChildEBP RetAddr  Args to Child              
89b2cac4 820da328 97dd800c 86858ce0 00000000 nt!VfReportIssueWithOptions+0x86
89b2caf4 820d92a2 00000001 00000000 97dd65fd nt!ViDeadlockAnalyze+0x1d1
89b2cb7c 820d424e 86858ce0 00000000 97dd65fd nt!VfDeadlockAcquireResource+0x2fd
89b2cb9c 97dd65fd 00007780 89b2cbbc 97dd605a nt!VerifierKfAcquireSpinLock+0x8c
89b2cba8 97dd605a 9a9e7780 88d08f48 00000000 MyTestDriver!DeviceControlIrpWorker+0x54a
89b2cbbc 820c4b4d 9a9e7780 88d08f48 820c4881 MyTestDriver!Dispatch_DeviceControl+0x1a
(Inline) -------- -------- -------- -------- nt!IopfCallDriver+0x47
89b2cbe0 81ca3772 81eb165e b3c9ff80 88d08f48 nt!IovCallDriver+0x2cc
89b2cbf4 81eb165e 88d08fdc 88d08f48 00000000 nt!IofCallDriver+0x62
```

调试器输出显示有问题的驱动程序违反了该规则，方法是获取并保存锁 A，然后在一个线程上获取锁 B，现在已获取锁 B 并尝试在另一个线程上获取锁定。 请注意，第一个线程 (线程 0) 终止，因此，在加载驱动程序映像后，在某个时间点会发生这两种锁的获取和后续版本。

加载测试驱动程序的适当符号时，调试器将显示在此时间获取锁的函数。 在此示例中，这种情况的发生是在同一函数中获取锁定 A 和锁定 B。 在线程0中，它们都是在 *SystemControlIrpWorker* 中获取的。 在线程1中，它们都是在 *DeviceControlIrpWorker* 中获取的， (从 **！死锁 3** 的锁 B 输出和当前堆栈输出 (**kb**) 中所示。

此时，查看每个函数的源代码应会显示代码路径存在，在此情况下，可以按此顺序获取锁。

这两个 *MyTestDriver！AlphaLock* 和 *MyTestDriver！BravoLock* 是驱动程序中全局可用的对象：

```
include "MyTestDriverHeader.h"

// Locks used to control access to various objects
extern KSPIN_LOCK AlphaLock;
extern KSPIN_LOCK BravoLock;
```

在函数 *SystemControlIrpWorker* 中，存在一个路径，在该路径中，AlphaLock (**在)** (锁定 B 获取时获取并保存) 。 还值得注意的是，锁按其获取顺序正确地释放。  (对以下代码进行了大量编辑，以便仅显示生成此方案) 所需的元素。

```ManagedCPlusPlus
NTSTATUS SystemControlIrpWorker(_In_ PIRP Irp)
{
    KIRQL IrqlAlpha;
    KIRQL IrqlBravo;
    // <<Other local variable declarations removed>>

    // <<Various lines of code not shown>>

    KeAcquireSpinLock (&AlphaLock, &IrqlAlpha);

    // <<Various lines of code not shown>>

    KeAcquireSpinLock (&BravoLock, &IrqlBravo);

    // <<Various lines of code not shown>>

    KeReleaseSpinLock (&BravoLock, IrqlBravo);
    KeReleaseSpinLock (&AlphaLock, IrqlAlpha);

    // <<Various lines of code not shown>>
}
```

如果查看下面的 *DeviceControlIrpWorker* 示例函数，可以看到可以按相反顺序获取锁。 也就是说，尝试获取 AlphaLock 时，可以获取和保留 BravoLock。 下面的示例是简化的，但它显示存在可能发生冲突的可能的路径。

```ManagedCPlusPlus
NTSTATUS DeviceControlIrpWorker(_In_ PIRP Irp, 
                                _In_ BOOLEAN bSomeCondition)
{
    KIRQL IrqlAlpha;
    KIRQL IrqlBravo;
    // <<Other local variable declarations removed>>

    if (bSomeCondition == FALSE)
    {
        //
        // Note that if bSomeCondition is FALSE, then AlphaLock is acquired here
        // If bSomeCondition is TRUE, it is not needed to be acquired right now
        //
        KeAcquireSpinLock (&AlphaLock, &IrqlAlpha);
    }

    // <<Various lines of code not shown>>

    KeAcquireSpinLock (&BravoLock, &IrqlBravo);

    // <<Various lines of code not shown>>

    if (bSomeCondition == TRUE)
    { 
        //
        // Need to acquire AlphaLock here for upcoming code logic
        //
        KeAcquireSpinLock (&AlphaLock, &IrqlAlpha);

        // <<Various lines of code not shown>>

        KeReleaseSpinLock (&AlphaLock, IrqlAlpha);
    }

    // <<Various lines of code not shown>>

    KeReleaseSpinLock (&BravoLock, IrqlBravo);

    if (bSomeCondition == FALSE)
    {
        //
        // Release the AlphaLock, which was acquired much earlier
        //
        KeReleaseSpinLock (&AlphaLock, IrqlAlpha);
    }

    // <<Various lines of code not shown>>
}
```

若要解决这种潜在的冲突，应执行的正确操作是确保每当驱动程序尝试获取 AlphaLock 时，它都会检查并确保未持有 BravoLock。 最简单的解决方法就是只发布 BravoLock，并在获取 AlphaLock 后立即重新获取。 但是，如果在等待 AlphaLock 和重新获取 BravoLock 时，保护的任何数据 BravoLock 不会更改，则可能需要更重要的代码更改。

有关自旋锁和其他同步技术的详细信息，请参阅 [自旋锁](../kernel/introduction-to-spin-locks.md)。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[自旋锁](../kernel/introduction-to-spin-locks.md)

[**Bug 检查0xC4：驱动程序 \_ 验证程序 \_ 检测到 \_ 冲突**](../debugger/bug-check-0xc4--driver-verifier-detected-violation.md)

[**!deadlock**](../debugger/-deadlock.md)
