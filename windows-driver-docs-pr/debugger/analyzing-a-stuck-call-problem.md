---
title: 分析调用阻塞问题
description: 分析调用阻塞问题
keywords:
- RPC 调试，停滞调用
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: f17e2428a320af84be7dffa9644ce6cde010f29d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96832013"
---
# <a name="analyzing-a-stuck-call-problem"></a>分析调用阻塞问题


## <span id="ddk_analyzing_a_stuck_call_problem_dbg"></span><span id="DDK_ANALYZING_A_STUCK_CALL_PROBLEM_DBG"></span>


当进程在持有关键部分或资源的同时直接或间接调用 RPC 时，会出现一个常见问题。 在这种情况下，RPC 调用将转到另一个进程或计算机，并调度到管理器例程 (server 例程) ，然后挂起或耗时太长。 这会导致原始调用方遇到关键部分超时。

通过调试器检查时，RPC 位于拥有临界区的线程的堆栈顶层，但并不清楚它的等待时间。

下面是此类堆栈的一个示例。 可能有很多变化。

```dbgcmd
0:002> ~1k
ChildEBP RetAddr
0068fba0 77e9e8eb ntdll!ZwWaitForSingleObject+0xb
0068fbc8 4efeff73 KERNEL32!WaitForSingleObjectEx+0x5a
0068fbe8 4eff0012 RPCRT4!UTIL_WaitForSyncIO+0x21
0068fc0c 4efe6e2b RPCRT4!UTIL_GetOverlappedResultEx+0x44
0068fc44 4ef973bf RPCRT4!WS_SyncRecv+0x12a
0068fc68 4ef98d5a RPCRT4!OSF_CCONNECTION__TransSendReceive+0xcb
0068fce4 4ef9b682 RPCRT4!OSF_CCONNECTION__SendFragment+0x297
0068fd38 4ef9a5a8 RPCRT4!OSF_CCALL__SendNextFragment+0x272
0068fd88 4ef9a9cb RPCRT4!OSF_CCALL__FastSendReceive+0x165
0068fda8 4ef9a7f8 RPCRT4!OSF_CCALL__SendReceiveHelper+0xed
0068fdd4 4ef946a7 RPCRT4!OSF_CCALL__SendReceive+0x37
0068fdf0 4efd56b3 RPCRT4!I_RpcSendReceive+0xc4
0068fe08 01002850 RPCRT4!NdrSendReceive+0x4f
0068ff40 01001f32 rtclnt+0x2850
0068ffb4 77e92ca8 rtclnt+0x1f32
0068ffec 00000000 KERNEL32!CreateFileA+0x11b
```

下面介绍如何解决此问题。

 **解决停滞呼叫问题**

1.  请确保调试器正在调试拥有粘滞单元的进程。  (这是包含怀疑 RPC 中挂起的客户端线程的进程 ) 

2.  获取此线程的堆栈指针。 堆栈将与前面的示例中所示的堆栈类似。 在此示例中，堆栈指针是0x0068FBA0。

3.  获取此线程的调用信息。 若要执行此操作，请使用带有线程堆栈指针的 [**！ rpcreadstack**](-rpcexts-rpcreadstack.md) 扩展作为其参数，如下所示：

    ```dbgcmd
    0:001> !rpcexts.rpcreadstack 68fba0
    CallID: 1
    IfStart: 19bb5061
    ProcNum: 0
            Protocol Sequence:      "ncacn_ip_tcp"  (Address: 00692ED8)
            NetworkAddress: ""      (Address: 00692F38)
            Endpoint:       "1120"  (Address: 00693988)
    ```

    此处显示的信息将允许你跟踪呼叫。

4.  "网络地址" 为空，表示本地计算机。 终结点为1120。 需要确定承载此终结点的进程。 为此，可将此终结点编号传递到 [**！ rpcexts getendpointinfo**](-rpcexts-getendpointinfo.md) 扩展，如下所示：

    ```dbgcmd
    0:001> !rpcexts.getendpointinfo 1120
    Searching for endpoint info ...
    PID  CELL ID   ST PROTSEQ        ENDPOINT
    --------------------------------------------
    0278 0000.0001 01            TCP 1120
    ```

5.  通过上述信息，可以看到进程0x278 包含此终结点。 你可以通过使用 [**！ rpcexts. getcallinfo**](-rpcexts-getcallinfo.md) 扩展来确定此进程是否知道此调用的任何内容。 此扩展需要四个参数： *CallID*、 *IfStart* 和 *ProcNum* (，它们是在步骤3中找到的) 和0x278 的 *ProcessID* ：

    ```dbgcmd
    0:001> !rpcexts.getcallinfo 1 19bb5061 0 278
    Searching for call info ...
    PID  CELL ID   ST PNO IFSTART  TIDNUMBER CALLFLAG CALLID   LASTTIME CONN/CLN
    ----------------------------------------------------------------------------
    0278 0000.0004 02 000 19bb5061 0000.0002 00000001 00000001 00072c09 0000.0003
    ```

6.  步骤5中的信息很有用，但略有简化。 单元 ID 在第二列中指定为0000.0004。 如果将进程 ID 和此单元格编号传递到 [**！ rpcexts; getdbgcell**](-rpcexts-getdbgcell.md) 扩展，则会看到此单元格的可读性更高：

    ```dbgcmd
    0:001> !rpcexts.getdbgcell 278 0.4
    Getting cell info ...
    Call
    Status: Dispatched
    Procedure Number: 0
    Interface UUID start (first DWORD only): 19BB5061
    Call ID: 0x1 (1)
    Servicing thread identifier: 0x0.2
    Call Flags: cached
    Last update time (in seconds since boot):470.25 (0x1D6.19)
    Owning connection identifier: 0x0.3
    ```

    这表明调用处于 "已调度" 状态，这意味着已离开 RPC 运行时。 上次更新时间为470.25。 你可以通过使用 [**！ rpcexts**](-rpcexts-rpctime.md) 扩展名来了解当前时间：

    ```dbgcmd
    0:001> !rpcexts.rpctime
    Current time is: 6003, 422
    ```

    这表明，与此调用的最后一次联系大约为5533秒，即约92分钟。 因此，这必须是停滞调用。

7.  在将调试器附加到服务器进程之前的最后一步，你可以使用服务线程标识符隔离当前应该为调用提供服务的线程。 这是另一个单元号码;它在步骤6中显示为 "0x 0.2"。 可以按以下方式使用它：

    ```dbgcmd
    0:001> !rpcexts.getdbgcell 278 0.2
    Getting cell info ...
    Thread
    Status: Dispatched
    Thread ID: 0x1A4 (420)
    Last update time (in seconds since boot):470.25 (0x1D6.19)
    ```

    现在，你已了解正在查找进程0x278 中的线程0x1A4。

线程可能会进行另一个 RPC 调用。 如果需要，可以通过重复此过程来跟踪此调用。

**注意**   此过程说明如何在知道客户端线程的情况下查找服务器线程。 有关反向方法的示例，请参阅 [从服务器线程标识调用方](identifying-the-caller-from-the-server-thread.md)。

 

 

 





