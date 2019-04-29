---
title: 获取 RPC 单元信息
description: 获取 RPC 单元信息
ms.assetid: 7dd5e77e-914d-4b00-90c5-92705eebf436
keywords:
- RPC 单元信息
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3fb6b3e72b260371fc342fa6e6738b3b2d8301f2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380235"
---
# <a name="get-rpc-cell-information"></a>获取 RPC 单元信息


## <span id="ddk_get_rpc_cell_information_dbg"></span><span id="DDK_GET_RPC_CELL_INFORMATION_DBG"></span>


通过显示详细的单元格信息 **！ rpcexts.getdbgcell**扩展，或通过 DbgRpc 时 **-l**使用开关。

必须指定包含首选的单元格的进程的进程 ID，以及单元格号。

在以下示例中，进程 ID 是 0x278，和的单元格号是 0000.0002:

```console
D:\wmsg>dbgrpc -l -P 278 -L 0.2
Getting cell info ...
Thread
Status: Dispatched
Thread ID: 0x1A4 (420)
Last update time (in seconds since boot):470.25 (0x1D6.19)
```

可选参数的详细信息，请参阅[ **DbgRpc 命令行选项**](dbgrpc-command-line-options.md)。

有关使用 RPC 的类似示例调试器扩展，请参阅[ **！ rpcexts.getdbgcell**](-rpcexts-getdbgcell.md)。

 

 





