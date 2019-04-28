---
title: 激活智能客户端
description: DbgSrv 进程服务器已激活后，您可以在另一台计算机上创建智能客户端并开始调试会话。
ms.assetid: 7199dc95-e8fc-4f58-ab6e-c0141681113e
keywords:
- 激活调试智能客户端 Windows
ms.date: 02/28/2019
topic_type:
- apiref
api_name:
- Activating a Smart Client
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e9db6fc4eead1efd0e893f62de4494a3f4be37f4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351491"
---
# <a name="activating-a-smart-client"></a>激活智能客户端


DbgSrv 进程服务器已激活后，您可以在另一台计算机上创建智能客户端并开始调试会话。

有两种方法来启动智能客户端： 通过 CDB 或 WinDbg 启动与-premote[命令行选项](command-line-options.md)，或使用 WinDbg 图形界面。

智能客户端的协议必须与匹配进程服务器的协议。 正在启动智能客户端的常规语法取决于所使用的协议。 可设置的选项包括：

```console
Debugger -premote npipe:server=Server,pipe=PipeName[,password=Password] [Options]

Debugger -premote tcp:server=Server,port=Socket[,password=Password][,ipversion=6] [Options]

Debugger -premote tcp:clicon=Server,port=Socket[,password=Password][,ipversion=6] [Options]

Debugger -premote com:port=COMPort,baud=BaudRate,channel=COMChannel[,password=Password] [Options]

Debugger -premote spipe:proto=Protocol,{certuser=Cert|machuser=Cert},server=Server,pipe=PipeName[,password=Password] [Options]

Debugger -premote ssl:proto=Protocol,{certuser=Cert|machuser=Cert},server=Server,port=Socket[,password=Password] [Options]

Debugger -premote ssl:proto=Protocol,{certuser=Cert|machuser=Cert},clicon=Server,port=Socket[,password=Password] [Options]
```

若要使用的图形用户界面连接到进程服务器，WinDbg 必须处于休眠模式-它必须或者已启动任何命令行参数，或它必须结束上一个调试会话。 选择**文件 |连接到远程存根 （stub）** 菜单命令。 当**连接到远程的存根 （stub） 服务器**出现对话框，请输入以下字符串之一**连接字符串**文本框中：

```dbgcmd
npipe:server=Server,pipe=PipeName[,password=Password] 

tcp:server=Server,port=Socket[,password=Password][,ipversion=6] 

tcp:clicon=Server,port=Socket[,password=Password][,ipversion=6] 

com:port=COMPort,baud=BaudRate,channel=COMChannel[,password=Password] 

spipe:proto=Protocol,{certuser=Cert|machuser=Cert},server=Server,pipe=PipeName[,password=Password] 

ssl:proto=Protocol,{certuser=Cert|machuser=Cert},server=Server,port=Socket[,password=Password] 

ssl:proto=Protocol,{certuser=Cert|machuser=Cert},clicon=Server,port=Socket[,password=Password] 
```

或者，可以使用**浏览**按钮以找到活动的进程服务器。 请参阅[文件 |连接到远程存根 （stub）](file---connect-to-remote-stub.md)有关详细信息。

## <span id="ddk_activating_a_smart_client_dbg"></span><span id="DDK_ACTIVATING_A_SMART_CLIENT_DBG"></span>


在以上命令中的参数具有以下可能值：

<span id="________Debugger"></span><span id="________debugger"></span><span id="________DEBUGGER"></span> *调试器*  
这可以是 CDB 或 WinDbg。

<span id="________Server"></span><span id="________server"></span><span id="________SERVER"></span> *Server*  
这是计算机的网络名称或 IP 地址创建进程服务器。 这两个初始反斜杠 (\\ \)是可选的命令行中，但不是允许在 WinDbg 对话框中。

<span id="________pipe_________PipeName"></span><span id="________pipe_________pipename"></span><span id="________PIPE_________PIPENAME"></span> **pipe=** *PipeName*  
如果使用 NPIPE 或 SPIPE 协议，则*PipeName*是创建进程服务器时提供给管道的名称。

如果未登录到客户端计算机与有权访问服务器计算机帐户，必须提供用户名和密码。 在客户端计算机上，在命令提示符窗口中，输入以下命令。

**使用 net \\ \\**  <em>Server</em>**\\ipc$ /user:**<em>用户名</em>

