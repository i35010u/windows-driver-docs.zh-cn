---
title: 标识服务器线程从调用方
description: 标识服务器线程从调用方
ms.assetid: d19dc242-1043-4e61-9fcb-eadac0ab63c8
keywords:
- RPC 调试、 标识调用方
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: ecea5be6fff755074eebc25c1fc64dcf56af8dc5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544505"
---
# <a name="identifying-the-caller-from-the-server-thread"></a>标识服务器线程从调用方


## <span id="ddk_identifying_the_caller_from_the_server_thread_dbg"></span><span id="DDK_IDENTIFYING_THE_CALLER_FROM_THE_SERVER_THREAD_DBG"></span>


就可以确定哪些操作对给定的 RPC 调用，即使您拥有的唯一信息是提供服务调用的服务器线程。

这可能非常有用-例如，若要找出谁传递给 RPC 调用的参数无效。

具体取决于哪个协议序列可供此特定的调用，可以获取不同程度的详细信息。 某些协议 （如 NetBios) 不在所有具有此信息。

**标识服务器线程从调用方**

1.  启动用户模式下调试程序与服务器线程作为目标。

2.  使用获取的进程 ID [ **|（进程状态）** ](---process-status-.md)命令：
    ```dbgcmd
    0:001> |
      0     id: 3d4 name: rtsvr.exe
    ```

3.  使用此过程中获取活动调用[ **！ rpcexts.getcallinfo** ](-rpcexts-getcallinfo.md)扩展。 （请参阅有关语法的说明的参考页。）需要提供 0x3D4 的进程 ID:

    ```dbgcmd
    0:001> !rpcexts.getcallinfo 0 0 FFFF 3d4
    Searching for call info ...
    PID  CELL ID   ST PNO IFSTART  THRDCELL  CALLFLAG CALLID   LASTTIME CONN/CLN
    ----------------------------------------------------------------------------
    03d4 0000.0004 02 000 19bb5061 0000.0002 00000001 00000001 00a1aced 0000.0003
    ```

    查找状态为 02 或 01 （调度或处于活动状态） 的调用。 在此示例中，该过程仅有一次调用。 如果没有更多，您将必须使用[ **！ rpcexts.getdbgcell** ](-rpcexts-getdbgcell.md)扩展名 THRDCELL 列中的单元格号。 这样，您可以检查 Id 以便您可以确定该调用您已对感兴趣的线程。

4.  您知道您感兴趣的调用，请查看 CONN/CLN 列中的单元格号。 这是连接对象的单元格 ID。 在这种情况下，单元格号是 0000.0003。 将此单元格号和进程 ID 与传递 **！ rpcexts.getdbgcell**:
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

此扩展将显示所有可用信息有关的客户端的此连接。 实际信息的量而异，具体取决于正在使用的传输。

在此示例中，正在使用本地命名的管道作为传输协议和显示进程对象地址的调用方。 如果您附加内核调试程序 （或启动本地内核调试程序），则可以使用[ **！ 过程**](-process.md)扩展来解释此进程的地址。

如果 LRPC 用作传输，将显示进程 ID 和调用方的线程 ID。

如果使用 TCP 作为传输协议，将显示调用方的 IP 地址。

如果作为传输协议使用远程命名的管道，不将提供任何信息。

**请注意**  上面的示例演示如何查找客户端线程，如果知道服务器线程。 有关反向技术的示例，请参阅[分析停滞调用问题](analyzing-a-stuck-call-problem.md)。

 

 

 





