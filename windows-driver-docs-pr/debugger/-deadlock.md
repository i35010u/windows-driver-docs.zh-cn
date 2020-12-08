---
title: deadlock
description: 死锁扩展显示了驱动程序验证程序的死锁检测选项收集的死锁的相关信息。
keywords:
- '驱动程序验证程序 (的死锁检测) '
- 死锁 Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- deadlock
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a30fd3a820de0e4b2a02e6dac5e886e1cb7876e5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96785323"
---
# <a name="deadlock"></a>!deadlock


**！死锁** 扩展显示了驱动程序验证程序的 **死锁检测** 选项收集的死锁的相关信息。

```dbgcmd
!deadlock 
!deadlock 1
```

## <span id="ddk__deadlock_dbg"></span><span id="DDK__DEADLOCK_DBG"></span>


### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

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

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关驱动程序验证程序的信息，请参阅 Windows 驱动程序工具包 (WDK) 文档。

<a name="remarks"></a>备注
-------

此扩展将仅在以下情况下提供有用信息：驱动程序验证程序的 **死锁检测** 选项检测到锁定层次结构冲突和发出 [**bug 检查 0XC4**](bug-check-0xc4--driver-verifier-detected-violation.md) (驱动程序 \_ 验证程序 \_ 检测到 \_ 冲突) 。

如果没有任何参数， **！死锁** 扩展将导致显示基本的锁层次结构拓扑。 如果此问题不是简单的循环死锁，则此命令将描述发生的情况。

**！死锁 1** 扩展会导致显示堆栈跟踪。 显示的堆栈将是在获取锁时处于活动状态的堆栈。

以下是示例：

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

这会告诉你哪些线程和涉及哪些锁。 不过，它只是一个摘要，可能没有足够的信息来充分调试这种情况。

使用 **！死锁 1** ，可在获取每个参与死锁的锁时输出调用堆栈的内容。 由于这些是运行时堆栈跟踪，因此，如果使用的是已检查的生成，则它们将更完整。 在 Windows 10 版本1803之前，已检查的生成在 windows 的早期版本上可用。 在免费版本上，它们可能会在很少一行后被截断。

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

使用此信息，你几乎可以获得所需的全部内容，但当前堆栈除外：

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

从此，你可以查看涉及的锁以及获取它们的位置。 此信息应该足以使您能够调试死锁。 如果源代码可用，则可以使用调试器来准确查看出现问题的位置：

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

现在，你知道了源文件的名称和进行获取的行号。 在这种情况下，源文件将显示线程的行为如下所示：

-   线程1： **DummyActivateVcComplete** 采用了 **虚** 微型端口锁。 然后，它称为 **dummyQueueRecvBuffers**，它采用了 **虚拟** 全局锁。

-   线程2： **dummyRxInterruptOnCompletion** 采用全局锁。 然后，几行后，它会使用微型端口锁。

此时，死锁会完全清晰。

 

 





