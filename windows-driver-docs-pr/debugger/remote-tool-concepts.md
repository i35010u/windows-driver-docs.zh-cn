---
title: 远程工具的概念
description: 远程工具的概念
keywords:
- 远程工具、远程工具概念
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1159e10277b2aea03a8a93be5d25651d434427f6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96788759"
---
# <a name="remote-tool-concepts"></a>远程工具的概念


## <span id="ddk_remote_tool_concepts_dtools"></span><span id="DDK_REMOTE_TOOL_CONCEPTS_DTOOLS"></span>


远程工具中使用了以下概念。

### <a name="span-idclient_and_serverspanspan-idclient_and_serverspanclient-and-server"></a><span id="client_and_server"></span><span id="CLIENT_AND_SERVER"></span>客户端和服务器

远程工具使用客户端-服务器范例来避免使用 *本地* 和 *远程* 语言，这是在有多个用户和多台计算机时可能会造成混淆的相对术语。

在客户端和服务器计算机上键入的命令将显示在这两台计算机的命令提示符窗口中。

### <a name="span-idthe_serverspanspan-idthe_serverspanthe-server"></a><span id="the_server"></span><span id="THE_SERVER"></span>服务器

*服务器* 是运行控制台程序的计算机。 *远程服务器* 是在服务器上运行的远程工具的实例。 服务器建立远程会话并将其命名为 (命名管道) ，发出命令以启动控制台程序，并确定允许谁连接到该会话。

### <a name="span-idthe_clientspanspan-idthe_clientspanthe-client"></a><span id="the_client"></span><span id="THE_CLIENT"></span>客户端

*客户端* 是向控制台程序发送命令的远程计算机。 *远程客户端* 是客户端计算机上运行的远程工具的实例。 客户端连接到服务器建立的远程会话，并使用远程会话 (命名管道) ，该服务器创建的命令将命令发送到在服务器上运行的控制台程序中。

远程工具支持每个远程会话中的多个客户端。 每个客户端都在运行一个远程客户端。 所有客户端都可以将命令发送到服务器上运行的控制台程序，并且所有客户端都可以看到发送的命令和输出。

### <a name="span-idvisible-sessionspanspan-idvisible_sessionspanvisible-session"></a><span id="visible-session"></span><span id="VISIBLE_SESSION"></span>可见会话

当远程会话 *可见* 时，它们将出现在计算机上的远程会话列表中。 若要显示列表，请使用 [**远程服务器查询命令**](remote-server-query-command.md) (**/q**) 。

默认情况下，只有调试器会话可见，即 *Command* 参数的值包括 **kd**、 **dbg**、 **remoteds**、 **ntsd** 或 **cdb** 的会话;否则，会话将不可见。 *命令* 参数是服务器上的远程工具命令的一部分。

若要使会话可见，请将 **/v** 参数添加到 [**远程服务器**](remote-server-syntax.md) 命令。 若要使调试器会话不可见，请将 **/-v** 参数添加到命令中。

有关远程服务器查询命令的帮助，请参阅 [**远程服务器查询命令**](remote-server-query-command.md)。

 

 





