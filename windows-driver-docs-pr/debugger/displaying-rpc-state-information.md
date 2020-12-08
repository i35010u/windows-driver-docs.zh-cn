---
title: 显示 RPC 状态信息
description: 显示 RPC 状态信息
keywords:
- RPC 调试，显示 RPC 状态信息
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6dd0eb963eb0ecebf33d9d404720dbc9bdc35e73
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836549"
---
# <a name="displaying-rpc-state-information"></a>显示 RPC 状态信息


## <span id="ddk_displaying_rpc_state_information_dbg"></span><span id="DDK_DISPLAYING_RPC_STATE_INFORMATION_DBG"></span>


所有 RPC 运行时状态信息都包含在单元格中。 单元是可单独查看和更新的信息的最小单位。 DbgRpc 工具和 RPC 调试器扩展都允许您查看任何给定单元的内容或运行高级查询。

RPC Run-Time 中的每个密钥对象将维护一个或多个有关其状态的信息单元。 每个单元都有一个单元 ID。 当对象引用另一对象时，它通过指定该对象的单元 ID 来实现此目的。

RPC Run-Time 可以维护的关键对象包括终结点、线程、连接对象、服务器调用 (SCALL) 对象和客户端调用 (CCALL) 对象。 服务器调用对象通常称为 *调用对象*。

无论你使用的是 DbgRpc 工具还是 RPC 调试器扩展，RPC 状态信息查询都会生成相同的信息。 以下各部分介绍如何在每个车辆中使用查询：

[使用 RPC 调试器扩展](using-the-rpc-debugger-extensions.md)

[使用 DbgRpc 工具](using-the-dbgrpc-tool.md)

最基本的查询只显示单个单元：

[获取 RPC 单元信息](get-rpc-cell-information.md)

还提供了以下高级查询：

[获取 RPC 终结点信息](get-rpc-endpoint-information.md)

[获取 RPC 线程信息](get-rpc-thread-information.md)

[获取 RPC 调用信息](get-rpc-call-information.md)

[获取 RPC 客户端调用信息](get-rpc-client-call-information.md)

 

 