其中*服务器*是服务器计算机的名称和*用户名*是有权访问服务器计算机帐户的名称。

当系统提示输入的密码*用户名*。

此命令成功后，你可以使用激活智能客户端 **-premote**命令行选项或通过使用 WinDbg 图形界面。

**请注意**  可能需要启用文件和打印机共享在服务器计算机上。 在控制面板中，导航到**网络和 Internet&gt;网络和共享中心&gt;高级共享设置**。 选择**启用文件和打印机共享**。

 

<span id="________port_________Socket"></span><span id="________port_________socket"></span><span id="________PORT_________SOCKET"></span> **port=** *Socket*  
如果使用 TCP 或 SSL 协议，则*套接字*是创建进程服务器时使用的同一套接字端口号。

<span id="________clicon"></span><span id="________CLICON"></span> **clicon**  
指定进程服务器将尝试连接到智能客户端通过反向连接。 客户端必须使用**clicon**当且仅当服务器使用的**clicon**。 在大多数情况下，智能客户端启动进程服务器之前，使用反向连接时。

<span id="port_________COMPort"></span><span id="port_________comport"></span><span id="PORT_________COMPORT"></span>**port=** *COMPort*  
如果使用 COM 协议，则*COMPort*指定要使用的 COM 端口。 前缀"COM"是可选的--例如，"com2"和"2"是可接受。

<span id="baud_________BaudRate"></span><span id="baud_________baudrate"></span><span id="BAUD_________BAUDRATE"></span>**baud=** *BaudRate*  
如果使用 COM 协议，则*BaudRate*应与进程服务器已创建时选择的波特率。

<span id="channel_________COMChannel"></span><span id="channel_________comchannel"></span><span id="CHANNEL_________COMCHANNEL"></span>**channel=** *COMChannel*  
如果使用 COM 协议，则*COMChannel*应匹配创建进程服务器时选择频道号。

<span id="________proto_________Protocol"></span><span id="________proto_________protocol"></span><span id="________PROTO_________PROTOCOL"></span> **proto=** *Protocol*  
如果使用 SSL 或 SPIPE 协议，则*协议*应匹配创建进程服务器时使用的安全协议。

<span id="Cert"></span><span id="cert"></span><span id="CERT"></span>*Cert*  
如果使用 SSL 或 SPIPE 协议，则应使用完全相同**certuser =**<em>Cert</em>或**machuser =**<em>Cert</em>时的参数时使用创建进程服务器。

<span id="________password_________Password"></span><span id="________password_________password"></span><span id="________PASSWORD_________PASSWORD"></span> **password=** *Password*  
如果在创建进程服务器后，使用的密码*密码*必须以创建智能客户端提供。 它必须与匹配的原始密码。 密码是区分大小写。 如果提供了错误的密码，则错误消息将指定"错误 0x80004005。"

<span id="________________ipversion_6"></span><span id="________________IPVERSION_6"></span> **ipversion=6**  
(调试工具的 Windows 6.6.07，之前仅)强制将 IP 版本 6 调试器而不是版本 4 时使用 TCP 连接到 Internet。 在 Windows Vista 和更高版本中，调试器将尝试自动默认为 IP 版本 6，这使得此选项不必要。

<span id="Options"></span><span id="options"></span><span id="OPTIONS"></span>*选项*  
可以在此处放置任何其他命令行参数。 请参阅[命令行选项](command-line-options.md)有关的完整列表。 如果使用 CDB，这必须指定要调试的过程。 如果使用 WinDbg，您可以指定进程，在命令行上或通过图形界面。

由于进程服务器只需充当网关的智能客户端的额外*选项*将会使用用户模式下调试程序开始在目标应用程序所在的同一计算机上的相同。

如果使用的 **-premote**选项与[ **.attach （附加到进程）** ](-attach--attach-to-process-.md)或者[ **.create （创建进程）** ](-create--create-process-.md)，参数将与上面所列相同。

## <a name="troubleshooting"></a>疑难解答

如果你看到此消息：*客户端与服务器不使用相同版本的远程处理协议*这指示使用 DbgSrv 尝试连接到的版本版本比 WinDbg 的版本的不同的协议。 

并不常见的协议进行更改。 这确实发生了，请确保使用匹配版本的 DbgSrv 和 WinDbg 或 WinDbg Preview 的最新可用版本。 下载最新版本的信息，请参阅[的 Windows 中下载调试的工具](debugger-download-tools.md)。

 

 





