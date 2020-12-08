---
title: 通过调试器进行远程调试
description: 通过调试器进行远程调试
keywords:
- 通过调试器进行远程调试
- 通过调试器进行远程调试，概述
- 调试客户端
- 调试服务器
- 'TCP (远程调试协议) '
- 'COM 端口 (远程调试协议) '
- '调制解调器 (远程调试协议) '
- 命名管道 (远程 debuggi
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9c42083c66905f68f227284919eef07eb4df8c8a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96831943"
---
# <a name="remote-debugging-through-the-debugger"></a>通过调试器进行远程调试


## <span id="ddk_remote_debugging_through_the_debugger_dbg"></span><span id="DDK_REMOTE_DEBUGGING_THROUGH_THE_DEBUGGER_DBG"></span>


直接通过调试器进行远程调试通常是执行远程调试的最佳且最简单的方法。

此方法涉及在不同位置运行两个调试器。 实际执行调试的调试器称为 *调试服务器*。 从距离控制会话的调试器称为 *调试客户端*。

这两台计算机不需要运行相同版本的 Windows;它们可以运行任何版本的 Windows。 实际使用的调试器不需要相同;WinDbg 调试客户端可以连接到 CDB 调试服务器，等等。

不过，最好是两台计算机上的调试器二进制文件都来自 Windows 包的相同版本的调试工具，或者至少从最新版本开始。

若要设置此远程会话，首先设置调试服务器，然后激活调试客户端。 任意数量的调试客户端都可以连接到调试服务器。 单个调试器可以同时将自身转换为多个调试服务器，以促进不同类型的连接。

但是，没有任何一个调试器可以同时作为调试客户端和调试服务器。

本节包括：

[激活调试服务器](activating-a-debugging-server.md)

[搜索调试服务器](searching-for-debugging-servers.md)

[激活调试客户端](activating-a-debugging-client.md)

[客户端和服务器示例](client-and-server-examples.md)

[控制远程调试会话](controlling-a-remote-debugging-session.md)

 

 





