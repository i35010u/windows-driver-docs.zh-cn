---
title: RPC 调试概述
description: RPC 调试概述
keywords:
- RPC 调试，概述
- '远程过程调用 (RPC) '
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: be3925bc5e119652fafe79f9ed3aa7ba320d298d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96828861"
---
# <a name="overview-of-rpc-debugging"></a>RPC 调试概述


## <span id="ddk_overview_of_rpc_debugging_dbg"></span><span id="DDK_OVERVIEW_OF_RPC_DEBUGGING_DBG"></span>


通过 Microsoft 远程过程调用 (RPC) 可以轻松地跨进程和计算机边界并携带数据。 这种网络编程标准是 Microsoft Windows 的网络功能非常强大的一个原因。

但是，由于 RPC 会隐藏单个进程的网络调用，因此它掩盖了计算机之间的交互的详细信息。 这可能很难确保线程执行操作的原因，或者无法执行应执行的操作。 因此，对 RPC 错误进行调试和故障排除可能比较困难。 此外，大多数出现 RPC 错误的问题都是配置问题、网络连接问题或其他组件问题。

适用于 Windows 的调试工具包含一个名为 DbgRpc 的工具，以及与 RPC 相关的调试器扩展。 这些问题可用于分析 Windows XP 和更高版本的 Windows 上的各种 RPC 问题。

可以将这些 Windows 版本配置为保存 RPC 运行时状态信息。 可以保存不同数量的状态信息;这样您就可以获得所需的信息，而不会给您的计算机带来很大的负担。 有关详细信息，请参阅 [启用 RPC 状态信息](enabling-rpc-state-information.md) 。

然后，可以通过调试器或 DbgRpc 工具访问此信息。 在每种情况下，都可以使用查询的集合。 有关详细信息，请参阅 [显示 RPC 状态信息](displaying-rpc-state-information.md) 。

在许多情况下，你可以通过使用 [常见 RPC 调试技术](common-rpc-debugging-techniques.md)中所述的技术对问题进行故障排除。

如果你想要了解如何存储此信息，或者如果你想要设计自己的状态信息分析方法，请参阅 [RPC 状态信息内部](rpc-state-information-internals.md)。

 

 





