---
title: RPC 调试概述
description: RPC 调试概述
ms.assetid: 21db61fe-a4a1-45d3-9026-f58aecd3a3bc
keywords:
- RPC 调试概述
- 远程过程调用 (RPC)
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7b9632cb274dcc8b2658c111e31e883f30dce57c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56569419"
---
# <a name="overview-of-rpc-debugging"></a>RPC 调试概述


## <span id="ddk_overview_of_rpc_debugging_dbg"></span><span id="DDK_OVERVIEW_OF_RPC_DEBUGGING_DBG"></span>


Microsoft 远程过程调用 (RPC) 轻松跨进程和计算机边界和实施周围的数据。 此网络编程标准是，与 Microsoft Windows 的网络是如此强大的原因之一。

但是，因为 RPC 隐藏从单个进程的网络调用，它会遮盖的计算机之间的交互的详细信息。 这会使硬确保为什么线程在做他们正在做-或操作是将要执行失败。 因此，调试和故障排除 RPC 错误可能很困难。 此外，大多数似乎是 RPC 错误的问题是实际配置问题，或网络连接问题或其他组件问题。

调试工具的 Windows 包含一个称为 DbgRpc，作为也为 RPC 相关的调试器扩展的工具。 这些可用于分析各种 Windows XP 上的 RPC 问题和更高版本的 Windows。

这些 Windows 版本可以配置为保存 RPC 运行时状态信息。 可以保存不同数量的状态信息;这样，你可以获取所需而无需带来沉重的负担置于您的计算机的信息。 请参阅[启用 RPC 状态信息](enabling-rpc-state-information.md)有关详细信息。

然后可以通过调试器或 DbgRpc 工具访问此信息。 在每种情况下，查询的集合是可用的。 请参阅[显示 RPC 状态信息](displaying-rpc-state-information.md)有关详细信息。

在许多情况下，可以通过使用中所述的技术排查问题[常见 RPC 调试技术](common-rpc-debugging-techniques.md)。

如果你想要浏览此信息的存储方式的机制，或如果你想要设计您自己的状态信息分析的技术，请参阅[RPC 状态信息内部](rpc-state-information-internals.md)。

这些工具和技术不适用于 Windows 2000。

 

 





