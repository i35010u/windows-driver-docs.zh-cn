---
title: 获取 RPC 线程信息
description: 获取 RPC 线程信息
keywords:
- RPC 线程信息
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 54107526dfd32b5742ba4f04a2489cd0584028a7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96816337"
---
# <a name="get-rpc-thread-information"></a>获取 RPC 线程信息


## <span id="ddk_get_rpc_thread_information_dbg"></span><span id="DDK_GET_RPC_THREAD_INFORMATION_DBG"></span>


当使用 **-t** 开关时，线程信息由 **！ rpcexts; Getthreadinfo** 扩展或 DbgRpc 显示。

必须指定进程的 PID。 您也可以在该过程中指定一个线程。 如果省略该线程，则将显示该进程中的所有线程。

在下面的示例中，进程 ID 为0x278 并且省略了线程 ID：

```console
D:\wmsg>dbgrpc -t -P 278
Searching for thread info ...
## PID  CELL ID   ST TID      LASTTIME
-----------------------------------
0278 0000.0002 01 000001a4 00072c09
0278 0000.0005 03 0000031c 00072bf5
```

有关可选参数的详细信息，请参阅 [**DbgRpc Command-Line Options**](dbgrpc-command-line-options.md)。

有关使用 RPC 调试器扩展的类似示例，请参阅 [**！ rpcexts. getthreadinfo**](-rpcexts-getthreadinfo.md)。

 

 





