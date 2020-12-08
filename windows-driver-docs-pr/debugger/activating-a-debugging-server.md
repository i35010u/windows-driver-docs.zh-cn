---
title: 激活调试服务器
description: 可以通过两种方法激活调试服务器。
keywords:
- 激活调试服务器 Windows 调试
ms.date: 03/02/2017
topic_type:
- apiref
api_name:
- Activating a Debugging Server
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3618eb6877f316593b85cd90645647e51a99e5f5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96824339"
---
# <a name="activating-a-debugging-server"></a>激活调试服务器


可以通过两种方法激活调试服务器。 通过在提升的命令提示符窗口中使用 **-server** 命令行选项 ("以管理员身份运行") ，可以激活调试器。 它也可以在调试器运行后激活。 以提升的权限启动调试器 (以管理员) 身份运行，然后输入 [**. server**](-server--create-debugging-server-.md) 命令。

**注意**  您可以在没有提升权限的情况下激活调试服务器，并且调试客户端将能够连接到服务器。 但是，客户端将无法发现调试服务器，除非已使用提升的权限激活它。 有关如何发现调试服务器的信息，请参阅 [搜索调试服务器](searching-for-debugging-servers.md)。

 

调试器支持多种传输协议：命名管道 (NPIPE) 、TCP、COM 端口、安全管道 (SPIPE) 和安全套接字层 (SSL) 。

激活调试服务器的一般语法取决于所使用的协议。

```console
Debugger -server npipe:pipe=PipeName[,hidden][,password=Password][,IcfEnable] [-noio] [Options]

Debugger -server tcp:port=Socket[,hidden][,password=Password][,ipversion=6][,IcfEnable] [-noio] [Options]

Debugger -server tcp:port=Socket,clicon=Client[,password=Password][,ipversion=6] [-noio] [Options]

Debugger -server com:port=COMPort,baud=BaudRate,channel=COMChannel[,hidden][,password=Password] [-noio] [Options]

Debugger -server spipe:proto=Protocol,{certuser=Cert|machuser=Cert},pipe=PipeName[,hidden][,password=Password] [-noio] [Options]

Debugger -server ssl:proto=Protocol,{certuser=Cert|machuser=Cert},port=Socket[,hidden][,password=Password] [-noio] [Options]

Debugger -server ssl:proto=Protocol,{certuser=Cert|machuser=Cert},port=Socket,clicon=Client[,password=Password] [-noio] [Options]
```

激活调试服务器的另一种方法是在启动调试器后使用 [**. server (Create 调试服务器)**](-server--create-debugging-server-.md) 命令。

```dbgcmd
.server npipe:pipe=PipeName[,hidden][,password=Password][,IcfEnable] 

.server tcp:port=Socket[,hidden][,password=Password][,ipversion=6][,IcfEnable] 

.server tcp:port=Socket,clicon=Client[,password=Password][,ipversion=6] 

.server com:port=COMPort,baud=BaudRate,channel=COMChannel[,hidden][,password=Password] 

.server spipe:proto=Protocol,{certuser=Cert|machuser=Cert},pipe=PipeName[,hidden][,password=Password] 

.server ssl:proto=Protocol,{certuser=Cert|machuser=Cert},port=Socket[,hidden][,password=Password] 

.server ssl:proto=Protocol,{certuser=Cert|machuser=Cert},port=Socket,clicon=Client[,password=Password] 
```

## <span id="ddk_activating_a_debugging_server_dbg"></span><span id="DDK_ACTIVATING_A_DEBUGGING_SERVER_DBG"></span>


前面的命令中的参数具有以下可能值：

<span id="________Debugger"></span><span id="________debugger"></span><span id="________DEBUGGER"></span>*调试器*  
可以是 KD、CDB、NTSD 或 WinDbg。

