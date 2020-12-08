---
title: 激活智能客户端
description: 激活 DbgSrv 进程服务器后，您可以在另一台计算机上创建一个智能客户端并开始一个调试会话。
keywords:
- 激活智能客户端 Windows 调试
ms.date: 02/28/2019
topic_type:
- apiref
api_name:
- Activating a Smart Client
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: aca62d1d85d6f40dea7798da8d8a1b6d0431e1d8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796305"
---
# <a name="activating-a-smart-client"></a>激活智能客户端


激活 DbgSrv 进程服务器后，您可以在另一台计算机上创建一个智能客户端并开始一个调试会话。

可以通过两种方式启动智能客户端：使用-premote [命令行选项](command-line-options.md)启动 CDB 或 WinDbg，或使用 WinDbg 图形界面。

智能客户端的协议必须与进程服务器的协议匹配。 用于启动智能客户端的常规语法取决于所使用的协议。 可设置的选项包括：

```console
Debugger -premote npipe:server=Server,pipe=PipeName[,password=Password] [Options]

Debugger -premote tcp:server=Server,port=Socket[,password=Password][,ipversion=6] [Options]

Debugger -premote tcp:clicon=Server,port=Socket[,password=Password][,ipversion=6] [Options]

Debugger -premote com:port=COMPort,baud=BaudRate,channel=COMChannel[,password=Password] [Options]

Debugger -premote spipe:proto=Protocol,{certuser=Cert|machuser=Cert},server=Server,pipe=PipeName[,password=Password] [Options]

Debugger -premote ssl:proto=Protocol,{certuser=Cert|machuser=Cert},server=Server,port=Socket[,password=Password] [Options]

Debugger -premote ssl:proto=Protocol,{certuser=Cert|machuser=Cert},clicon=Server,port=Socket[,password=Password] [Options]
```

若要使用图形界面连接到进程服务器，WinDbg 必须处于休眠模式--它必须在没有命令行参数的情况下启动，或者必须已结束了前面的调试会话。 选择 **文件 |连接到远程存根** 菜单命令。 出现 " **连接到远程存根服务器** " 对话框时，请在 " **连接字符串** " 文本框中输入以下字符串之一：

```dbgcmd
npipe:server=Server,pipe=PipeName[,password=Password] 

tcp:server=Server,port=Socket[,password=Password][,ipversion=6] 

tcp:clicon=Server,port=Socket[,password=Password][,ipversion=6] 

com:port=COMPort,baud=BaudRate,channel=COMChannel[,password=Password] 

spipe:proto=Protocol,{certuser=Cert|machuser=Cert},server=Server,pipe=PipeName[,password=Password] 

ssl:proto=Protocol,{certuser=Cert|machuser=Cert},server=Server,port=Socket[,password=Password] 

ssl:proto=Protocol,{certuser=Cert|machuser=Cert},clicon=Server,port=Socket[,password=Password] 
```

或者，您可以使用 " **浏览** " 按钮来查找活动进程服务器。 请参阅 [文件 |连接到远程存根](file---connect-to-remote-stub.md) 获取详细信息。

## <span id="ddk_activating_a_smart_client_dbg"></span><span id="DDK_ACTIVATING_A_SMART_CLIENT_DBG"></span>


上述命令中的参数具有以下可能值：

<span id="________Debugger"></span><span id="________debugger"></span><span id="________DEBUGGER"></span>*调试器*  
这可以是 CDB 或 WinDbg。

<span id="________Server"></span><span id="________server"></span><span id="________SERVER"></span>*服务器*  
这是在其上创建进程服务器的计算机的网络名称或 IP 地址。 两个初始反斜杠 (在 \\ \) 命令行上是可选的，但在 WinDbg 对话框中是不允许的。

<span id="________pipe_________PipeName"></span><span id="________pipe_________pipename"></span><span id="________PIPE_________PIPENAME"></span>**管道 =** *PipeName*  
如果使用 NPIPE 或 SPIPE 协议，则 *PipeName* 是创建进程服务器时为管道提供的名称。

如果你没有使用有权访问服务器计算机的帐户登录到客户端计算机，则必须提供用户名和密码。 在客户端计算机上的命令提示符窗口中，输入以下命令。

**net use \\ \\**<em>服务器</em>**\\ ipc $/user：**<em>用户名</em>

其中 *server* 是服务器计算机的名称， *用户名* 是有权访问服务器计算机的帐户的名称。

出现提示时，请输入 *用户名* 的密码。

