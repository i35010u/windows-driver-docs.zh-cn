---
title: 远程工具的概念
description: 远程工具的概念
ms.assetid: 509b25cd-d69a-442d-bd5b-a69266d341c3
keywords:
- 远程工具、 远程工具的概念
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: fd804aa61f79d37a8879387ad0a8758884302359
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63353494"
---
# <a name="remote-tool-concepts"></a>远程工具的概念


## <span id="ddk_remote_tool_concepts_dtools"></span><span id="DDK_REMOTE_TOOL_CONCEPTS_DTOOLS"></span>


远程工具中使用以下概念。

### <a name="span-idclientandserverspanspan-idclientandserverspanclient-and-server"></a><span id="client_and_server"></span><span id="CLIENT_AND_SERVER"></span>客户端和服务器

远程工具使用一个客户端-服务器范例，它可避免单词*本地*并*远程*，这都是相对的术语，当有多个用户和多台计算机时可能会造成混淆。

在客户端和服务器计算机键入的命令也显示在两台计算机的命令提示符窗口中。

### <a name="span-idtheserverspanspan-idtheserverspanthe-server"></a><span id="the_server"></span><span id="THE_SERVER"></span>在服务器

*Server*是控制台程序运行的计算机。 *远程服务器*是在服务器上运行的远程工具的实例。 服务器建立和名称 （命名管道） 的远程会话，发出命令以启动控制台程序，并确定谁有权连接到该会话。

### <a name="span-idtheclientspanspan-idtheclientspanthe-client"></a><span id="the_client"></span><span id="THE_CLIENT"></span>客户端

*客户端*是将命令发送到控制台程序的远程计算机。 *远程客户端*是远程工具客户端计算机上运行的实例。 客户端连接到远程服务器建立的会话，并使用创建的服务器将命令发送到在服务器运行的控制台程序的远程会话 （命名管道）。

每个远程会话中，远程工具支持多个客户端。 每个客户端运行一台远程客户端。 所有客户端可以将命令发送到的服务器上，运行的控制台程序，所有客户端可以看到发送命令和输出显示。

### <a name="span-idvisible-sessionspanspan-idvisiblesessionspanvisible-session"></a><span id="visible-session"></span><span id="VISIBLE_SESSION"></span>可见的会话

当远程会话都*可见*，它们出现在计算机上的远程会话的列表。 若要显示的列表，请使用[**远程服务器查询命令**](remote-server-query-command.md) (**/q**)。

默认情况下，仅调试器会话是可见的也就是说，在其中的会话的值*命令*参数包含词**kd**， **dbg**， **remoteds**， **ntsd**，或**cdb**; 否则为该会话将不可见。 *命令*参数是在服务器上的远程工具命令的一部分。

若要使会话可见，请添加 **/v**参数[**远程服务器**](remote-server-syntax.md)命令。 若要使调试器会话不可见，添加 **/v**命令参数。

远程服务器查询命令的帮助，请参阅[**远程服务器查询命令**](remote-server-query-command.md)。

 

 





