---
title: 分析调用阻塞问题
description: 分析调用阻塞问题
ms.assetid: e1a80cde-cf83-4a16-ae4b-5ddd5eb77b6d
keywords:
- RPC 调试停滞的调用
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: dfdd02f84b9bff7f826339b87ac577636ee372f6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576083"
---
# <a name="analyzing-a-stuck-call-problem"></a>分析调用阻塞问题


## <span id="ddk_analyzing_a_stuck_call_problem_dbg"></span><span id="DDK_ANALYZING_A_STUCK_CALL_PROBLEM_DBG"></span>


当某个进程持有关键节或资源时直接或间接地做出 RPC 调用，，会出现一个常见问题。 在这种情况下，RPC 调用将转到另一个进程或计算机，并将调度到 manager 例程 （server 例程），然后挂起或时间太长。 这将导致原始调用方会遇到的关键部分超时。

拥有关键部分中，线程的堆栈顶部时，通过调试程序将检查是 RPC，但不是清楚它正在等待。

下面是此类堆栈的一个示例。 可能会出现许多变体。

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

下面介绍了如何解决此问题。

 **停滞的调用问题进行故障排除**

1.  请确保调试器为调试拥有卡滞的单元格的进程。 （这是包含怀疑挂起 RPC 中的客户端线程进程。）

2.  获取此线程的堆栈指针。 堆栈将如下所示在前面的示例所示。 在此示例中，堆栈指针是 0x0068FBA0。

3.  获取此线程的调用信息。 为了做到这一点，使用[ **！ rpcexts.rpcreadstack** ](-rpcexts-rpcreadstack.md)扩展与线程作为其参数，堆栈指针，如下所示：

    ```dbgcmd
    0:001> !rpcexts.rpcreadstack 68fba0
    CallID: 1
    IfStart: 19bb5061
    ProcNum: 0
            Protocol Sequence:      "ncacn_ip_tcp"  (Address: 00692ED8)
            NetworkAddress: ""      (Address: 00692F38)
            Endpoint:       "1120"  (Address: 00693988)
    ```

    此处显示的信息将允许你跟踪调用。

4.  网络地址为空，指示在本地计算机。 终结点是 1120年。 您需要确定哪个进程承载此终结点。 这可以通过将传递到此终结点号[ **！ rpcexts.getendpointinfo** ](-rpcexts-getendpointinfo.md)扩展，按如下所示：

    ```dbgcmd
    0:001> !rpcexts.getendpointinfo 1120
    Searching for endpoint info ...
    PID  CELL ID   ST PROTSEQ        ENDPOINT
    --------------------------------------------
    0278 0000.0001 01            TCP 1120
    ```

5.  从上述信息，可以看到进程 0x278 包含此终结点。 您可以确定是否此过程就会知道任何有关此调用通过使用[ **！ rpcexts.getcallinfo** ](-rpcexts-getcallinfo.md)扩展。 此扩展插件需要四个参数：*CallID*， *IfStart*，和*ProcNum* （其中已找到在步骤 3 中），和*ProcessID* 0x278 的：

    ```dbgcmd
    0:001> !rpcexts.getcallinfo 1 19bb5061 0 278
    Searching for call info ...
    PID  CELL ID   ST PNO IFSTART  TIDNUMBER CALLFLAG CALLID   LASTTIME CONN/CLN
    ----------------------------------------------------------------------------
    0278 0000.0004 02 000 19bb5061 0000.0002 00000001 00000001 00072c09 0000.0003
    ```

6.  步骤 5 中的信息很有用，但有些缩写。 单元格 ID 作为 0000.0004 提供第二列中。 如果传递进程 ID 和为此单元格号[ **！ rpcexts.getdbgcell** ](-rpcexts-getdbgcell.md)扩展，您将看到显示的此单元格是更具可读性：

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

    这将显示在调用处于状态"调度"，这意味着是已离开 RPC 运行时。 上次更新时间是 470.25。 可通过使用了解目前[ **！ rpcexts.rpctime** ](-rpcexts-rpctime.md)扩展：

    ```dbgcmd
    0:001> !rpcexts.rpctime
    Current time is: 6003, 422
    ```

    这将显示，通过此调用的最后一个联系人以来大约 5533 秒，即大约 92 分钟。 因此，这必须是停滞的调用。

7.  最后一步将调试器附加到服务器进程之前可以隔离当前应使用服务的线程标识符服务调用的线程。 这是另一个单元格号;它在步骤 6 中显示为"0x0.2"。 可以使用它，如下所示：

    ```dbgcmd
    0:001> !rpcexts.getdbgcell 278 0.2
    Getting cell info ...
    Thread
    Status: Dispatched
    Thread ID: 0x1A4 (420)
    Last update time (in seconds since boot):470.25 (0x1D6.19)
    ```

    现在您知道您正在寻找进程 0x278 0x1A4 线程。

很可能该线程已进行另一个 RPC 调用。 如有必要，可以通过重复此过程中跟踪此调用。

**请注意**  此过程演示如何查找服务器线程，如果您知道客户端线程。 有关反向技术的示例，请参阅[标识的调用方从服务器线程](identifying-the-caller-from-the-server-thread.md)。

 

 

 





