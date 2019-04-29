---
title: 远程服务器查询命令
description: 若要显示的本地或远程服务器上可用的会话的列表，请使用以下语法。
ms.assetid: c95114a3-2ff5-456b-90e2-4d7bc6346f1f
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
ms.openlocfilehash: d98ff180d451e52e4f2e4e2b11b3c1240d95d37c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63353525"
---
# <a name="remote-server-query-command"></a>远程服务器查询命令


若要显示的本地或远程服务器上可用的会话的列表，请使用以下语法。

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

但是，当在计算机上运行的仅远程会话不可见的远程会话时，远程工具将显示以下消息：

```console
No visible sessions on server \\Computer
```

 

 





