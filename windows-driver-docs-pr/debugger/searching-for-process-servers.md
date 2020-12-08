---
title: 搜索进程服务器
description: 可以将 KD 或 CDB 与-QR 命令行选项一起使用，以获取在网络服务器计算机上运行的可用进程服务器的列表。
keywords:
- 搜索进程服务器 Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- Searching for Process Servers
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 56f78f1f9a6c3d077da226dc457495fb1ddea292
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96801889"
---
# <a name="searching-for-process-servers"></a>搜索进程服务器


可以将 KD 或 CDB 与 **-QR** 命令行选项一起使用，以获取在网络服务器计算机上运行的可用进程服务器的列表。

此列表可能包含不再存在但未正确关闭的服务器--连接到其中一个将生成错误消息。 此列表还将包含调试服务器和 KD 连接服务器。 每种情况下都将指示服务器类型。

此操作的语法如下所示：

```console
Debugger -QR \\Server
```

## <span id="ddk_searching_for_process_servers_dbg"></span><span id="DDK_SEARCHING_FOR_PROCESS_SERVERS_DBG"></span>


*调试器* 可以是 KD 或 CDB，这两种情况下的显示都是相同的。 前面服务器)  (两个反斜杠 **\\\\** 是可选的。 *Server*

在 WinDbg 中，可以使用 " **连接到远程存根服务器** " 对话框浏览可用进程服务器的列表。 请参阅 [文件 |](file---connect-to-remote-stub.md) 有关更多详细信息，请连接到远程存根。

**注意**  要使进程服务器可被发现，必须使用提升的权限将其激活。 有关详细信息，请参阅 [激活进程服务器](activating-a-process-server.md)。

 

**注意**  
如果你没有使用有权访问服务器计算机的帐户登录到客户端计算机，则可能需要提供用户名和密码。 在客户端计算机上的命令提示符窗口中，输入以下命令。

**net use \\ \\**<em>服务器</em>**\\ ipc $/user：**<em>username</em> ，其中 *server* 是服务器计算机的名称，*用户名* 是有权访问服务器计算机的帐户的名称。

出现提示时，请输入 *用户名* 的密码。

此命令成功后，可以使用 **-QR** 或 **连接到远程存根来** 发现服务器计算机上运行 (的进程服务器) 。

 


 
