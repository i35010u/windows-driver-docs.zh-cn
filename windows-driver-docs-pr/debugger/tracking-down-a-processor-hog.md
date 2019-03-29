---
title: 跟踪占用大量处理器资源的进程
description: 跟踪占用大量处理器资源的进程
ms.assetid: 8ecd000d-34e6-4471-a040-b50627915a20
keywords:
- 处理器占用了大量
- 占用处理器
- 耗尽应用程序
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 239a417a979d1509bdca7b8b0ffc0421b5075eb5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563276"
---
# <a name="tracking-down-a-processor-hog"></a>跟踪占用大量处理器资源的进程


## <span id="ddk_tracking_down_a_processor_hog_dbg"></span><span id="DDK_TRACKING_DOWN_A_PROCESSOR_HOG_DBG"></span>


如果一个应用程序占用了 （"占用"） 的其他进程将结束所有处理器的注意，"耗尽"和无法运行。

使用以下过程来更正此类 bug。

**调试应用程序正在使用所有 CPU 周期**

1.  **确定哪个应用程序导致此问题：** 使用**任务管理器**或**Perfmon**查找哪些进程正在使用 99%或 100%的处理器的时钟周期数。 这可能会告诉您有问题的线程。

2.  将 WinDbg、 KD 或 CDB 附加到此过程。

3.  **确定哪个线程问题的原因：** 分解为有问题的应用程序。 使用[ **！ 失控 3** ](-runaway.md)将扩展来创建所有 CPU 时间的"快照"的位置。 使用[ **g （转向）** ](g--go-.md)并等待几秒钟。 然后，中断并使用 **！ 失控 3**试。

    ```dbgcmd
    0:002> !runaway 3
     User Mode Time
     Thread    Time
     4e0        0:12:16.0312
     268        0:00:00.0000
     22c        0:00:00.0000
     Kernel Mode Time
     Thread    Time
     4e0        0:00:05.0312
     268        0:00:00.0000
     22c        0:00:00.0000

    0:002> g

    0:001> !runaway 3
     User Mode Time
     Thread    Time
     4e0        0:12:37.0609
     3d4        0:00:00.0000
     22c        0:00:00.0000
     Kernel Mode Time
     Thread    Time
     4e0        0:00:07.0421
     3d4        0:00:00.0000
     22c        0:00:00.0000
    ```

    比较两组数字，并查找其用户模式时间或内核模式时间已增加最多的线程。 因为 **！ 失控**按降序 CPU 时间、 有问题的线程排序通常是在列表顶部的一个。 在这种情况下，线程 0x4E0 引起问题。

4.  使用[ **~ （线程状态）** ](---thread-status-.md)并[ **~ s （设置当前线程）** ](-s--set-current-thread-.md)以使这成为当前线程的命令：
    ```dbgcmd
    0:001> ~
       0  Id: 3f4.3d4 Suspend: 1 Teb: 7ffde000 Unfrozen
    .  1  Id: 3f4.22c Suspend: 1 Teb: 7ffdd000 Unfrozen
     2  Id: 3f4.4e0 Suspend: 1 Teb: 7ffdc000 Unfrozen

    0:001> ~2s
    ```

5.  使用[ **kb （显示堆栈回溯）** ](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)若要获取此线程的堆栈跟踪：
    ```dbgcmd
    0:002> kb
    FramePtr  RetAddr   Param1   Param2   Param3   Function Name
    0b4ffc74  77f6c600  000000c8.00000000 77fa5ad0 BuggyProgram!CreateMsgFile+0x1b
    0b4ffce4  01836060  0184f440 00000001 0b4ffe20 BuggyProgram!OpenDestFileStream+0xb3
    0b4ffd20  01843eba  02b5b920 00000102 02b1e0e0 BuggyProgram!SaveMsgToDestFolder+0xb3
    0b4ffe20  01855924  0b4ffef0 00145970 0b4ffef0 BuggyProgram!DispatchToConn+0xa4
    0b4ffe5c  77e112e6  01843e16 0b4ffef0 0b4fff34 RPCRT4!DispatchToStubInC+0x34
    0b4ffeb0  77e11215  0b4ffef0 00000000 0b4fff34 RPCRT4!?DispatchToStubWorker@RPC_INTERFACE@@AAEJPAU_RPC_MESSAGE@@IPAJ@Z+0xb0
    0b4ffed0  77e1a3b1  0b4ffef0 00000000 0b4fff34 RPCRT4!?DispatchToStub@RPC_INTERFACE@@QAEJPAU_RPC_MESSAGE@Z+0x41
    0b4fff40  77e181e4  02b1e0b0 00000074 0b4fff90 RPCRT4!?ReceiveOriginalCall@OSF_SCONNECTION@Z+0x14b
    0b4fff60  77e1a5df  02b1e0b0 00000074 00149210 RPCRT4!?DispatchPacket@OSF_SCONNECTION@+0x91
    0b4fff90  77e1ac1c  77e15eaf 00149210 0b4fffec RPCRT4!?ReceiveLotsaCalls@OSF_ADDRESS@@QAEXXZ+0x76
    ```

