---
title: 激活 KD 连接服务器
description: 若要激活 KD 连接服务器，打开提升的命令提示符窗口 （以管理员身份运行），并输入 kdsrv 命令。
ms.assetid: 1b6f6f72-2679-45c7-bf1b-9607bf7e7d89
keywords:
- 激活调试 KD 连接服务器 Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- Activating a KD Connection Server
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: cbb6307c64e2ff19ddd694995921455e0ac663bf
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63353143"
---
# <a name="activating-a-kd-connection-server"></a>激活 KD 连接服务器


包含有关 Windows 调试工具在 KD 连接服务器称为 KdSrv (kdsrv.exe)。 若要激活 KD 连接服务器，打开提升的命令提示符窗口 （以管理员身份运行），并输入**kdsrv**命令。

**请注意**  可以激活 KD 连接服务器，无需具有提升的权限，并调试客户端将能够连接到服务器。 但是，客户端将不能发现 KD 连接服务器，除非它已激活使用提升的权限。 有关如何发现调试服务器的信息，请参阅[ **KD 连接服务器搜索**](searching-for-kd-connection-servers.md)。

 

KdSrv 支持多个传输协议： 命名管道 (NPIPE)，TCP、 COM 端口、 安全管道 (SPIPE) 和安全套接字层 (SSL)。

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


上述命令中的参数具有以下可能值：

<span id="________pipe_________PipeName"></span><span id="________pipe_________pipename"></span><span id="________PIPE_________PIPENAME"></span> **pipe=** *PipeName*  
当使用 NPIPE 或 SPIPE 协议时， *PipeName*是一个字符串，将作为管道的名称。 每个管道名称应标识唯一进程服务器。 如果您尝试重复使用的管道名称，将收到一条错误消息。 *PipeName*不能包含空格或引号。 *PipeName*可以包含数值**printf**的样式设置代码格式，如 **%x**或 **%d**。 这将由进程 ID 的 KdSrv 替换。 线程 ID 的 KdSrv 将替换为第二个代码。

<span id="________port_________Socket"></span><span id="________port_________socket"></span><span id="________PORT_________SOCKET"></span> **port=** *Socket*  
当使用 TCP 或 SSL 协议时，*套接字*是套接字端口号。

还有可能要指定一系列由冒号分隔的端口。 KdSrv 将检查在此范围内，以查看它是否是免费的每个端口。 如果它找到了可用端口，并且不会发生错误，将创建 KD 连接服务器。 智能客户端必须指定用于连接到服务器的实际端口。 若要确定实际端口，请使用任何一种方法中所述[ **KD 连接服务器搜索**](searching-for-kd-connection-servers.md); 当显示此 KD 连接服务器时，该端口将跟分隔的两个数字冒号。 第一个数字将使用; 的实际端口可以忽略第二个。 例如，如果该端口指定为**端口 = 51:60**，和实际使用端口 53，搜索结果将显示"端口 = 53:60"。 (如果使用的**clicon**参数，以建立反向连接，智能客户端可以指定一系列端口以这种方式，而 KD 连接服务器必须指定使用的实际端口。)

<span id="________clicon_________Client"></span><span id="________clicon_________client"></span><span id="________CLICON_________CLIENT"></span> **clicon=** *Client*  
在使用 TCP 或 SSL 协议时， **clicon**指定参数，则*反向连接*将打开。 这意味着 KD 连接服务器将尝试连接到智能客户端，而不是让客户端启动联系人。 这可以是防火墙阻止中常规方向的连接的情况下很有用。 *客户端*指定网络名称或智能客户端在其存在或将创建的计算机的 IP 地址。 这两个初始反斜杠 (\\ \)都是可选的。

由于 KD 连接服务器正在寻找一个特定的客户端，因此不能多个客户端连接到服务器如果使用此方法。 如果连接被拒绝或已损坏，必须重启进程服务器。 当有人使用时，将不会出现反向连接 KD 连接服务器 **-QR**命令行选项以显示所有活动服务器。

