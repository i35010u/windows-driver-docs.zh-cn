---
title: 客户端和服务器示例
description: 客户端和服务器示例
keywords:
- 通过调试器进行远程调试，示例
ms.date: 06/08/2020
ms.localizationpriority: medium
ms.openlocfilehash: 22ac6d1e26d13f7d5c4bddf30eaa138ba04eab8b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96808499"
---
# <a name="client-and-server-examples"></a>客户端和服务器示例


## <span id="ddk_client_and_server_examples_dbg"></span><span id="DDK_CLIENT_AND_SERVER_EXAMPLES_DBG"></span>


假设一个人在名为 *\\ \\ BOX17* 的计算机上运行应用程序。 此应用程序存在问题，但调试技术人员在不同的站点上。

第一名用户在 *\\ \\ BOX17* 上使用 CDB 设置调试服务器。 目标应用程序的进程 ID 为122。 选择 TCP 协议，套接字端口号为1025。 通过在提升的命令提示符窗口中输入以下命令来启动服务器， (以管理员身份运行) ：

```console
E:\Debugging Tools for Windows> cdb -server tcp:port=1025 -p 122
```

在另一台计算机上，技术人员决定使用 WinDbg 作为调试客户端。 可以通过以下命令来启动：

```console
G:\Debugging Tools> windbg -remote tcp:server=BOX17,port=1025
```

以下是另一个示例。 在这种情况下，将选择 NPIPE 协议，并使用 CDB 而不是 WinDbg。 第一个用户选择一个管道名称。 这可以是任何字母数字字符串，在此示例中为 "MainPipe"。 第一个用户打开提升的命令提示符窗口 (以管理员身份运行) 并通过输入以下命令启动调试服务器：

```console
E:\Debugging Tools for Windows> cdb -server npipe:pipe=MainPipe -v winmine.exe 
```

技术人员使用无法访问服务器计算机的帐户登录到客户端计算机。 但技术人员知道有权访问服务器计算机的帐户的用户名和密码。 该帐户的用户名为 Contoso。 技术人员输入以下命令：

```console
net use \\BOX17\ipc$ /user:Contoso
```

系统提示时，技术人员输入 Contoso 帐户的密码。

技术人员不能确定命名管道所使用的名称，因此它们会查询 BOX17 中的可用调试服务器。

```console
G:\Debugging Tools> cdb -QR \\BOX17
Servers on \\BOX17:
Debugger Server - npipe:Pipe=MainPipe
Remote Process Server - npipe:Pipe=AnotherPipe
```

显示两个管道。 但只有一个调试服务器，另一个是进程服务器，我们对此不感兴趣。 因此， **MainPipe** 必须是正确的名称。 技术人员使用以下命令来启动调试客户端：

```console
G:\Debugging Tools> cdb -remote npipe:server=BOX17,pipe=MyPipe 
```

### <a name="span-idusing_a_secure_serverspanspan-idusing_a_secure_serverspanusing-a-secure-server"></a><span id="using_a_secure_server"></span><span id="USING_A_SECURE_SERVER"></span>使用安全服务器

下面是一个安全服务器的示例。 此服务器使用是 TLS1 协议为 S 通道协议的安全套接字层。 调试器将在计算机存储区中查找该证书。 证书由其十六进制指纹指定。

```console
D:\> cdb -server "ssl:proto=tls1,machuser=ab 38 f7 ae 13 20 ac da 05 14 65 60 30 83 7b 83 09 2c d2 34,port=1234" notepad.exe
```

 

 