6.  当前正在运行函数的返回地址上设置断点。 在这种情况下，返回地址的第一行上显示为 0x77F6C600。 寄信人地址等效于在第二行所示的函数偏移量 (**BuggyProgram ！OpenDestFileStream + 0xB3**)。 如果没有符号可用于应用程序，函数名称可能不会显示。 使用[ **g （转向）** ](g--go-.md)命令以执行，直到达到此寄信人地址时，使用符号或十六进制的地址：
    ```dbgcmd
    0:002> g BuggyProgram!OpenDestFileStream+0xb3
    ```

7.  如果此断点被命中，重复该过程。 例如，假设命中此断点。 应执行以下步骤：

    ```dbgcmd
    0:002> kb
    FramePtr  RetAddr   Param1   Param2   Param3   Function Name
    0b4ffce4  01836060  0184f440 00000001 0b4ffe20 BuggyProgram!OpenDestFileStream+0xb3
    0b4ffd20  01843eba  02b5b920 00000102 02b1e0e0 BuggyProgram!SaveMsgToDestFolder+0xb3
    0b4ffe20  01855924  0b4ffef0 00145970 0b4ffef0 BuggyProgram!DispatchToConn+0xa4
    0b4ffe5c  77e112e6  01843e16 0b4ffef0 0b4fff34 RPCRT4!DispatchToStubInC+0x34
    0b4ffeb0  77e11215  0b4ffef0 00000000 0b4fff34 RPCRT4!?DispatchToStubWorker@RPC_INTERFACE@@AAEJPAU_RPC_MESSAGE@@IPAJ@Z+0xb0
    0b4ffed0  77e1a3b1  0b4ffef0 00000000 0b4fff34 RPCRT4!?DispatchToStub@RPC_INTERFACE@@QAEJPAU_RPC_MESSAGE@Z+0x41
    0b4fff40  77e181e4  02b1e0b0 00000074 0b4fff90 RPCRT4!?ReceiveOriginalCall@OSF_SCONNECTION@Z+0x14b
    0b4fff60  77e1a5df  02b1e0b0 00000074 00149210 RPCRT4!?DispatchPacket@OSF_SCONNECTION@+0x91
    0b4fff90  77e1ac1c  77e15eaf 00149210 0b4fffec RPCRT4!?ReceiveLotsaCalls@OSF_ADDRESS@@QAEXXZ+0x76

    0:002> g BuggyProgram!SaveMsgToDestFolder+0xb3
    ```

    如果此被命中，继续学习：

    ```dbgcmd
    0:002> kb
    FramePtr  RetAddr   Param1   Param2   Param3   Function Name
    0b4ffd20  01843eba  02b5b920 00000102 02b1e0e0 BuggyProgram!SaveMsgToDestFolder+0xb3
    0b4ffe20  01855924  0b4ffef0 00145970 0b4ffef0 BuggyProgram!DispatchToConn+0xa4
    0b4ffe5c  77e112e6  01843e16 0b4ffef0 0b4fff34 RPCRT4!DispatchToStubInC+0x34
    0b4ffeb0  77e11215  0b4ffef0 00000000 0b4fff34 RPCRT4!?DispatchToStubWorker@RPC_INTERFACE@@AAEJPAU_RPC_MESSAGE@@IPAJ@Z+0xb0
    0b4ffed0  77e1a3b1  0b4ffef0 00000000 0b4fff34 RPCRT4!?DispatchToStub@RPC_INTERFACE@@QAEJPAU_RPC_MESSAGE@Z+0x41
    0b4fff40  77e181e4  02b1e0b0 00000074 0b4fff90 RPCRT4!?ReceiveOriginalCall@OSF_SCONNECTION@Z+0x14b
    0b4fff60  77e1a5df  02b1e0b0 00000074 00149210 RPCRT4!?DispatchPacket@OSF_SCONNECTION@+0x91
    0b4fff90  77e1ac1c  77e15eaf 00149210 0b4fffec RPCRT4!?ReceiveLotsaCalls@OSF_ADDRESS@@QAEXXZ+0x76

    0:002> g BuggyProgram!DispatchToConn+0xa4
    ```

8.  最后，您将发现则不会命中断点。 在这种情况下，您应该假定上次**g**命令，将运行目标和它不会中断。 这意味着**SaveMsgToDestFolder()** 函数将永远不会返回。

9.  再次分解成线程，并设置一个断点**BuggyProgram ！SaveMsgToDestFolder + 0xB3**与[**最佳实践 （设置断点）** ](bp--bu--bm--set-breakpoint-.md)命令。 然后，使用**g**重复命令。 如果立即命中此断点，而不考虑多少次执行目标，它是很有可能您确定了有问题的函数：
    ```dbgcmd
    0:002> bp BuggyProgram!SaveMsgToDestFolder+0xb3

    0:002> g 

    0:002> g 
    ```

10. 使用[ **p （步骤）** ](p--step-.md)命令以查看该函数，直到识别的指令循环序列所在的位置。 然后可以分析应用程序的源代码，以确定原因，旋转线程。 原因将通常就会造成问题的逻辑**虽然**，**执行-时**， **goto**，或**为**循环。

 

 





