---
title: 调试死锁-DRIVER_VERIFIER_DETECTED_VIOLATION (C4) 0x1001
description: 当驱动程序验证程序检测到数值调节钮锁层次结构冲突，在参数 1 值为 0x1001 驱动程序 Verifiergenerates Bug 检查 0xC4 DRIVER_VERIFIER_DETECTED_VIOLATION。
ms.assetid: 4C3ED1DB-5EDC-4386-B91C-CF86973EE1F6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d3b49d9c51ca2141a12f518298bb56fd5505e94e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63344867"
---
# <a name="span-iddevtestdebuggingdeadlocks-driververifierdetectedviolationc40x1001spandebugging-deadlocks---driververifierdetectedviolation-c4-0x1001"></a><span id="devtest.debugging_deadlocks_-_driver_verifier_detected_violation__c4___0x1001"></span>调试死锁的驱动程序\_VERIFIER\_检测到\_冲突 (C4):0x1001


当[Driver Verifier](driver-verifier.md)检测到自旋锁层次结构冲突，驱动程序 Verifiergenerates [ **Bug 检查 0xC4:驱动程序\_VERIFIER\_已检测\_冲突**](https://msdn.microsoft.com/library/windows/hardware/ff560187) 0x1001 的参数 1 值。

当死锁检测选项处于活动状态 （死锁检测是驱动程序验证工具标准选项的一部分）， [Driver Verifier](driver-verifier.md)跟踪的每个分配的自旋锁并已获得和释放的顺序。 锁层次结构冲突意味着驱动程序验证程序检测到这种情况中至少一个的情况下，位置*LockA*是获取和保存之前*LockB*是已获得，并在另一个， *LockB*是获取和保存之前*LockA*是必需的。

**重要**此 bug 检查会发生[Driver Verifier](driver-verifier.md)检测到的层次结构已发生冲突，不在发生实际的死锁情况时。 此冲突，强制实施强强制要求的驱动程序的各种组件之间共享的任何锁始终应获取和释放以这样两个线程不可能的死锁的顺序。



**Windows 8.1 中的新增功能**时[Driver Verifier](driver-verifier.md)遇到此冲突，如果附加调试器，调试器将要求您输入有关该错误。 在 Windows 8 和 Windows 的早期版本中，此冲突会导致立即 bug 检查。

```
************ Verifier Detected a Potential Deadlock *************
**
** Type !deadlock in the debugger for more information.
**
*****************************************************************

*** Verifier assertion failed ***
(B)reak, (I)gnore, (W)arn only, (R)emove assert?
```

若要调试此冲突运行 Windows 8.1 的计算机上，选择**B** （中断），请输入建议的调试器命令和 ([**！ 死锁**](https://msdn.microsoft.com/library/windows/hardware/ff562326)):

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

[ **！ 死锁**](https://msdn.microsoft.com/library/windows/hardware/ff562326) **3**还可以使用命令以显示详细信息，包括上一次时候的堆栈获取：

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

调试器会建议使用[ **kb （显示堆栈回溯）** ](https://msdn.microsoft.com/library/windows/hardware/ff551943)命令以显示当前的堆栈跟踪。

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

调试器输出显示有问题的驱动程序通过获取和上一个线程获取锁 B 之前保存锁定一个违反此规则，以及现在已获取锁 B 以及尝试获取锁的另一个线程上。 请注意，第一个线程 （线程 0） 将被终止，因此，在某些时候加载驱动程序映像后发生的购置与这些两个锁的后续版本。

在加载测试驱动程序的正确符号时，调试器会显示在其中已获取锁时的函数。 在此示例中，因此发生在同一函数中获取的锁和锁 B。 在线程 0 中，同时获得中*SystemControlIrpWorker*。 在线程 1 中，同时获得中*DeviceControlIrpWorker* (从锁 B 输出所示 **！ 死锁 3**和当前的堆栈输出 (**kb**)。

此时，查看每个函数的源代码应显示的代码路径存在，这种顺序获取锁。

同时*MyTestDriver ！AlphaLock*和*MyTestDriver ！BravoLock*是全球可用驱动程序中的对象：

```
include "MyTestDriverHeader.h"

// Locks used to control access to various objects
extern KSPIN_LOCK AlphaLock;
extern KSPIN_LOCK BravoLock;
```

在函数内部*SystemControlIrpWorker*，存在一个路径其中 AlphaLock (中的一个锁 **！ 死锁**输出) 是获取和保存时获取 BravoLock (锁 B)。 它也是值得一提，在其中何种方式获得的相反顺序正确释放锁。 （下面的代码是很大程度编辑以仅显示元素生成这种情况下所需）。

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

如果您查看以下*DeviceControlIrpWorker*示例函数，可以看到，就可以按相反的顺序获取锁。 也就是说，BravoLock 可以获取并持有尝试获取 AlphaLock 时。 以下示例进行了简化，但它显示存在可能的路径可能发生冲突。

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

若要修复此潜在的冲突，正确的做法是确保，只要该驱动程序尝试获取 AlphaLock，它会检查并确保没有保留 BravoLock。 最简单的解决方法是只需释放 BravoLock 和重新获取它，就立即获取 AlphaLock。 但更重要的代码更改可能会需要非常重要 BravoLock 保护任何数据不会更改在等待 AlphaLock 和 BravoLock 重新获取。

有关自旋锁和其他同步技术的详细信息，请参阅[自旋锁](https://msdn.microsoft.com/library/windows/hardware/ff563830)。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[自旋锁](https://msdn.microsoft.com/library/windows/hardware/ff563830)

[**Bug 检查 0xC4:驱动程序\_VERIFIER\_检测到\_冲突**](https://msdn.microsoft.com/library/windows/hardware/ff560187)

[**!deadlock**](https://msdn.microsoft.com/library/windows/hardware/ff562326)










