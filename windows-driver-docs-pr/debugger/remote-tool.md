---
title: 远程工具
description: 远程工具 Remote.exe 是一种命令行工具，可用于从远程计算机运行和控制任何控制台程序。
keywords:
- 远程工具
- Remote.exe
- Remote.exe，请参阅远程工具
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 23bc6357c8c31ce8e45aa370801bc153908596b2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96816937"
---
# <a name="remote-tool"></a>远程工具


远程工具 Remote.exe 是一种命令行工具，可用于从远程计算机运行和控制任何控制台程序。

## <a name="span-idwhere_to_get_the_remote_toolspanspan-idwhere_to_get_the_remote_toolspanspan-idwhere_to_get_the_remote_toolspanwhere-to-get-the-remote-tool"></a><span id="Where_to_get_the_Remote_tool"></span><span id="where_to_get_the_remote_tool"></span><span id="WHERE_TO_GET_THE_REMOTE_TOOL"></span>在何处获取远程工具


Remote.exe 包含在 [Windows 调试工具](index.md)中。

## <a name="span-idddk_remote_tool_dtoolsspanspan-idddk_remote_tool_dtoolsspanremote-tool-components"></a><span id="ddk_remote_tool_dtools"></span><span id="DDK_REMOTE_TOOL_DTOOLS"></span>远程工具组件


远程工具包含以下组件：

-   启动控制台程序并为客户端连接打开命名管道的服务器应用程序。

-   与服务器建立连接的客户端应用程序。 在客户端计算机上键入的命令将发送到服务器上的控制台应用程序，远程客户端将从服务器的控制台窗口中显示输出。

-   列出服务器计算机上运行的远程会话的查询功能。

使用远程工具，你可以在一台计算机上启动多个服务器会话，多个客户端可以连接到每个会话。 会话仅受计算机资源的限制。

这是一个较旧的工具，已经 eclipsed 了更复杂的工具，主要用于远程桌面。 但是，因为它很简单，只使用很少的资源，所以通常用于远程调试。

远程工具要求同时在本地和远程计算机上提交命令。 因此，若要在没有本地用户的计算机上使用此工具，必须开发一种替代方法来提交命令和重新启动计算机（如有必要）。

远程工具会损害计算机上的安全性，因为它不会对用户进行身份验证或使用 Microsoft Windows 权限。 默认情况下，任何可以连接并提供会话名称的远程计算机都可以使用此工具创建的命名管道，不过，你可以使用远程工具选项来包含和排除特定的用户和组。

本节包括：

[远程工具的概念](remote-tool-concepts.md)

[远程工具命令](remote-tool-commands.md)

[远程工具示例](remote-tool-examples.md)

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[Windows 调试工具中包含的工具](extra-tools.md)

 

 






