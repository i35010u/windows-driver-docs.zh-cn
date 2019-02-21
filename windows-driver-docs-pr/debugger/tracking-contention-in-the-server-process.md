---
title: 跟踪中的服务器进程的争用
description: 跟踪中的服务器进程的争用
ms.assetid: ef0c0294-a010-439b-82dd-25148e05a7f1
keywords:
- RPC 调试、 跟踪争用
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 041d8a089755a25fafb2586295b787fa2776081c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547709"
---
# <a name="tracking-contention-in-the-server-process"></a>跟踪中的服务器进程的争用


## <span id="ddk_tracking_contention_in_the_server_process_dbg"></span><span id="DDK_TRACKING_CONTENTION_IN_THE_SERVER_PROCESS_DBG"></span>


为了处理传入的请求，RPC 将维护一组工作线程。 理想情况下，线程数将很小。 但是，这种理想的情况下仅出现在实验室环境中，进行了仔细调整服务器管理器例程。 在真实的情况下，具体取决于服务器工作负荷而异的线程数，但它可以是任意位置从 1 到 50。

如果工作线程数大于 50，您可能过度争用资源的服务器进程中。 此常见原因是不加选择地使用堆的内存压力或序列化的服务器通过单一的关键部分中的大多数活动。

若要查看给定的服务器进程中的线程数，请使用[ **！ rpcexts.getthreadinfo** ](-rpcexts-getthreadinfo.md)扩展，或使用与 DbgRpc **-t**切换。 提供的进程 ID （在下面的示例中，0xC4）：

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

在这种情况下，有七个工作线程，这是合理。

如果有 100 多个线程，应将调试器附加到此过程，并调查原因。

**请注意**  运行查询，如**dbgrpc t**远程是代价高昂的服务器和网络。 如果在脚本中使用此查询，应确保不经常运行此命令。

 

 

 





