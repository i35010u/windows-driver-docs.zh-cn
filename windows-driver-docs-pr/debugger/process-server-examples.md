---
title: 进程服务器示例
description: 进程服务器示例
ms.assetid: f87e6ff5-05a4-4dae-8151-913ea469b4ec
keywords:
- 进程服务器示例
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4dcd91d44f7883d5e4a75388f72304935ef13534
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543800"
---
# <a name="process-server-examples"></a>进程服务器示例


## <span id="ddk_process_server_examples_dbg"></span><span id="DDK_PROCESS_SERVER_EXAMPLES_DBG"></span>


假设一个人名为的计算机上运行应用程序\\ \\BOX17。 此应用程序有问题，但调试技术人员在其他站点。

第一个人设置进程服务器上使用 DbgSrv \\ \\BOX17。 该目标应用程序的进程 ID 为 122。 选择是 TCP 协议，套接字端口号 1025年。 使用以下命令启动服务器：

```console
E:\Debugging Tools for Windows> dbgsrv -t tcp:port=1025 
```

在另一台计算机，技术人员启动 WinDbg，充当智能客户端使用以下命令：

```console
G:\Debugging Tools> windbg -premote tcp:server=BOX17,port=1025 -p 122 
```

下面是另一个示例。 在这种情况下，选择 NPIPE 协议，而 CDB 代替 WinDbg。 第一个用户选择的管道名称。 这可以是任何字母数字字符串-在此示例中，"AnotherPipe"。 第一个用户打开提升的命令提示符窗口 （以管理员身份运行），并通过输入此命令启动调试服务器：

```console
E:\Debugging Tools for Windows> dbgsrv -t npipe:pipe=AnotherPipe
```

技术人员在登录到客户端计算机不具有访问服务器计算机的帐户。 但该技术人员知道用户名和确实有权访问服务器计算机帐户的密码。 该帐户的用户名是 Contoso。 技术人员输入以下命令：

```console
net use \\BOX17\ipc$ /user:Contoso
```

出现提示时，该技术人员会为 Contoso 帐户输入密码。

技术人员不能确定哪些名称已用于命名管道，因此她查询 BOX17 进程服务器：

```console
G:\Debugging Tools> cdb -QR \\BOX17 
Servers on \\BOX17:
Debugger Server - npipe:Pipe=MainPipe
Remote Process Server - npipe:Pipe=AnotherPipe
```

显示了两个管道。 但是，仅有一个为进程服务器--另一个是调试服务器，并且我们不感兴趣的。 因此**AnotherPipe**必须是正确的名称。 技术人员输入以下命令以启动智能客户端：

```console
G:\Debugging Tools> cdb -premote npipe:server=BOX17,pipe=AnotherPipe -v sol.exe 
```

使用进程服务器的更复杂示例，请参阅[中间符号](symbols-in-the-middle.md)。

 

 





