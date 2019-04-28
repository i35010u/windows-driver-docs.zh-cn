---
title: 远程工具
description: 远程工具，Remote.exe，是的可以运行和控制远程计算机中的任何控制台程序的命令行工具。
ms.assetid: b6fbde9b-1a2a-46b8-9edc-7fa143f5a711
keywords:
- 远程工具
- Remote.exe
- Remote.exe，请参阅远程工具
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6859127b5d6f86606161440495c73ac2d0b756f8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63353487"
---
# <a name="remote-tool"></a>远程工具


远程工具，Remote.exe，是的可以运行和控制远程计算机中的任何控制台程序的命令行工具。

## <a name="span-idwheretogettheremotetoolspanspan-idwheretogettheremotetoolspanspan-idwheretogettheremotetoolspanwhere-to-get-the-remote-tool"></a><span id="Where_to_get_the_Remote_tool"></span><span id="where_to_get_the_remote_tool"></span><span id="WHERE_TO_GET_THE_REMOTE_TOOL"></span>获取远程工具的位置


中包含 Remote.exe[有关 Windows 调试工具](index.md)。

## <a name="span-idddkremotetooldtoolsspanspan-idddkremotetooldtoolsspanremote-tool-components"></a><span id="ddk_remote_tool_dtools"></span><span id="DDK_REMOTE_TOOL_DTOOLS"></span>远程工具组件


远程工具包括以下组件：

-   服务器应用程序启动一个控制台程序并打开客户端连接的命名的管道。

-   客户端应用程序与服务器建立连接。 类型化客户端计算机上的命令发送到的服务器上，控制台应用程序和远程客户端会显示服务器的控制台窗口的输出。

-   一种查询功能，其中列出了在服务器计算机上运行的远程会话。

使用远程工具，可以启动多个服务器会话，其中多个客户端可以连接到每个会话在单台计算机上。 会话仅受计算机的资源。

这是大关更复杂的工具，主要是远程桌面的较旧工具。 但是，因为它很简单，而且使用非常少的资源，它是仍然很广泛，通常用于进行远程调试。

远程工具需要，在本地和远程计算机上提交命令。 在这种情况下，若要在没有本地用户的计算机上使用此工具，必须开发另一种方法要提交命令，然后重新启动计算机，如有必要。

远程工具可以降低您的计算机上的安全，因为它不会对用户进行身份验证或使用 Microsoft Windows 权限。 默认情况下，可以连接并提供会话名称的任何远程计算机可以使用此工具创建，命名的管道，尽管可以使用远程工具选项包括和排除特定的用户和组。

本部分包括：

[远程工具的概念](remote-tool-concepts.md)

[远程工具的命令](remote-tool-commands.md)

[远程工具示例](remote-tool-examples.md)

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[Windows 调试工具中包含的工具](extra-tools.md)

 

 






