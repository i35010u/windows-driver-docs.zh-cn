---
title: 获取 RPC 单元信息
description: 获取 RPC 单元信息
keywords:
- RPC 单元信息
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: a438f2f47599b10d04a782391928968c07c9542e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96816339"
---
# <a name="get-rpc-cell-information"></a>获取 RPC 单元信息


## <span id="ddk_get_rpc_cell_information_dbg"></span><span id="DDK_GET_RPC_CELL_INFORMATION_DBG"></span>


当使用 **-l** 开关时，详细的单元信息将由 **！ rpcexts. Getdbgcell** 扩展或 DbgRpc 显示。

必须指定包含首选单元的进程的进程 ID 以及单元号码。

在下面的示例中，进程 ID 为0x278，单元号码为0000.0002：

```console
D:\wmsg>dbgrpc -l -P 278 -L 0.2
Getting cell info ...
Thread
Status: Dispatched
Thread ID: 0x1A4 (420)
Last update time (in seconds since boot):470.25 (0x1D6.19)
```

有关可选参数的详细信息，请参阅 [**DbgRpc Command-Line Options**](dbgrpc-command-line-options.md)。

有关使用 RPC 调试器扩展的类似示例，请参阅 [**！ rpcexts. getdbgcell**](-rpcexts-getdbgcell.md)。

 

 





