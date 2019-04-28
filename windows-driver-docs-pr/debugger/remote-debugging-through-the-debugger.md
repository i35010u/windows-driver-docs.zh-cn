---
title: 通过调试器进行远程调试
description: 通过调试器进行远程调试
ms.assetid: a9f6f355-e684-471f-a45c-b2235a5372b1
keywords:
- 远程执行调试程序调试
- 通过调试器，远程调试概述
- 调试客户端
- 调试服务器
- TCP （远程调试协议）
- COM 端口 （远程调试协议）
- 调制解调器 （远程调试协议）
- 命名的管道 (远程 debuggi
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: dcfd0480df9e266b7bd46c6a775ff0587c2de14d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63353579"
---
# <a name="remote-debugging-through-the-debugger"></a>通过调试器进行远程调试


## <span id="ddk_remote_debugging_through_the_debugger_dbg"></span><span id="DDK_REMOTE_DEBUGGING_THROUGH_THE_DEBUGGER_DBG"></span>


直接通过调试器的远程调试通常是执行远程调试的最佳和最简单的方法。

这种策略涉及的不同位置运行两个调试器。 调用实际执行调试调试器*调试服务器*。 调用调试器，控制会话在远处*调试客户端*。

两台计算机不需要运行相同版本的 Windows;它们可以运行任何版本的 Windows。 使用实际调试器不需要相同;WinDbg 调试客户端可以连接到 CDB 调试服务器，依次类推。

但是，最好是在两台计算机这两个调试程序二进制文件是从相同版本的调试工具对于 Windows 包，或在最少同时从最新版本。

若要设置此远程会话，在调试服务器设置第一个，并调试客户端激活。 任意数量的调试客户端可以连接到的调试服务器。 单个调试器可以将自身转换多个调试服务器在同一时间，以便于不同类型的连接。

但是，任何单个调试器可以不在调试客户端和调试服务器同时。

本部分包括：

[激活调试服务器](activating-a-debugging-server.md)

[调试服务器搜索](searching-for-debugging-servers.md)

[激活调试客户端](activating-a-debugging-client.md)

[客户端和服务器示例](client-and-server-examples.md)

[控制远程调试会话](controlling-a-remote-debugging-session.md)

 

 





