---
title: 激活智能客户端（内核模式）
description: 激活 KD 连接服务器后，可以在另一台计算机上创建一个智能客户端，并开始一个调试会话。
keywords:
- ) Windows 调试中激活智能客户端 (内核模式
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- Activating a Smart Client (Kernel Mode)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a7e1ec98203b86c09c3d9aaa04e70de5cd51efc4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838249"
---
# <a name="activating-a-smart-client-kernel-mode"></a>激活智能客户端（内核模式）


激活 KD 连接服务器后，可以在另一台计算机上创建一个智能客户端，并开始一个调试会话。

可以通过两种方式启动智能客户端：通过使用内核协议 **kdsrv** 启动 KD 或 windbg，或使用 WinDbg 图形界面。

你需要指定 KD 连接服务器使用的远程传输协议。 还可以为 KD 连接服务器与目标计算机之间的实际内核连接指定协议，也可以使用默认值。

用于启动智能客户端的常规语法取决于所使用的协议。 可设置的选项包括：

```console
Debugger -k kdsrv:server=@{npipe:server=Server,pipe=PipeName[,password=Password]},trans=@{ConnectType} [Options]

Debugger -k kdsrv:server=@{tcp:server=Server,port=Socket[,password=Password][,ipversion=6]},trans=@{ConnectType} [Options]

Debugger -k kdsrv:server=@{tcp:clicon=Server,port=Socket[,password=Password][,ipversion=6]},trans=@{ConnectType} [Options]

Debugger -k kdsrv:server=@{com:port=COMPort,baud=BaudRate,channel=COMChannel[,password=Password]},trans=@{ConnectType} [Options]

Debugger -k kdsrv:server=@{spipe:proto=Protocol,{certuser=Cert|machuser=Cert},server=Server,pipe=PipeName[,password=Password]},trans=@{ConnectType} [Options]

Debugger -k kdsrv:server=@{ssl:proto=Protocol,{certuser=Cert|machuser=Cert},server=Server,port=Socket[,password=Password]},trans=@{ConnectType} [Options]

Debugger -k kdsrv:server=@{ssl:proto=Protocol,{certuser=Cert|machuser=Cert},clicon=Server,port=Socket[,password=Password]},trans=@{ConnectType} [Options]
```

若要使用图形界面连接到 KD 连接服务器，WinDbg 必须处于休眠模式--它必须在没有命令行参数的情况下启动，或者必须已结束了前面的调试会话。 选择 **文件 |连接到远程存根** 菜单命令。 出现 " **连接到远程存根服务器** " 对话框时，请在 " **连接字符串** " 文本框中输入以下字符串之一：

```dbgcmd
npipe:server=Server,pipe=PipeName[,password=Password] 

tcp:server=Server,port=Socket[,password=Password][,ipversion=6] 

tcp:clicon=Server,port=Socket[,password=Password][,ipversion=6] 

com:port=COMPort,baud=BaudRate,channel=COMChannel[,password=Password] 

spipe:proto=Protocol,{certuser=Cert|machuser=Cert},server=Server,pipe=PipeName[,password=Password] 

ssl:proto=Protocol,{certuser=Cert|machuser=Cert},server=Server,port=Socket[,password=Password] 

ssl:proto=Protocol,{certuser=Cert|machuser=Cert},clicon=Server,port=Socket[,password=Password] 
```

或者，您可以使用 " **浏览** " 按钮查找活动 KD 连接服务器。 请参阅 [文件 |连接到远程存根](file---connect-to-remote-stub.md) 获取详细信息。

## <span id="ddk_activating_a_smart_client_kernel_mode__dbg"></span><span id="DDK_ACTIVATING_A_SMART_CLIENT_KERNEL_MODE__DBG"></span>


上述命令中的参数具有以下可能值：

<span id="________Debugger"></span><span id="________debugger"></span><span id="________DEBUGGER"></span>*调试器*  
这可以是 KD 或 WinDbg。

<span id="Server"></span><span id="server"></span><span id="SERVER"></span>*服务*  
这是在其上创建 KD 连接服务器的计算机的网络名称或 IP 地址。两个初始反斜杠 (在 \\ \) 命令行上是可选的，但在 WinDbg 对话框中是不允许的。

<span id="________pipe_________PipeName"></span><span id="________pipe_________pipename"></span><span id="________PIPE_________PIPENAME"></span>**管道 =** *PipeName*  
如果使用 NPIPE 或 SPIPE 协议，则 *PipeName* 是创建 KD 连接服务器时为管道提供的名称。

如果你没有使用有权访问服务器计算机的帐户登录到客户端计算机，则必须提供用户名和密码。 在客户端计算机上的命令提示符窗口中，输入以下命令。

**net use \\ \\**<em>服务器</em>**\\ ipc $/user：**<em>用户名</em>

其中 *server* 是服务器计算机的名称， *用户名* 是有权访问服务器计算机的帐户的名称。

出现提示时，请输入 *用户名* 的密码。

此命令成功后，可以使用 **-k kdsrv** 或使用 WinDbg 图形界面激活智能客户端。

<span id="________port_________Socket"></span><span id="________port_________socket"></span><span id="________PORT_________SOCKET"></span>**端口 =** *套接字*  
如果使用了 TCP 或 SSL 协议， *套接字* 就是在创建 KD 连接服务器时使用的套接字端口号。

<span id="clicon"></span><span id="CLICON"></span>**clicon**  
指定 KD 连接服务器将尝试通过反向连接连接到智能客户端。 当且仅当服务器使用 **clicon** 时，客户端才能使用 **clicon** 。 在大多数情况下，在使用反向连接时，会在 KD 连接服务器之前启动智能客户端。

<span id="port_________COMPort"></span><span id="port_________comport"></span><span id="PORT_________COMPORT"></span>**端口 =** *COMPort*  
如果使用 COM 协议， *COMPort* 将指定要使用的 com 端口。 前缀 "COM" 是可选的，例如，"com2" 和 "2" 都是可接受的。

<span id="baud_________BaudRate"></span><span id="baud_________baudrate"></span><span id="BAUD_________BAUDRATE"></span>**波特 =** *波特率*  
如果使用 COM 协议， *波特率* 应与创建 KD 连接服务器时选择的波特率匹配。

<span id="channel_________COMChannel"></span><span id="channel_________comchannel"></span><span id="CHANNEL_________COMCHANNEL"></span>**通道 =** *COMChannel*  
如果使用 COM 协议，则 *COMChannel* 应匹配创建 KD 连接服务器时选择的通道号。

<span id="________proto_________Protocol"></span><span id="________proto_________protocol"></span><span id="________PROTO_________PROTOCOL"></span>**proto =** *协议*  
如果使用 SSL 或 SPIPE 协议，则 *协议* 应与创建 KD 连接服务器时使用的安全协议匹配。

<span id="________Cert"></span><span id="________cert"></span><span id="________CERT"></span>*证书*  
如果使用 SSL 或 SPIPE 协议，则应使用创建 KD 连接服务器时使用的相同 **certuser =**<em>cert</em> 或 **machuser =**<em>cert</em> 参数。

<span id="________password_________Password"></span><span id="________password_________password"></span><span id="________PASSWORD_________PASSWORD"></span>**密码 =** *密码*  
如果在创建 KD 连接服务器时使用了密码，则必须提供 *密码* 才能创建智能客户端。 它必须与原始密码匹配。 密码是区分大小写的。 如果提供了错误的密码，错误消息会指定 "错误 0x80004005"。

<span id="________ipversion_6"></span><span id="________IPVERSION_6"></span>**ipversion = 6**  
适用于 Windows 6.6.07 和更早版本的 (调试工具仅) 强制调试器在使用 TCP 连接到 Internet 时使用 IP 版本6而不是版本4。 在 Windows Vista 和更高版本中，调试器会尝试自动默认为 IP 版本6，这不需要此选项。

<span id="________trans___________ConnectType_________"></span><span id="________trans___________connecttype_________"></span><span id="________TRANS___________CONNECTTYPE_________"></span>**交易额 = @ {** *ConnectType* **}**  
告诉调试器如何连接到目标。 允许使用以下内核连接协议：

```dbgcmd
com:port=ComPort,baud=BaudRate 
1394:channel=1394Channel[,symlink=1394Protocol] 
usb2:targetname=String 
com:pipe,port=\\VMHost\pipe\PipeName[,resets=0][,reconnect]
com:modem 
```

有关这些协议的信息，请参阅 [获取调试设置](getting-set-up-for-debugging.md)。 您可以省略这些协议的任何参数-例如，可以说 " **交易额 = @ {com：}** "，并且调试器将默认为运行 KdSrv 的计算机上的环境变量所指定的值。

<span id="Options"></span><span id="options"></span><span id="OPTIONS"></span>*选项*  
可在此处放置任何其他命令行参数。 有关完整列表，请参阅 [命令行选项](command-line-options.md) 。

由于 KD 连接服务器仅充当智能客户端的网关，因此，如果在运行 KdSrv 的计算机上启动内核调试器，则附加选项将与你要使用的 *选项* 相同。 这种情况的例外是在智能客户端运行的计算机上指定路径或文件名的任何选项。

 

 