<span id="________pipe_________PipeName"></span><span id="________pipe_________pipename"></span><span id="________PIPE_________PIPENAME"></span>**管道 =** *PipeName*  
如果使用 NPIPE 或 SPIPE 协议，则 *PipeName* 是将充当管道名称的字符串。 每个管道名称都应标识唯一的调试服务器。 如果尝试重用管道名称，您将收到一条错误消息。 *PipeName* 不得包含空格或引号。 *PipeName* 可以包含数字 **printf** 样式格式代码，如 **% x** 或 **% d**。 调试器会将此替换为调试器的进程 ID。 第二个这样的代码将替换为调试器的线程 ID。

**注意**  你可能需要在运行调试服务器的计算机上启用 "文件和打印机共享"。 在 "控制面板" 中，导航到 " **网络和 Internet &gt; 网络" 和 "共享中心 &gt; 高级共享设置**"。 选择 **"打开文件和打印机共享"**。

 

<span id="________port_________Socket"></span><span id="________port_________socket"></span><span id="________PORT_________SOCKET"></span>**端口 =** *套接字*  
使用 TCP 或 SSL 协议时， *套接字* 为套接字端口号。

还可以指定由冒号分隔的一系列端口。 调试器将检查此范围内的每个端口，查看其是否可用。 如果它找到一个可用端口而不发生错误，则将创建调试服务器。 调试客户端将必须指定用于连接到服务器的实际端口。 若要确定实际端口，请使用 [**搜索调试服务器**](searching-for-debugging-servers.md)中所述的任何方法;当显示此调试服务器时，端口后跟两个数字，由冒号分隔。 第一个数字将是使用的实际端口;可以忽略第二个。 例如，如果将端口指定为 **port = 51： 60**，并实际使用端口53，搜索结果将显示 "port = 53： 60"。  (如果使用 **clicon** 参数建立反向连接，则调试客户端可以通过这种方式指定一定范围的端口，而服务器必须指定使用的实际端口。 ) 

<span id="________clicon_________Client"></span><span id="________clicon_________client"></span><span id="________CLICON_________CLIENT"></span>**clicon =** *客户端*  
使用 TCP 或 SSL 协议并指定 **clicon** 参数时，将打开 *反向连接* 。 这意味着，调试服务器将尝试连接到调试客户端，而不是让客户端启动该联系人。 如果防火墙阻止连接正常，这会很有用。 *客户端* 指定在其上存在或将创建调试客户端的计算机的网络名称或 IP 地址。  (的两个初始反斜杠 \\ \) 是可选的。

由于服务器正在查找一个特定客户端，因此，如果使用此方法，则不能将多个客户端连接到服务器。 如果连接被拒绝或被破坏，则必须重新启动服务器连接。 当另一个调试器显示所有活动的服务器时，将不会显示反向连接服务器。

