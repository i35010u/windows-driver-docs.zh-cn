---
title: 搜索进程服务器
description: 可以使用 KD 或 CDB-QR 命令行选项来获取网络服务器计算机运行的可用进程服务器的列表。
ms.assetid: 2f0cd4df-f18a-4222-ab90-7aba0f177eff
keywords:
- 搜索调试的进程服务器 Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- Searching for Process Servers
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 652878d1ba1423eca72285f7f4651fc56e557b35
ms.sourcegitcommit: b13e6d44c71197971697f710c0ecb23db13fea91
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57203932"
---
# <a name="searching-for-process-servers"></a>搜索进程服务器


可以使用 KD 或与 CDB **-QR**命令行选项来获取网络服务器计算机运行的可用进程服务器的列表。

此列表可能包含不再存在的服务器，但这不正确关闭-连接到其中一种生成一条错误消息。 该列表还将包括调试服务器和 KD 连接服务器。 每种情况下，将指示该服务器类型。

此语法如下所示：

```console
Debugger -QR \\Server
```

## <span id="ddk_searching_for_process_servers_dbg"></span><span id="DDK_SEARCHING_FOR_PROCESS_SERVERS_DBG"></span>


*调试器*可以是 KD 或 CDB-显示将在任一情况下相同。 两个反斜杠 (**\\\\**) 前面*Server*都是可选的。

在 WinDbg 中，可以使用**连接到远程的存根 （stub） 服务器**对话框浏览可用的进程服务器的列表。 请参阅[文件 |连接到远程存根 （stub）](file---connect-to-remote-stub.md)的更多详细信息。

**请注意**  对于可供检测的进程服务器，则必须激活使用提升的权限。 有关详细信息，请参阅[激活进程服务器](activating-a-process-server.md)。

 

**请注意**  如果未登录到客户端计算机与有权访问服务器计算机帐户，你可能需要提供用户名和密码。 在客户端计算机上，在命令提示符窗口中，输入以下命令。

**使用 net \\ \\**  <em>Server</em>**\\ipc$ /user:**<em>用户名</em>其中*Server*是服务器计算机的名称和*用户名*是有权访问服务器计算机帐户的名称。

当系统提示输入的密码*用户名*。

此命令成功后，可以通过使用发现的进程服务器 （在服务器计算机上运行） **-QR**或**连接到远程存根 （stub）**。

 


 