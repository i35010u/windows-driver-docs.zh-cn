---
title: 激活调试客户端
description: 激活调试服务器后，您可以在另一台计算机上启动调试客户端并连接到调试会话。
keywords:
- 激活调试客户端 Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- Activating a Debugging Client
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 0f98bbebd87e40dd3db452b2c4ff8749ede8d277
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96824347"
---
# <a name="activating-a-debugging-client"></a>激活调试客户端


激活调试服务器后，您可以在另一台计算机上启动调试客户端并连接到调试会话。

可以通过两种方式启动调试客户端：使用-remote [命令行选项](command-line-options.md)，或使用 WinDbg 图形界面。

客户端的协议必须与服务器的协议匹配。 启动调试客户端的常规语法取决于所使用的协议。 可设置的选项包括：

```dbgcmd
Debugger -remote npipe:server=Server,pipe=PipeName[,password=Password] 

Debugger -remote tcp:server=Server,port=Socket[,password=Password][,ipversion=6] 

Debugger -remote tcp:clicon=Server,port=Socket[,password=Password][,ipversion=6] 

Debugger -remote com:port=COMPort,baud=BaudRate,channel=COMChannel[,password=Password] 

Debugger -remote spipe:proto=Protocol,{certuser=Cert|machuser=Cert},server=Server,pipe=PipeName[,password=Password] 

Debugger -remote ssl:proto=Protocol,{certuser=Cert|machuser=Cert},server=Server,port=Socket[,password=Password] 

Debugger -remote ssl:proto=Protocol,{certuser=Cert|machuser=Cert},clicon=Server,port=Socket[,password=Password] 
```

若要使用图形界面连接到远程调试会话，WinDbg 必须处于休眠模式--它必须在没有命令行参数的情况下启动，或者必须已结束了前面的调试会话。 选择 **文件 |连接到远程会话** 菜单命令，或按 CTRL + R 快捷键。 出现 " **连接到远程调试器会话** " 对话框时，请在 " **连接字符串** " 文本框中输入以下字符串之一：

```dbgcmd
npipe:server=Server,pipe=PipeName[,password=Password] 

tcp:server=Server,port=Socket[,password=Password][,ipversion=6] 

tcp:clicon=Server,port=Socket[,password=Password][,ipversion=6] 

com:port=COMPort,baud=BaudRate,channel=COMChannel[,password=Password] 

spipe:proto=Protocol,{certuser=Cert|machuser=Cert},server=Server,pipe=PipeName[,password=Password] 

ssl:proto=Protocol,{certuser=Cert|machuser=Cert},server=Server,port=Socket[,password=Password] 

ssl:proto=Protocol,{certuser=Cert|machuser=Cert},clicon=Server,port=Socket[,password=Password] 
```

或者，您可以使用 " **浏览** " 按钮来查找活动的调试服务器。 请参阅 [文件 |](file---connect-to-remote-session.md) 有关详细信息，请连接到远程会话。

## <span id="ddk_activating_a_debugging_client_dbg"></span><span id="DDK_ACTIVATING_A_DEBUGGING_CLIENT_DBG"></span>


上述命令中的参数具有以下可能值：

<span id="________Debugger"></span><span id="________debugger"></span><span id="________DEBUGGER"></span>*调试器*  
这不必与调试客户端使用的调试器相同-对于通过调试器进行远程调试，WinDbg、KD 和 CDB 都是可互换的。

<span id="________Server"></span><span id="________server"></span><span id="________SERVER"></span>*服务器*  
这是在其上创建调试服务器的计算机的网络名称或 IP 地址。 两个初始反斜杠 (在 \\ \) 命令行上是可选的，但在 WinDbg 对话框中是不允许的。

<span id="________pipe_________PipeName"></span><span id="________pipe_________pipename"></span><span id="________PIPE_________PIPENAME"></span>**管道 =** *PipeName*  
如果使用 NPIPE 或 SPIPE 协议，则 *PipeName* 是在创建服务器时为管道提供的名称。

