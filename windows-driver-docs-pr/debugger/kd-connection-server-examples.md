---
title: KD 连接服务器示例
description: KD 连接服务器示例
ms.assetid: 5e54dda7-4f79-40e3-bcc5-248a3a047e31
keywords:
- KD 连接服务器示例
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5e3e4e7a0a0c87a50c742c614f74acce2b32d8f7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534525"
---
# <a name="kd-connection-server-examples"></a>KD 连接服务器示例


## <span id="ddk_kd_connection_server_examples_dbg"></span><span id="DDK_KD_CONNECTION_SERVER_EXAMPLES_DBG"></span>


假设调试技术人员在要调试的计算机所在的站点不存在。 调试技术人员可能会在此站点以将此目标计算机连接到使用调试电缆的一些其他计算机上。

允许此计算机处于 127.0.0.42 的 IP 地址。 调试电缆连接 COM1 到任何端口已在目标计算机上调试启用此计算机上。 使用此命令启动 KD 连接服务器：

```console
E:\Debugging Tools for Windows> kdsrv -t tcp:port=1027 
```

然后在其他位置，该技术人员启动 WinDbg 充当智能客户端使用以下命令：

```console
G:\Debugging Tools> windbg -k kdsrv:server=@{tcp:server=127.0.0.42,port=1027},trans=@{com:port=com1,baud=57600} -y SymbolPath 
```

符号路径将相对于运行智能客户端的计算机。

下面是另一个示例。 在这种情况下，选择 NPIPE 协议，则和 KD 使用而不是 WinDbg。 第一个用户选择的管道名称。 这可以是任何字母数字字符串-在此示例中，"KernelPipe"。 第一个用户打开提升的命令提示符窗口 （以管理员身份运行），并通过输入以下命令启动调试服务器：

```console
E:\Debugging Tools for Windows> set _NT_DEBUG_PORT=com1 
E:\Debugging Tools for Windows> kdsrv -t npipe:pipe=KernelPipe 
```

技术人员在登录到客户端计算机不具有访问服务器计算机的帐户。 但该技术人员知道用户名和确实有权访问服务器计算机帐户的密码。 该帐户的用户名是 Contoso。 技术人员输入以下命令：

```console
net use \\BOX17\ipc$ /user:Contoso
```

出现提示时，该技术人员会为 Contoso 帐户输入密码。

技术人员不能确定哪些名称已用于命名管道，因此她查询 127.0.0.42 KD 连接服务器：

```console
G:\Debugging Tools> cdb -QR 127.0.0.42 
Servers on 127.0.0.42:
Debugger Server - npipe:Pipe=MainPipe
Remote Process Server - npipe:Pipe=AnotherPipe
Remote Kernel Debugger Server - npipe:Pipe=KernelPipe
```

显示三个管道。 但是，仅有一个为 KD 连接服务器--其他类型是调试服务器和用户模式进程服务器。 技术人员输入下面的命令可以启动智能客户端：

```console
G:\Debugging Tools> kd -k kdsrv:server=@{npipe:server=127.0.0.42,pipe=KernelPipe},trans=@{com:baud=57600} -y SymbolPath 
```

请注意，虽然指定的波特率，端口不是。 这将导致调试程序对指定的端口的默认\_NT\_调试\_KdSrv 正在其中运行的计算机上的端口。

 

 





