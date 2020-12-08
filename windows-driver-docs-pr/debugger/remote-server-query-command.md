---
title: 远程服务器查询命令
description: 若要显示本地或远程服务器上的可用会话列表，请使用以下语法。
keywords:
- 远程服务器查询命令 Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- Remote Server Query Command
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1673a5268cd1ffc68fa813459698f9bfb7b6816d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96831930"
---
# <a name="remote-server-query-command"></a>远程服务器查询命令


若要显示本地或远程服务器上的可用会话列表，请使用以下语法。

```console
remote /q Computer
```dbgcmd

## <span id="ddk_remote_server_query_command_dtools"></span><span id="DDK_REMOTE_SERVER_QUERY_COMMAND_DTOOLS"></span>Parameters


<span id="________q______"></span><span id="________Q______"></span> **/q**   
Query. Displays the visible remote sessions on the specified computer.

<span id="_______Computer______"></span><span id="_______computer______"></span><span id="_______COMPUTER______"></span> *Computer*   
Specifies the name of the computer. This parameter is required (even on the local computer).

### <span id="comments"></span><span id="COMMENTS"></span>Comments

The query display includes only server sessions; it does not display client connections to remote sessions.

The query display includes only visible sessions. There is no command to display invisible sessions.

The query display includes all visible sessions, including those that restrict users (**/u** and **/ud**). The user might not have permission to connect to all of the sessions in the list.

When there are no remote sessions running on the server, the Remote tool displays the following message:

```console
No Remote servers running on \\Computer
```

但是，当计算机上运行的唯一远程会话不可见时，远程工具会显示以下消息：

```console
No visible sessions on server \\Computer
```

 

 





