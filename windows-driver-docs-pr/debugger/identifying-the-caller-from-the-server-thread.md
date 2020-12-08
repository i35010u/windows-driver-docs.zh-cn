---
title: 识别服务器线程中的调用方
description: 识别服务器线程中的调用方
keywords:
- RPC 调试，标识调用方
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 50c1f0d60afb8fa928a7b094f58f4ee6a7cbfe49
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96814569"
---
# <a name="identifying-the-caller-from-the-server-thread"></a>识别服务器线程中的调用方


## <span id="ddk_identifying_the_caller_from_the_server_thread_dbg"></span><span id="DDK_IDENTIFYING_THE_CALLER_FROM_THE_SERVER_THREAD_DBG"></span>


即使您拥有的信息是为调用提供服务的服务器线程，也可以确定执行给定 RPC 调用的操作。

这可能非常有用，例如，要找出谁向 RPC 调用传递无效参数。

根据此特定调用所使用的协议顺序，您可以获得不同的详细程度。 某些协议 (如 NetBios) 根本没有此信息。

**从服务器线程标识调用方**

1.  使用服务器线程作为目标启动用户模式调试器。

2.  使用 [**| (进程状态)**](---process-status-.md) 命令获取进程 ID：
    ```dbgcmd
    0:001> |
      0     id: 3d4 name: rtsvr.exe
    ```

3.  使用 [**！ rpcexts**](-rpcexts-getcallinfo.md) 扩展名获取此进程中的活动调用。  (参见参考页获取语法说明。 ) 需要提供0x3D4 的进程 ID：

    ```dbgcmd
    0:001> !rpcexts.getcallinfo 0 0 FFFF 3d4
    Searching for call info ...
    PID  CELL ID   ST PNO IFSTART  THRDCELL  CALLFLAG CALLID   LASTTIME CONN/CLN
    ----------------------------------------------------------------------------
    03d4 0000.0004 02 000 19bb5061 0000.0002 00000001 00000001 00a1aced 0000.0003
    ```

    查找状态为02或 01 (的调用) 已调度或处于活动状态。 在此示例中，该进程只有一个调用。 如果有更多的信息，则必须对 THRDCELL 列中的单元号码使用 [**！ getdbgcell**](-rpcexts-getdbgcell.md) 扩展。 这将允许你检查线程 Id，以便确定你感兴趣的调用。

4.  知道您感兴趣的调用后，请查看 CONN/CLN 列中的单元编号。 这是连接对象的单元 ID。 在这种情况下，单元号码为0000.0003。 将此单元格数字和进程 ID 传递到 **！ rpcexts。 getdbgcell**：
    ```dbgcmd
    0:001> !rpcexts.getdbgcell 3d4 0.3
    Getting cell info ...
    Connection
    Connection flags: Exclusive
    Authentication Level: Default
    Authentication Service: None
    Last Transmit Fragment Size: 24 (0x6F56D)
    Endpoint for the connection: 0x0.1
    Last send time (in seconds since boot):10595.565 (0x2963.235)
    Last receive time (in seconds since boot):10595.565 (0x2963.235)
    Getting endpoint info ...
    Process object for caller is 0xFF9DF5F0
    ```

此扩展将显示有关此连接的客户端的所有可用信息。 实际信息量会有所不同，具体取决于所使用的传输。

在此示例中，将使用本地命名管道作为传输，并显示调用方的进程对象地址。 如果将内核调试器附加 (或启动本地内核调试器) ，则可以使用 [**！进程**](-process.md) 扩展解释此进程地址。

如果将 LRPC 用作传输，则将显示调用方的进程 ID 和线程 ID。

如果使用 TCP 作为传输，则将显示调用方的 IP 地址。

如果使用远程命名管道作为传输，则将不会提供任何信息。

**注意**   前面的示例演示了在知道服务器线程的情况如何查找客户端线程。 有关反向方法的示例，请参阅 [分析停滞调用问题](analyzing-a-stuck-call-problem.md)。

 

 

 





