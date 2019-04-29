---
title: 客户端和服务器示例
description: 客户端和服务器示例
ms.assetid: 78dea1c0-6e94-4980-8042-375f11386d53
keywords:
- 调试器，示例通过远程调试
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 04a03d207896a9a0b07a0ef8e0570c4ecdd17ced
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63375097"
---
# <a name="client-and-server-examples"></a>客户端和服务器示例


## <span id="ddk_client_and_server_examples_dbg"></span><span id="DDK_CLIENT_AND_SERVER_EXAMPLES_DBG"></span>


假设一个人名为的计算机上运行应用程序 *\\ \\BOX17*。 此应用程序有问题，但调试技术人员在其他站点。

第一个人设置的调试服务器上使用 CDB  *\\ \\BOX17*。 该目标应用程序的进程 ID 为 122。 选择是 TCP 协议，套接字端口号 1025年。 通过在提升的命令提示符窗口 （以管理员身份运行） 中输入以下命令启动服务器：

```console
E:\Debugging Tools for Windows> cdb -server tcp:port=1025 -p 122
```

在另一台计算机，技术人员决定使用 WinDbg 作为调试客户端。 它可以开始使用此命令：

```console
G:\Debugging Tools> windbg -remote tcp:server=BOX17,port=1025
```

下面是另一个示例。 在这种情况下，选择 NPIPE 协议，而 CDB 代替 WinDbg。 第一个用户选择的管道名称。 这可以是任何字母数字字符串-在此示例中，"MainPipe"。 第一个用户打开提升的命令提示符窗口 （以管理员身份运行），并通过输入此命令启动调试服务器：

```console
E:\Debugging Tools for Windows> cdb -server npipe:pipe=MainPipe -v winmine.exe 
```

技术人员在登录到客户端计算机不具有访问服务器计算机的帐户。 但该技术人员知道用户名和确实有权访问服务器计算机帐户的密码。 该帐户的用户名是 Contoso。 技术人员输入以下命令：

```console
net use \\BOX17\ipc$ /user:Contoso
```

出现提示时，该技术人员会为 Contoso 帐户输入密码。

技术人员不能确定哪些名称已用于命名管道，因此她查询 BOX17 可用调试服务器。

```console
G:\Debugging Tools> cdb -QR \\BOX17 
Servers on \\BOX17:
Debugger Server - npipe:Pipe=MainPipe
Remote Process Server - npipe:Pipe=AnotherPipe
```

显示了两个管道。 但是，仅有一个为调试的服务器--另一个是进程服务器，并且我们不感兴趣的。 因此**MainPipe**必须是正确的名称。 技术人员使用以下命令来启动调试客户端：

```console
G:\Debugging Tools> cdb -remote npipe:server=BOX17,pipe=MyPipe 
```

### <a name="span-idusingasecureserverspanspan-idusingasecureserverspanusing-a-secure-server"></a><span id="using_a_secure_server"></span><span id="USING_A_SECURE_SERVER"></span>使用安全服务器

下面是服务器的安全的一个示例。 此服务器使用安全套接字层与 TLS1 S 通道协议。 调试器将查找计算机存储区中的证书。 十六进制指纹来指定证书。

```console
D:\> cdb -server "ssl:proto=tls1,machuser=ab 38 f7 ae 13 20 ac da 05 14 65 60 30 83 7b 83 09 2c d2 34,port=1234" notepad.exe
```

 

 





