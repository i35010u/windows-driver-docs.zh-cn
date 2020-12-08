---
title: 远程会话命令
description: 远程会话命令
keywords:
- 远程工具-远程会话命令
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: f11686757b338ec14779327ce784c99c920b7670
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96791977"
---
# <a name="remote-session-commands"></a>远程会话命令


## <span id="ddk_remote_session_commands_dtools"></span><span id="DDK_REMOTE_SESSION_COMMANDS_DTOOLS"></span>


使用以下命令在控制台会话过程中与远程工具进行通信。

<span id="_H"></span><span id="_h"></span><strong>@H</strong>  
显示服务器和客户端计算机上的会话命令。 在服务器和客户端计算机上工作。

<span id="_M_Message"></span><span id="_m_message"></span><span id="_M_MESSAGE"></span><strong>@M</strong>*消息*  
显示会话中所有服务器和客户端计算机上的指定消息。 在服务器和客户端计算机上工作。

<span id="_P_Message"></span><span id="_p_message"></span><span id="_P_MESSAGE"></span><strong>@P</strong>*消息*  
使用指定的消息生成服务器计算机上的弹出窗口。 在客户端计算机上，消息显示在命令窗口中。 在服务器和客户端计算机上工作。

<span id="_Q"></span><span id="_q"></span><strong>@Q</strong>  
结束. 断开客户端计算机与会话的连接。 仅适用于客户端计算机。

<span id="_K"></span><span id="_k"></span><strong>@K</strong>  
断开所有客户端的连接并结束远程会话。 仅适用于服务器计算机。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>提出

有关示例，请参阅 [远程工具示例](remote-tool-examples.md)中的 "使用会话命令"。

在响应会话命令时，远程工具会显示一个标签，其中包含执行命令的日期和时间。 所有事件的时间显示为服务器计算机的时区。

 

 





