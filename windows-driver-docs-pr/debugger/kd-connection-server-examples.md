---
title: KD 连接服务器示例
description: KD 连接服务器示例
keywords:
- KD 连接服务器，示例
ms.date: 06/08/2020
ms.localizationpriority: medium
ms.openlocfilehash: 4114a202a558524170a827a48afc5cb9995bbb60
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96801931"
---
# <a name="kd-connection-server-examples"></a>KD 连接服务器示例


## <span id="ddk_kd_connection_server_examples_dbg"></span><span id="DDK_KD_CONNECTION_SERVER_EXAMPLES_DBG"></span>


假设调试技术人员在要调试的计算机所在的站点上不存在。 调试技术人员要求此站点的用户将此目标计算机连接到另一台具有调试电缆的计算机。

让其他计算机位于 IP 地址127.0.0.42。 调试电缆将此计算机上的 COM1 连接到目标计算机上已启用调试的任何端口。 此命令启动了 KD 连接服务器：

```console
E:\Debugging Tools for Windows> kdsrv -t tcp:port=1027
```

然后，在其他位置，技术人员使用此命令以智能客户端的形式启动 WinDbg：

```console
G:\Debugging Tools> windbg -k kdsrv:server=@{tcp:server=127.0.0.42,port=1027},trans=@{com:port=com1,baud=57600} -y SymbolPath
```

符号路径将相对于运行智能客户端的计算机。

以下是另一个示例。 在这种情况下，将选择 NPIPE 协议，并使用 KD 而不是 WinDbg。 第一个用户选择一个管道名称。 这可以是任何字母数字字符串，在此示例中为 "KernelPipe"。 第一个用户打开提升的命令提示符窗口 (以管理员身份运行) 并通过输入以下命令启动调试服务器：

```console
E:\Debugging Tools for Windows> set _NT_DEBUG_PORT=com1
E:\Debugging Tools for Windows> kdsrv -t npipe:pipe=KernelPipe
```

技术人员使用无法访问服务器计算机的帐户登录到客户端计算机。 但技术人员知道有权访问服务器计算机的帐户的用户名和密码。 该帐户的用户名为 Contoso。 技术人员输入以下命令：

```console
net use \\BOX17\ipc$ /user:Contoso
```

系统提示时，技术人员输入 Contoso 帐户的密码。

技术人员不能确定命名管道所使用的名称，因此它们会查询 127.0.0.42 KD 连接服务器：

```console
G:\Debugging Tools> cdb -QR 127.0.0.42
Servers on 127.0.0.42:
Debugger Server - npipe:Pipe=MainPipe
Remote Process Server - npipe:Pipe=AnotherPipe
Remote Kernel Debugger Server - npipe:Pipe=KernelPipe
```

显示了三个管道。 但只有一个连接服务器是 KD 连接服务器，其他服务器是调试服务器和用户模式进程服务器。 技术人员输入以下命令来启动智能客户端：

```console
G:\Debugging Tools> kd -k kdsrv:server=@{npipe:server=127.0.0.42,pipe=KernelPipe},trans=@{com:baud=57600} -y SymbolPath
```

请注意，尽管指定了波特速率，但端口却不是。 这会使调试器默认为 \_ \_ \_ 运行 KdSrv 的计算机上的 NT 调试端口指定的端口。
