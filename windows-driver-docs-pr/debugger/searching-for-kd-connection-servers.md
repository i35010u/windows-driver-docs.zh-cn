---
title: 搜索 KD 连接服务器
description: 可以使用 KD 或 CDB-QR 命令行选项来获取网络服务器运行的可用 KD 连接服务器的列表。
ms.assetid: 24ff0e2f-d40a-4f52-91ef-e766b9387a8a
keywords:
- 搜索 KD 连接服务器 Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- Searching for KD Connection Servers
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b6b1e0f630ea6c62633b081006ea59d199cf0168
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382003"
---
# <a name="searching-for-kd-connection-servers"></a>搜索 KD 连接服务器


可以使用 KD 或与 CDB **-QR**命令行选项来获取网络服务器运行的可用 KD 连接服务器的列表。

此列表可能包含不再存在的服务器，但这不正确关闭-连接到其中一种生成一条错误消息。 该列表还将包括调试服务器和用户模式进程服务器。 每种情况下，将指示该服务器类型。

此语法如下所示：

```console
Debugger -QR \\Server 
```

## <span id="ddk_searching_for_kd_connection_servers_dbg"></span><span id="DDK_SEARCHING_FOR_KD_CONNECTION_SERVERS_DBG"></span>


*调试器*可以是 KD 或 CDB-显示将在任一情况下相同。 两个反斜杠 (**\\\\**) 前面*Server*都是可选的。

在 WinDbg 中，可以使用**连接到远程的存根 （stub） 服务器**对话框浏览可用 KD 连接服务器的列表。 请参阅[文件 |连接到远程存根 （stub）](file---connect-to-remote-stub.md)的更多详细信息。

**请注意**  对于可供检测的 KD 连接服务器，则必须激活使用提升的权限。 有关详细信息，请参阅[激活 KD 连接服务器](activating-a-kd-connection-server.md)。

 

**请注意**  如果未登录到客户端计算机与有权访问服务器计算机帐户，你可能需要提供用户名和密码。 在客户端计算机上，在命令提示符窗口中，输入以下命令。

**使用 net \\ \\**  <em>Server</em>**\\ipc$ /user:**<em>用户名</em>其中*Server*是服务器计算机的名称和*用户名*是有权访问服务器计算机帐户的名称。

当系统提示输入的密码*用户名*。

此命令成功后，可以通过使用发现 KD 连接服务器 （在服务器计算机上运行） **-QR**或**连接到远程存根 （stub）**。

 

 

 





