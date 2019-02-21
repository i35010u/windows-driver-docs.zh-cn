---
title: 显示 RPC 状态信息
description: 显示 RPC 状态信息
ms.assetid: 9931cf62-a7c2-4270-8664-a77a82207aa9
keywords:
- RPC 调试、 显示 RPC 状态信息
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4391d3286be2d33b5c0843d39fb9c5047fe78171
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555864"
---
# <a name="displaying-rpc-state-information"></a>显示 RPC 状态信息


## <span id="ddk_displaying_rpc_state_information_dbg"></span><span id="DDK_DISPLAYING_RPC_STATE_INFORMATION_DBG"></span>


RPC 运行时状态的所有信息都包含在单元格。 单元格是信息的可以查看和更新单独的最小单位。 DbgRpc 工具和 RPC 调试器扩展允许您以查看任何给定的单元格的内容或运行高级查询。

每个键的对象中 RPC 运行时将保持其状态信息的一个或多个单元格。 每个单元格有一个单元格的 id。 当一个对象引用另一个对象时，它是通过指定该对象的单元格 id。

RPC 运行时可以维护有关的信息的关键对象是终结点、 线程、 连接对象、 服务器调用 (SCALL) 对象和客户端调用 (CCALL) 对象。 服务器调用对象通常被当做*调用对象*。

RPC 状态信息查询生成相同的信息，无论您使用 DbgRpc 工具或 RPC 调试器扩展。 以下部分介绍如何在每个车辆中使用的查询：

[使用 RPC 调试程序扩展](using-the-rpc-debugger-extensions.md)

[使用 DbgRpc 工具](using-the-dbgrpc-tool.md)

最基本的查询只是显示的单个单元格：

[获取 RPC 单元格的信息](get-rpc-cell-information.md)

下面的高级查询均可用：

[获取 RPC 终结点信息](get-rpc-endpoint-information.md)

[获取 RPC 线程信息](get-rpc-thread-information.md)

[获取 RPC 调用信息](get-rpc-call-information.md)

[获取 RPC 客户端调用信息](get-rpc-client-call-information.md)

 

 





