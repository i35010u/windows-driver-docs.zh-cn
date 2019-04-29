---
title: 获取 RPC 线程信息
description: 获取 RPC 线程信息
ms.assetid: 4cb8d11f-5b0a-4526-9f64-ee69fd15d1ba
keywords:
- RPC 线程信息
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: cbee1913f1dd40f0d4a27809e611f781a2d1bde7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380791"
---
# <a name="get-rpc-thread-information"></a>获取 RPC 线程信息


## <span id="ddk_get_rpc_thread_information_dbg"></span><span id="DDK_GET_RPC_THREAD_INFORMATION_DBG"></span>


通过显示线程信息 **！ rpcexts.getthreadinfo**扩展，或通过 DbgRpc 时 **-t**使用开关。

必须指定进程的 PID。 你可以指定该进程也内的线程。 如果省略该线程，则将显示该进程内的所有线程。

在以下示例中，进程 ID 是 0x278，省略的线程 ID:

```console
D:\wmsg>dbgrpc -t -P 278
Searching for thread info ...
## PID  CELL ID   ST TID      LASTTIME
-----------------------------------
0278 0000.0002 01 000001a4 00072c09
0278 0000.0005 03 0000031c 00072bf5
```

可选参数的详细信息，请参阅[ **DbgRpc 命令行选项**](dbgrpc-command-line-options.md)。

有关使用 RPC 的类似示例调试器扩展，请参阅[ **！ rpcexts.getthreadinfo**](-rpcexts-getthreadinfo.md)。

 

 