如果你没有使用有权访问服务器计算机的帐户登录到客户端计算机，则必须提供用户名和密码。 在客户端计算机上的命令提示符窗口中，输入以下命令。

**net use \\ \\**<em>服务器</em>**\\ ipc $/user：**<em>用户名</em>

其中 *server* 是服务器计算机的名称， *用户名* 是有权访问服务器计算机的帐户的名称。

出现提示时，请输入 *用户名* 的密码。

此命令成功后，可以使用 **-remote** 命令行选项或通过使用 WinDbg 图形界面激活调试客户端。

**注意**  可能需要在服务器计算机上启用 "文件和打印机共享"。 在 "控制面板" 中，导航到 " **网络和 Internet &gt; 网络" 和 "共享中心 &gt; 高级共享设置**"。 选择 **"打开文件和打印机共享"**。

 

<span id="________port_________Socket"></span><span id="________port_________socket"></span><span id="________PORT_________SOCKET"></span>**端口 =** *套接字*  
如果使用 TCP 或 SSL 协议， *套接字* 就是创建服务器时所用的同一个套接字端口号。

<span id="clicon"></span><span id="CLICON"></span>**clicon**  
指定调试服务器将尝试通过反向连接连接到客户端。 当且仅当服务器使用 **clicon** 时，客户端才能使用 **clicon** 。 在大多数情况下，调试客户端在使用反向连接时在调试服务器之前开始。

<span id="________port_________COMPort"></span><span id="________port_________comport"></span><span id="________PORT_________COMPORT"></span>**端口 =** *COMPort*  
如果使用 COM 协议， *COMPort* 将指定要使用的 com 端口。 前缀 "COM" 是可选的，例如，"com2" 和 "2" 都是可接受的。

<span id="baud_________BaudRate"></span><span id="baud_________baudrate"></span><span id="BAUD_________BAUDRATE"></span>**波特 =** *波特率*  
如果使用 COM 协议， *波特率* 应与创建服务器时选择的波特率匹配。

<span id="channel_________COMChannel"></span><span id="channel_________comchannel"></span><span id="CHANNEL_________COMCHANNEL"></span>**通道 =** *COMChannel*  
如果使用 COM 协议，则 *COMChannel* 应与创建服务器时选择的通道号匹配。

<span id="________proto_________Protocol"></span><span id="________proto_________protocol"></span><span id="________PROTO_________PROTOCOL"></span>**proto =** *协议*  
如果使用 SSL 或 SPIPE 协议，则 *协议* 应与创建服务器时使用的安全协议匹配。

<span id="________Cert"></span><span id="________cert"></span><span id="________CERT"></span>*证书*  
如果使用 SSL 或 SPIPE 协议，则应使用创建服务器时所用的相同 **certuser =**<em>cert</em> 或 **machuser =** *cert* 参数。

<span id="________password_________Password"></span><span id="________password_________password"></span><span id="________PASSWORD_________PASSWORD"></span>**密码 =** *密码*  
如果在创建服务器时使用了密码，则必须提供 *密码* 才能创建调试客户端。 它必须与原始密码匹配。 密码是区分大小写的。 如果提供了错误的密码，错误消息会指定 "错误 0x80004005"。 密码长度必须小于或等于12个字符。

<span id="________ipversion_6"></span><span id="________IPVERSION_6"></span>**ipversion = 6**  
适用于 Windows 6.6.07 和更早版本的 (调试工具仅) 强制调试器在使用 TCP 连接到 Internet 时使用 IP 版本6而不是版本4。 在 Windows Vista 和更高版本中，调试器会尝试自动默认为 IP 版本6，这不需要此选项。

调试客户端不能使用用于启动新调试会话的命令行选项 (如 **-p**) ，但只能由服务器使用。  (类似于 **-n**) 的配置选项将从客户端或服务器运行。

 

 





