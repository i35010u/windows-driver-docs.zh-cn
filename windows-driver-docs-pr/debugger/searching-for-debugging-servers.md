---
title: 搜索调试服务器
description: 可以使用 KD 或 CDB-QR 命令行选项来获取可用的网络服务器运行的调试服务器的列表。
ms.assetid: 510d5f9a-cde8-4dc8-8e2f-80f84ad44fce
keywords:
- 搜索调试服务器 Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- Searching for Debugging Servers
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 6e3dfbf210bd28e7ff008da18015e0f24d95af58
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567509"
---
# <a name="searching-for-debugging-servers"></a>搜索调试服务器


可以使用 KD 或与 CDB **-QR**命令行选项来获取可用的网络服务器运行的调试服务器的列表。

此列表可能包含不再存在的服务器，但这不正确关闭-连接到其中一种生成一条错误消息。 列表还将包括的进程服务器和 KD 连接服务器。 每种情况下，将指示该服务器类型。

此语法如下所示：

```console
Debugger -QR \\Server 
```

## <span id="ddk_searching_for_debugging_servers_dbg"></span><span id="DDK_SEARCHING_FOR_DEBUGGING_SERVERS_DBG"></span>


*调试器*可以是 KD 或 CDB-显示将在任一情况下相同。 两个反斜杠 (**\\\\**) 前面*Server*都是可选的。

在 WinDbg 中，可以使用**连接到远程调试器会话**对话框浏览可用服务器的列表。 请参阅[文件 |连接到远程会话](file---connect-to-remote-session.md)有关详细信息。

**请注意**  对于调试服务器可供检测，则必须激活使用提升的权限。 有关详细信息，请参阅[激活调试服务器](activating-a-debugging-server.md)。

 

**请注意**  如果未登录到客户端计算机与有权访问服务器计算机帐户，你可能需要提供用户名和密码。 在客户端计算机上，在命令提示符窗口中，输入以下命令。

**使用 net \\ \\**  <em>Server</em>**\\ipc$ /user:**<em>用户名</em>其中*Server*是服务器计算机的名称和*用户名*是有权访问服务器计算机帐户的名称。

当系统提示输入的密码*用户名*。

此命令成功后，可以通过使用发现 （在服务器计算机上运行） 的调试服务器 **-QR**或**连接到远程调试器会话**。

 

 

 