此命令成功后，可以使用 **-premote** 命令行选项或使用 WinDbg 图形界面激活智能客户端。

**注意**  可能需要在服务器计算机上启用 "文件和打印机共享"。 在 "控制面板" 中，导航到 " **网络和 Internet &gt; 网络" 和 "共享中心 &gt; 高级共享设置**"。 选择 **"打开文件和打印机共享"**。

 

<span id="________port_________Socket"></span><span id="________port_________socket"></span><span id="________PORT_________SOCKET"></span>**端口 =** *套接字*  
如果使用了 TCP 或 SSL 协议， *套接字* 就是创建进程服务器时使用的同一个套接字端口号。

<span id="________clicon"></span><span id="________CLICON"></span>**clicon**  
指定进程服务器将尝试通过反向连接连接到智能客户端。 当且仅当服务器使用 **clicon** 时，客户端才能使用 **clicon** 。 在大多数情况下，在使用反向连接时，将在进程服务器之前启动智能客户端。

<span id="port_________COMPort"></span><span id="port_________comport"></span><span id="PORT_________COMPORT"></span>**端口 =** *COMPort*  
如果使用 COM 协议， *COMPort* 将指定要使用的 com 端口。 前缀 "COM" 是可选的，例如，"com2" 和 "2" 都是可接受的。

<span id="baud_________BaudRate"></span><span id="baud_________baudrate"></span><span id="BAUD_________BAUDRATE"></span>**波特 =** *波特率*  
如果使用 COM 协议， *波特率* 应与创建进程服务器时选择的波特率匹配。

<span id="channel_________COMChannel"></span><span id="channel_________comchannel"></span><span id="CHANNEL_________COMCHANNEL"></span>**通道 =** *COMChannel*  
如果使用 COM 协议，则 *COMChannel* 应与创建进程服务器时选择的通道号匹配。

<span id="________proto_________Protocol"></span><span id="________proto_________protocol"></span><span id="________PROTO_________PROTOCOL"></span>**proto =** *协议*  
如果使用 SSL 或 SPIPE 协议，则 *协议* 应与创建进程服务器时使用的安全协议匹配。

<span id="Cert"></span><span id="cert"></span><span id="CERT"></span>*Cert*  
如果使用 SSL 或 SPIPE 协议，则应该使用创建进程服务器时使用的相同 **certuser =**<em>cert</em> 或 **machuser =**<em>cert</em> 参数。

<span id="________password_________Password"></span><span id="________password_________password"></span><span id="________PASSWORD_________PASSWORD"></span>**密码 =** *密码*  
如果在创建进程服务器时使用了密码，则必须提供 *密码* 才能创建智能客户端。 它必须与原始密码匹配。 密码是区分大小写的。 如果提供了错误的密码，错误消息会指定 "错误 0x80004005"。

<span id="________________ipversion_6"></span><span id="________________IPVERSION_6"></span>**ipversion = 6**  
适用于 Windows 6.6.07 和更早版本的 (调试工具仅) 强制调试器在使用 TCP 连接到 Internet 时使用 IP 版本6而不是版本4。 在 Windows Vista 和更高版本中，调试器会尝试自动默认为 IP 版本6，这不需要此选项。

<span id="Options"></span><span id="options"></span><span id="OPTIONS"></span>*选项*  
可在此处放置任何其他命令行参数。 有关完整列表，请参阅 [命令行选项](command-line-options.md) 。 如果使用的是 CDB，则必须指定要调试的进程。 如果使用的是 WinDbg，则可以在命令行上或通过图形界面指定进程。

由于进程服务器仅充当智能客户端的网关，因此，如果在目标应用程序所在的同一台计算机上启动用户模式调试器，则附加选项将与你要使用的 *选项* 相同。

如果将-premote 选项 (与一起使用，请将 **-** 选项附加 [**到进程)**](-attach--attach-to-process-.md) 或 [**。创建 (创建进程)**](-create--create-process-.md)，参数与上面列出的参数相同。

## <a name="troubleshooting"></a>故障排除

如果看到此消息： *客户端未使用与服务器相同的远程处理协议版本* ，则表示你尝试连接到的 DbgSrv 版本所使用的协议版本不同于 WinDbg 的版本。 

不太常见，协议发生了更改。 发生这种情况时，请确保使用的是最新可用版本的 DbgSrv 和 WinDbg 或 WinDbg 预览版的匹配版本。 有关下载最新版本的信息，请参阅 [下载适用于 Windows 的调试工具](debugger-download-tools.md)。

 

 





