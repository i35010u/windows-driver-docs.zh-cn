---
title: 激活 KD 连接服务器
description: 若要激活 KD 连接服务器，请打开提升的命令提示符窗口 (以管理员) 身份运行，然后输入 kdsrv 命令。
keywords:
- 激活 KD 连接服务器 Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- Activating a KD Connection Server
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ce4244dbea1f6c5302087e2b0d00adc2d49ae3cd
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96824337"
---
# <a name="activating-a-kd-connection-server"></a>激活 KD 连接服务器


Windows 调试工具中包含的 KD 连接服务器称为 KdSrv ( # A0) 。 若要激活 KD 连接服务器，请打开提升的命令提示符窗口 (以管理员) 身份运行，然后输入 **kdsrv** 命令。

**注意**  你可以在没有提升权限的情况下激活 KD 连接服务器，并且调试客户端将能够连接到服务器。 但是，除非使用提升的特权激活，否则客户端将无法发现 KD 连接服务器。 有关如何发现调试服务器的信息，请参阅 [**搜索 KD 连接服务器**](searching-for-kd-connection-servers.md)。

 

KdSrv 支持多个传输协议：命名管道 (NPIPE) 、TCP、COM 端口、安全管道 (SPIPE) 和安全套接字层 (SSL) 。

KdSrv 命令行的语法取决于所使用的协议。 可设置的选项包括：

```console
kdsrv -t npipe:pipe=PipeName[,hidden][,password=Password][,IcfEnable] 

kdsrv -t tcp:port=Socket[,hidden][,password=Password][,ipversion=6][,IcfEnable] 

kdsrv -t tcp:port=Socket,clicon=Client[,password=Password][,ipversion=6] 

kdsrv -t com:port=COMPort,baud=BaudRate,channel=COMChannel[,hidden][,password=Password] 

kdsrv -t spipe:proto=Protocol,{certuser=Cert|machuser=Cert},pipe=PipeName[,hidden][,password=Password] 

kdsrv -t ssl:proto=Protocol,{certuser=Cert|machuser=Cert},port=Socket[,hidden][,password=Password] 

kdsrv -t ssl:proto=Protocol,{certuser=Cert|machuser=Cert},port=Socket,clicon=Client[,password=Password] 
```

## <span id="ddk_activating_a_kd_connection_server_dbg"></span><span id="DDK_ACTIVATING_A_KD_CONNECTION_SERVER_DBG"></span>


前面的命令中的参数具有以下可能值：

<span id="________pipe_________PipeName"></span><span id="________pipe_________pipename"></span><span id="________PIPE_________PIPENAME"></span>**管道 =** *PipeName*  
如果使用 NPIPE 或 SPIPE 协议，则 *PipeName* 是将充当管道名称的字符串。 每个管道名称应标识唯一的进程服务器。 如果尝试重用管道名称，您将收到一条错误消息。 *PipeName* 不得包含空格或引号。 *PipeName* 可以包含数字 **printf** 样式格式代码，如 **% x** 或 **% d**。 这将替换为 KdSrv 的进程 ID。 第二个这样的代码将替换为 KdSrv 的线程 ID。

<span id="________port_________Socket"></span><span id="________port_________socket"></span><span id="________PORT_________SOCKET"></span>**端口 =** *套接字*  
使用 TCP 或 SSL 协议时， *套接字* 为套接字端口号。

还可以指定由冒号分隔的一系列端口。 KdSrv 将检查此范围内的每个端口，查看其是否可用。 如果它找到一个可用端口且不发生错误，则将创建 KD 连接服务器。 智能客户端将必须指定用于连接到服务器的实际端口。 若要确定实际端口，请使用 [**搜索 KD 连接服务器**](searching-for-kd-connection-servers.md)中所述的任何方法;当显示此 KD 连接服务器时，端口后跟两个数字，由冒号分隔。 第一个数字将是使用的实际端口;可以忽略第二个。 例如，如果将端口指定为 **port = 51： 60**，并实际使用端口53，搜索结果将显示 "port = 53： 60"。  (如果你使用 **clicon** 参数建立反向连接，则智能客户端可以采用这种方式指定一定范围的端口，而 KD 连接服务器必须指定使用的实际端口。 ) 

<span id="________clicon_________Client"></span><span id="________clicon_________client"></span><span id="________CLICON_________CLIENT"></span>**clicon =** *客户端*  
使用 TCP 或 SSL 协议并指定 **clicon** 参数时，将打开 *反向连接* 。 这意味着 KD 连接服务器将尝试连接到智能客户端，而不是让客户端启动该联系人。 如果防火墙阻止连接正常，这会很有用。 *客户端* 指定智能客户端所在计算机的网络名称或 IP 地址，或将在该计算机上创建。  (的两个初始反斜杠 \\ \) 是可选的。

由于 KD 连接服务器正在查找一个特定客户端，因此，如果使用此方法，则不能将多个客户端连接到服务器。 如果连接被拒绝或被破坏，则必须重新启动进程服务器。 当某个用户使用 **-QR** 命令行选项显示所有活动的服务器时，将不会显示反向连接 KD 连接服务器。

**注意**   当使用 **clicon** 时，最好在创建 KD 连接服务器之前启动智能客户端，不过，在客户端) 之前通常 (服务器的顺序。

 

<span id="port_________COMPort"></span><span id="port_________comport"></span><span id="PORT_________COMPORT"></span>**端口 =** *COMPort*  
使用 COM 协议时， *COMPort* 指定要使用的 com 端口。 前缀 "COM" 是可选的，例如，"com2" 和 "2" 都是可接受的。

<span id="baud_________BaudRate"></span><span id="baud_________baudrate"></span><span id="BAUD_________BAUDRATE"></span>**波特 =** *波特率*  
使用 COM 协议时， *波特率* 指定连接的运行波特率。 允许硬件支持的任何波特率。

<span id="channel_________COMChannel"></span><span id="channel_________comchannel"></span><span id="CHANNEL_________COMCHANNEL"></span>**通道 =** *COMChannel*  
如果使用 COM 协议，则 *COMChannel* 指定要用于与调试客户端进行通信的 com 通道。 该值可以是0到254之间的任何值（含0和）。 你可以使用一个 COM 端口来实现使用不同通道号的多个连接。  (这不同于将 COM 端口用于调试电缆-在这种情况下，不能在 COM 端口中使用通道。 ) 

<span id="________proto_________Protocol"></span><span id="________proto_________protocol"></span><span id="________PROTO_________PROTOCOL"></span>**proto =** *协议*  
如果使用 SSL 或 SPIPE 协议，则 *协议* 指定 (S 通道) 协议的安全通道。 这可以是字符串是 tls1、是 pct1、是 ssl2 或 ssl3 中的任何一个。

<span id="________Cert"></span><span id="________cert"></span><span id="________CERT"></span>*证书*  
如果使用 SSL 或 SPIPE 协议，则 *Cert* 指定证书。 这可以是证书名称，也可以是证书的指纹 (由证书的管理单元) 指定的十六进制数字的字符串。 如果使用语法 **certuser =**<em>Cert</em> ，则调试器将在默认存储)  (系统存储中查找证书。 如果使用语法 **machuser =**<em>Cert</em> ，则调试器将在计算机存储中查找证书。 指定的证书必须支持服务器身份验证。

<span id="________hidden"></span><span id="________HIDDEN"></span>**隐藏**  
当有人使用 **-QR** 命令行选项显示所有活动的服务器时，禁止显示 KD 连接服务器。

<span id="________password_________Password"></span><span id="________password_________password"></span><span id="________PASSWORD_________PASSWORD"></span>**密码 =** *密码*  
要求智能客户端提供指定的密码才能连接到 KD 连接服务器。 *密码* 可以是任意字母数字字符串，长度最多为12个字符。

**警告**   使用带有 TCP、NPIPE 或 COM 协议的密码仅提供少量保护，因为密码未加密。 当密码与 SSL 或 SPIPE 协议一起使用时，将对其进行加密。 如果要建立安全远程会话，则必须使用 SSL 或 SPIPE 协议。

 

<span id="________ipversion_6"></span><span id="________IPVERSION_6"></span>**ipversion = 6**  
适用于 Windows 6.6.07 和更早版本的 (调试工具仅) 强制调试器在使用 TCP 连接到 Internet 时使用 IP 版本6而不是版本4。 在 Windows Vista 和更高版本中，调试器会尝试自动默认为 IP 版本6，这不需要此选项。

<span id="________IcfEnable"></span><span id="________icfenable"></span><span id="________ICFENABLE"></span>**IcfEnable**  
当 Internet 连接防火墙处于活动状态时，使调试器为 TCP 或命名管道通信启用必要的端口连接。 默认情况下，Internet 连接防火墙禁用这些协议使用的端口。 当 **IcfEnable** 与 TCP 连接一起使用时，调试器会使 Windows 打开 *Socket* 参数指定的端口。 当 **IcfEnable** 与命名管道连接一起使用时，调试器会使 Windows 打开用于命名管道 (端口139和 445) 的端口。 在连接终止后，调试器不会关闭这些端口。

 

 





