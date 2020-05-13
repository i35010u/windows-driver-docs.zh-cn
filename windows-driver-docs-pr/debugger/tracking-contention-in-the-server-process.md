---
title: 跟踪服务器进程中的争用
description: 跟踪服务器进程中的争用
ms.assetid: ef0c0294-a010-439b-82dd-25148e05a7f1
keywords:
- RPC 调试，跟踪争用
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 935cad63601665b2f24e98809497c48514600e61
ms.sourcegitcommit: 958a5ced83856df22627c06eb42c9524dd547906
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/12/2020
ms.locfileid: "83235422"
---
# <a name="tracking-contention-in-the-server-process"></a>跟踪服务器进程中的争用


## <span id="ddk_tracking_contention_in_the_server_process_dbg"></span><span id="DDK_TRACKING_CONTENTION_IN_THE_SERVER_PROCESS_DBG"></span>


为了为传入请求服务，RPC 将维护一组工作线程。 理想情况下，线程数会很小。 但是，这种理想情况只会出现在实验室环境中，其中服务器管理器例程经过仔细优化。 在实际情况下，线程数会因服务器工作负荷而异，但它可以在1到50之间。

如果工作线程数超过50，则服务器进程的争用可能会过多。 导致此问题的常见原因是 icriminate 使用堆、内存不足或通过单个关键部分序列化服务器中的大部分活动。

若要查看给定服务器进程中的线程数，请使用[**！ rpcexts. getthreadinfo**](-rpcexts-getthreadinfo.md)扩展，或将 DbgRpc 与 **-t**开关一起使用。 提供进程 ID （在以下示例中为0xC4）：

```console
D:\wmsg>dbgrpc -t -P c4
Searching for thread info ...
## PID  CELL ID   ST TID      LASTTIME
-----------------------------------
00c4 0000.0004 03 0000011c 000f164f
00c4 0000.0007 03 00000120 008a6290
00c4 0000.0015 03 0000018c 008a6236
00c4 0000.0026 03 00000264 0005c443
00c4 0000.002d 03 00000268 000265bb
00c4 0000.0030 03 0000026c 000f1d32
00c4 0000.0034 03 00000388 007251e9
```

在这种情况下，只有七个工作线程是合理的。

如果有超过100个线程，则调试器应附加到此进程，并调查原因。

**注意**   远程运行查询（如**dbgrpc）** 在服务器和网络上非常昂贵。 如果在脚本中使用此查询，应确保此命令运行不太频繁。

 

 

 