**请注意**  时**clicon**是使用，最好是启动智能客户端，然后创建 KD 连接服务器时，虽然还允许常规顺序 （客户端之前的服务器）。

 

<span id="port_________COMPort"></span><span id="port_________comport"></span><span id="PORT_________COMPORT"></span>**port=** *COMPort*  
当使用 COM 协议时， *COMPort*指定要使用的 COM 端口。 前缀"COM"是可选的--例如，"com2"和"2"是可接受。

<span id="baud_________BaudRate"></span><span id="baud_________baudrate"></span><span id="BAUD_________BAUDRATE"></span>**baud=** *BaudRate*  
当使用 COM 协议时， *BaudRate*指定连接将在其中运行的波特率。 允许使用任何支持的硬件的波特率。

<span id="channel_________COMChannel"></span><span id="channel_________comchannel"></span><span id="CHANNEL_________COMCHANNEL"></span>**channel=** *COMChannel*  
如果使用 COM 协议，则*COMChannel*指定与调试客户端的通信中使用的 COM 通道。 这可以是 0 和 254 之间 （含） 之间的任何值。 有关使用不同的频道号的多个连接，可以使用一个 COM 端口。 （这与调试电缆的 COM 端口用于不同--在这种情况下无法在 COM 端口使用通道。）

<span id="________proto_________Protocol"></span><span id="________proto_________protocol"></span><span id="________PROTO_________PROTOCOL"></span> **proto=** *Protocol*  
如果使用 SSL 或 SPIPE 协议，则*协议*指定安全通道 （S-通道） 协议。 这可以是字符串 tls1、 pct1、 ssl2 或 ssl3 的任何一个。

<span id="________Cert"></span><span id="________cert"></span><span id="________CERT"></span> *Cert*  
如果使用 SSL 或 SPIPE 协议，则*Cert*指定的证书。 这可以是证书名称或证书的指纹 （给定证书的管理单元的十六进制数字的字符串）。 如果语法**certuser =**<em>Cert</em>是使用，调试器将查找系统存储 （默认存储） 中的证书。 如果语法**machuser =**<em>Cert</em>是使用，调试器将查找计算机存储区中的证书。 指定的证书必须支持服务器身份验证。

<span id="________hidden"></span><span id="________HIDDEN"></span> **hidden**  
可防止 KD 连接服务器出现在有人使用时 **-QR**命令行选项以显示所有活动服务器。

<span id="________password_________Password"></span><span id="________password_________password"></span><span id="________PASSWORD_________PASSWORD"></span> **password=** *Password*  
需要智能客户端才能连接到 KD 连接 server 提供指定的密码。 *密码*可以是任何字母数字字符串，最多 12 个字符的长度。

**警告**  使用 TCP、 NPIPE 或 COM 协议使用密码只提供少量的保护，因为未加密密码。 当使用 SSL 或 SPIPE 协议使用密码时，对其进行加密。 如果你想要建立安全的远程会话，必须使用 SSL 或 SPIPE 协议。

 

<span id="________ipversion_6"></span><span id="________IPVERSION_6"></span> **ipversion=6**  
(调试工具的 Windows 6.6.07，之前仅)强制将 IP 版本 6 调试器而不是版本 4 时使用 TCP 连接到 Internet。 在 Windows Vista 和更高版本中，调试器将尝试自动默认为 IP 版本 6，这使得此选项不必要。

<span id="________IcfEnable"></span><span id="________icfenable"></span><span id="________ICFENABLE"></span> **IcfEnable**  
使调试器以启用必要的端口连接的 TCP 或命名的管道通信，Internet 连接防火墙处于活动状态时。 默认情况下，Internet 连接防火墙禁用这些协议使用的端口。 当**IcfEnable**使用与 TCP 连接，调试器会导致 Windows 以打开指定的端口*套接字*参数。 当**IcfEnable**使用通过命名的管道连接，调试器会导致 Windows 打开端口用于命名管道 （端口 139 和 445）。 在连接终止后，调试器不会关闭这些端口。

 

 