**注意**   当使用 **clicon** 时，最好在创建调试服务器之前启动调试客户端，不过，在客户端) 之前通常 (服务器的顺序也是允许的。

 

<span id="port_________COMPort"></span><span id="port_________comport"></span><span id="PORT_________COMPORT"></span>**端口 =** *COMPort*  
使用 COM 协议时， *COMPort* 指定要使用的 com 端口。 前缀 "COM" 是可选的，例如，"com2" 和 "2" 都是可接受的。

<span id="baud_________BaudRate"></span><span id="baud_________baudrate"></span><span id="BAUD_________BAUDRATE"></span>**波特 =** *波特率*  
使用 COM 协议时， *波特率* 指定连接的运行波特率。 允许硬件支持的任何波特率。

<span id="channel_________COMChannel"></span><span id="channel_________comchannel"></span><span id="CHANNEL_________COMCHANNEL"></span>**通道 =** *COMChannel*  
如果使用 COM 协议，则 *COMChannel* 指定要用于与调试客户端进行通信的 com 通道。 该值可以是0到254之间的任何值（含0和）。 你可以使用一个 COM 端口来实现使用不同通道号的多个连接。  (这不同于将 COM 端口用于调试电缆-在这种情况下，不能在 COM 端口中使用通道。 ) 

<span id="________proto_________Protocol"></span><span id="________proto_________protocol"></span><span id="________PROTO_________PROTOCOL"></span>**proto =** *协议*  
如果使用 SSL 或 SPIPE 协议，则 *协议* 指定 (S 通道) 协议的安全通道。 这可以是字符串是 tls1、是 pct1、是 ssl2 或 ssl3 中的任何一个。

<span id="Cert"></span><span id="cert"></span><span id="CERT"></span>*Cert*  
如果使用 SSL 或 SPIPE 协议，则 *Cert* 指定证书。 这可以是证书名称，也可以是证书的指纹 (由证书的管理单元) 指定的十六进制数字的字符串。 如果使用语法 **certuser =**<em>Cert</em> ，则调试器将在默认存储)  (系统存储中查找证书。 如果使用语法 **machuser =**<em>Cert</em> ，则调试器将在计算机存储中查找证书。 指定的证书必须支持服务器身份验证。

<span id="________hidden"></span><span id="________HIDDEN"></span>**隐藏**  
当另一个调试器显示所有活动的服务器时，禁止显示服务器。

<span id="________password_________Password"></span><span id="________password_________password"></span><span id="________PASSWORD_________PASSWORD"></span>**密码 =** *密码*  
要求客户端提供指定的密码才能连接到调试会话。 *密码* 可以是任意字母数字字符串，长度最多为12个字符。

**警告**   使用带有 TCP、NPIPE 或 COM 协议的密码仅提供少量保护，因为密码未加密。 当密码与 SSL 或 SPIPE 协议一起使用时，将对其进行加密。 如果要建立安全远程会话，则必须使用 SSL 或 SPIPE 协议。

 

<span id="________ipversion_6"></span><span id="________IPVERSION_6"></span>**ipversion = 6**  
适用于 Windows 6.6.07 和更早版本的 (调试工具仅) 强制调试器在使用 TCP 连接到 Internet 时使用 IP 版本6而不是版本4。 在 Windows Vista 和更高版本中，调试器会尝试自动默认为 IP 版本6，这不需要此选项。

<span id="-noio"></span><span id="-NOIO"></span>**-noio**  
如果调试服务器是使用 **-noio** 选项创建的，则不能通过服务器本身来执行任何输入或输出。 调试器只接受来自调试客户端的输入 (以及由 **-c** 命令行选项) 指定的任何初始命令或命令脚本。 所有输出都将定向到调试客户端。 **-Noio** 选项仅适用于 KD、CDB 和 NTSD。 如果服务器使用了 NTSD，则根本不会创建控制台窗口。

<span id="________IcfEnable"></span><span id="________icfenable"></span><span id="________ICFENABLE"></span>**IcfEnable**  
当 Internet 连接防火墙处于活动状态时，使调试器为 TCP 或命名管道通信启用必要的端口连接。 默认情况下，Internet 连接防火墙禁用这些协议使用的端口。 当 **IcfEnable** 与 TCP 连接一起使用时，调试器会使 Windows 打开 *Socket* 参数指定的端口。 当 **IcfEnable** 与命名管道连接一起使用时，调试器会使 Windows 打开用于命名管道 (端口139和 445) 的端口。 在连接终止后，调试器不会关闭这些端口。

<span id="Options_______"></span><span id="options_______"></span><span id="OPTIONS_______"></span>*选项*   
可在此处放置任何其他命令行参数。 有关完整列表，请参阅 [命令行选项](command-line-options.md) 。

您可以使用 [**. server**](-server--create-debugging-server-.md) 命令通过不同的协议选项启动多个服务器。 这允许不同类型的调试客户端加入会话。


## <a name="see-also"></a>另请参阅

[控制远程调试会话](controlling-a-remote-debugging-session.md)

[.endsrv（结束调试服务器）](-endsrv--end-debugging-server-.md)
 

------





