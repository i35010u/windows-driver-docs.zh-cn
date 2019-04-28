---
title: 死锁
description: 死锁扩展显示有关死锁由驱动程序验证程序的死锁检测选项收集的信息。
ms.assetid: c0e6074f-8afe-4526-a30f-427aac67ab99
keywords:
- 死锁检测 （驱动程序验证程序）
- Windows 调试的死锁
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- deadlock
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3df3c218a781e2d42d3e1b7bb1477059bad8e97c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336842"
---
# <a name="deadlock"></a>!deadlock


**！ 死锁**扩展显示有关死锁所收集的信息**死锁检测**Driver Verifier 选项。

```dbgcmd
!deadlock 
!deadlock 1
```

## <span id="ddk__deadlock_dbg"></span><span id="DDK__DEADLOCK_DBG"></span>


### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

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
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关驱动程序验证程序的信息，请参阅 Windows Driver Kit (WDK) 文档。

<a name="remarks"></a>备注
-------

此扩展仅提供有用信息 Driver Verifier**死锁检测**违反锁层次结构并颁发选项[ **bug 检查 0xC4** ](bug-check-0xc4--driver-verifier-detected-violation.md)(驱动程序\_VERIFIER\_检测到\_冲突)。

不带任何参数， **！ 死锁**扩展会导致要显示的基本锁层次结构拓扑。 如果此问题不是简单的循环死锁，此命令将描述已发生这种情况。

**！ 死锁 1**扩展会导致堆栈跟踪以显示。 显示的堆栈将在与活动已获取锁的时间。

下面是一个示例：

```dbgcmd
0:kd> !deadlock

Deadlock detected (2 resources in 2 threads):

Thread 0: A B
Thread 1: B A

Where:
Thread 0 = 8d3ba030
Thread 1 = 8d15c030
Lock A =   bba2af30 Type 'Spinlock'
Lock B =   dummy!GlobalLock Type 'Spinlock'
```

这将告知您哪些线程以及涉及哪些锁。 但是，它用于摘要，可能不是足够的信息来充分调试这种情况。

使用 **！ 死锁 1**可以在每个参与死锁的锁定的时间打印出的调用堆栈的内容。 由于这些是运行时堆栈跟踪，则会更完整，如果正在使用已检验的版本。 免费版本，它们可能会被截断后只需少量的一行。

```dbgcmd
0:kd> !deadlock 1

Deadlock detected (2 resources in 2 threads):

Thread 0 (8D14F750) took locks in the following order:

    Lock A -- b7906f30 (Spinlock)
    Stack:   dummy!DummyActivateVcComplete+0x63
             dummy!dummyOpenVcChannels+0x2E1
             dummy!DummyAllocateRecvBufferComplete+0x436
             dummy!DummyAllocateComplete+0x55
             NDIS!ndisMQueuedAllocateSharedHandler+0xC9
             NDIS!ndisWorkerThread+0xEE

    Lock B -- dummy!GlobalLock (Spinlock)
    Stack:   dummy!dummyQueueRecvBuffers+0x2D
             dummy!DummyActivateVcComplete+0x90
             dummy!dummyOpenVcChannels+0x2E1
             dummy!DummyAllocateRecvBufferComplete+0x436
             dummy!DummyAllocateComplete+0x55

Thread 1 (8D903030) took locks in the following order:

    Lock B -- dummy!GlobalLock (Spinlock)
    Stack:   dummy!dummyRxInterruptOnCompletion+0x25D
             dummy!DummyHandleInterrupt+0x32F
             NDIS!ndisMDpcX+0x3C
             ntkrnlpa!KiRetireDpcList+0x5D

    Lock A -- b7906f30 (Spinlock)
    Stack:   << Current stack >>
```

使用此信息，有需要除当前堆栈几乎所有内容：

```dbgcmd
0: kd> k
ChildEBP RetAddr
f78aae6c 80664c58 ntkrnlpa!DbgBreakPoint
f78aae74 8066523f ntkrnlpa!ViDeadlockReportIssue+0x2f
f78aae9c 806665df ntkrnlpa!ViDeadlockAnalyze+0x253
f78aaee8 8065d944 ntkrnlpa!VfDeadlockAcquireResource+0x20b
f78aaf08 bfd6df46 ntkrnlpa!VerifierKeAcquireSpinLockAtDpcLevel+0x44
f78aafa4 b1bf2d2d dummy!dummyRxInterruptOnCompletion+0x2b5
f78aafc4 bfde9d8c dummy!DummyHandleInterrupt+0x32f
f78aafd8 804b393b NDIS!ndisMDpcX+0x3c
f78aaff4 804b922b ntkrnlpa!KiRetireDpcList+0x5d
```

从这可以看到哪些锁的过程中涉及和其中它们已获取。 这应该是足够的信息，以便调试死锁。 如果源代码不可用，您可以使用调试器查看问题发生的确切位置：

```dbgcmd
0: kd> .lines
Line number information will be loaded

0: kd> u dummy!DummyActivateVcComplete+0x63 l1
dummy!DummyActivateVcComplete+63 [d:\nt\drivers\dummy\vc.c @ 2711]:
b1bfe6c9 837d0c00         cmp     dword ptr [ebp+0xc],0x0

0: kd> u dummy!dummyQueueRecvBuffers+0x2D l1
dummy!dummyQueueRecvBuffers+2d [d:\nt\drivers\dummy\receive.c @ 2894]:
b1bf4e39 807d0c01         cmp     byte ptr [ebp+0xc],0x1

0: kd> u dummy!dummyRxInterruptOnCompletion+0x25D l1
dummy!dummyRxInterruptOnCompletion+25d [d:\nt\drivers\dummy\receive.c @ 1424]:
b1bf5d05 85f6             test    esi,esi

0: kd> u dummy!dummyRxInterruptOnCompletion+0x2b5 l1
dummy!dummyRxInterruptOnCompletion+2b5 [d:\nt\drivers\dummy\receive.c @ 1441]:
b1bf5d5d 8b4648           mov     eax,[esi+0x48]
```

现在您已了解的源文件和获取发生的行号的名称。 在这种情况下，在源代码文件将显示线程的行为，如下所示：

-   线程 1:**DummyActivateVcComplete**耗时**虚拟**微型端口锁。 然后，调用其**dummyQueueRecvBuffers**，耗时**虚拟**全局锁。

-   线程 2: **dummyRxInterruptOnCompletion**花费了全局锁。 然后，几行更高版本，它占用微型端口锁定。

在此情况下，死锁变得完全清楚。

 

 





