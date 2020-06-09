---
title: 进程服务器示例
description: 进程服务器示例
ms.assetid: f87e6ff5-05a4-4dae-8151-913ea469b4ec
keywords:
- 进程服务器，示例
ms.date: 06/08/2020
ms.localizationpriority: medium
ms.openlocfilehash: 6d1e4618071c9b407aa5b75f16b9bf828ae12dc1
ms.sourcegitcommit: 8097a09d2f989a9b3dca250c4e2ffd4cec2172e3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/09/2020
ms.locfileid: "84563159"
---
# <a name="process-server-examples"></a>进程服务器示例

假设一个人在名为 BOX17 的计算机上运行应用程序 \\ \\ 。 此应用程序存在问题，但调试技术人员在不同的站点上。

第一员使用 BOX17 上的 DbgSrv 设置进程服务器 \\ \\ 。 目标应用程序的进程 ID 为122。 选择 TCP 协议，套接字端口号为1025。 通过以下命令启动服务器：

```console
E:\Debugging Tools for Windows> dbgsrv -t tcp:port=1025 
```

在另一台计算机上，技术人员使用以下命令启动 WinDbg 作为智能客户端：

```console
G:\Debugging Tools> windbg -premote tcp:server=BOX17,port=1025 -p 122 
```

以下是另一个示例。 在这种情况下，将选择 NPIPE 协议，并使用 CDB 而不是 WinDbg。 第一个用户选择一个管道名称。 这可以是任何字母数字字符串，在此示例中为 "AnotherPipe"。 第一个用户打开提升的命令提示符窗口（以管理员身份运行），并通过输入以下命令启动调试服务器：

```console
E:\Debugging Tools for Windows> dbgsrv -t npipe:pipe=AnotherPipe
```

技术人员使用无法访问服务器计算机的帐户登录到客户端计算机。 但技术人员知道有权访问服务器计算机的帐户的用户名和密码。 该帐户的用户名为 Contoso。 技术人员输入以下命令：

```console
net use \\BOX17\ipc$ /user:Contoso
```

系统提示时，技术人员输入 Contoso 帐户的密码。

技术人员不能确定命名管道所使用的名称，因此它们会查询进程服务器的 BOX17：

```console
G:\Debugging Tools> cdb -QR \\BOX17
Servers on \\BOX17:
Debugger Server - npipe:Pipe=MainPipe
Remote Process Server - npipe:Pipe=AnotherPipe
```

显示两个管道。 但只有一个进程服务器，另一个是调试服务器，我们对此不感兴趣。 因此， **AnotherPipe**必须是正确的名称。 技术人员输入以下命令来启动智能客户端：

```console
G:\Debugging Tools> cdb -premote npipe:server=BOX17,pipe=AnotherPipe -v sol.exe
```

有关使用进程服务器的更复杂示例，请参阅[中间的符号](symbols-in-the-middle.md)。
