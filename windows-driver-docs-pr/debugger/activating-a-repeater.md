---
title: 激活中继器
description: 若要激活 repeater 连接，您将通常首先启动服务器，然后启动 repeater，然后启动客户端。还有可能开始 repeater 第一个和服务器。
ms.assetid: a2409b3d-48eb-46eb-8a53-7c4d505bb6ea
keywords:
- 激活 Repeater Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- Activating a Repeater
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 8472755660c478cd454d2ef644dd17ec1015226c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354005"
---
# <a name="activating-a-repeater"></a>激活中继器


若要激活 repeater 连接，您将通常首先启动服务器，然后启动 repeater，然后启动客户端。

还有可能开始 repeater 第一个和服务器。 除非您使用的，但**clicon**参数，以建立反向连接，客户端必须始终在启动最后一个。

## <a name="span-idsteponestartingtheserverspanspan-idsteponestartingtheserverspanstep-one-starting-the-server"></a><span id="step_one__starting_the_server"></span><span id="STEP_ONE__STARTING_THE_SERVER"></span>第一步：启动服务器


服务器可以是调试服务器、 进程服务器或 KD 连接服务器。 首先，这像通常那样，只传输协议设置将用于连接到 repeater，而不是客户端。 有关详细信息，请参阅[**激活调试服务器**](activating-a-debugging-server.md)， [**激活进程服务器**](activating-a-process-server.md)，或[ **激活 KD 连接服务器**](activating-a-kd-connection-server.md)。

创建服务器时使用密码，如果时客户端将附加，但不是创建 repeater 时将需要此密码。

如果您使用**隐藏**参数，服务器将像往常一样隐藏。 始终隐藏 repeater 本身。

## <a name="span-idsteptwostartingtherepeaterspanspan-idsteptwostartingtherepeaterspanstep-two-starting-the-repeater"></a><span id="step_two__starting_the_repeater"></span><span id="STEP_TWO__STARTING_THE_REPEATER"></span>第二步：启动 Repeater


中继器中的 Windows 调试工具包含称为 DbEngPrx (dbengprx.exe)。

DbEngPrx 理解以下传输协议： 命名管道 (NPIPE) TCP，和 COM 端口。

如果客户端和服务器使用安全套接字层 (SSL) 协议，应为 repeater 中使用 TCP 协议。 如果客户端和服务器使用的安全管道 (SPIPE) 协议，应为 repeater 中使用 NPIPE 协议。 Repeater 将通过其接收-无论数据在它不会不解释、 加密或解密的任何信息。 将由客户端和服务器完成所有加密和解密。

DbEnPrx 命令行的语法如下所示：

## <span id="ddk_activating_a_repeater_dbg"></span><span id="DDK_ACTIVATING_A_REPEATER_DBG"></span>


**dbengprx \[-p\] -c** *ClientTransport* **-s** *ServerTransport*

上述命令中的参数具有以下可能值：

<span id="________-p"></span><span id="________-P"></span> **-p**  
导致 DbEngPrx 继续现有即使与它的所有连接将被都删除。

<span id="ClientTransport"></span><span id="clienttransport"></span><span id="CLIENTTRANSPORT"></span>*ClientTransport*  
指定要在连接到服务器中使用的协议设置。 与协议应匹配创建服务器时使用。 协议语法如下所示：

```dbgcmd
npipe:server=Server,pipe=PipeName[,password=Password] 
tcp:server=Server,port=Socket[,password=Password][,ipversion=6] 
tcp:clicon=Server,port=Socket[,password=Password][,ipversion=6] 
com:port=COMPort,baud=BaudRate,channel=COMChannel[,password=Password] 
```

协议参数具有以下含义：

<span id="Server"></span><span id="server"></span><span id="SERVER"></span>*Server*  
这是计算机的网络名称或 IP 地址创建服务器。 这两个初始反斜杠 (\\ \)都是可选的。

<span id="________pipe_________PipeName"></span><span id="________pipe_________pipename"></span><span id="________PIPE_________PIPENAME"></span> **pipe=** *PipeName*  
如果使用 NPIPE 或 SPIPE 协议，则*PipeName*是创建服务器时提供给管道的名称。

<span id="________port_________Socket"></span><span id="________port_________socket"></span><span id="________PORT_________SOCKET"></span> **port=** *Socket*  
如果使用 TCP 或 SSL 协议，则*套接字*是创建服务器时使用的同一套接字端口号。

<span id="clicon"></span><span id="CLICON"></span>**clicon**  
指定服务器将尝试连接到通过反向连接 repeater。 *ClientTransport*必须使用**clicon**当且仅当服务器使用的**clicon**。 在大多数情况下，repeater 启动服务器之前，使用反向连接时。

<span id="port_________COMPort"></span><span id="port_________comport"></span><span id="PORT_________COMPORT"></span>**port=** *COMPort*  
如果使用 COM 协议，则*COMPort*指定要使用的 COM 端口。 前缀"COM"是可选的--例如，"com2"和"2"是可接受。

<span id="baud_________BaudRate"></span><span id="baud_________baudrate"></span><span id="BAUD_________BAUDRATE"></span>**baud=** *BaudRate*  
如果使用 COM 协议，则*BaudRate*应与该服务器已创建时选择的波特率。

<span id="channel_________COMChannel"></span><span id="channel_________comchannel"></span><span id="CHANNEL_________COMCHANNEL"></span>**channel=** *COMChannel*  
如果使用 COM 协议，则*COMChannel*应匹配该服务器已创建时选择频道号。

<span id="________password_________Password"></span><span id="________password_________password"></span><span id="________PASSWORD_________PASSWORD"></span> **password=** *Password*  
如果在创建服务器后，使用的密码*密码*若要创建调试客户端必须提供。 它必须与匹配的原始密码。 密码是区分大小写。 如果提供了错误的密码，则错误消息将指定"错误 0x80004005。"

<span id="________ipversion_6"></span><span id="________IPVERSION_6"></span> **ipversion=6**  
(调试工具的 Windows 6.6.07，之前仅)强制将 IP 版本 6 调试器而不是版本 4 时使用 TCP 连接到 Internet。 在 Windows Vista 和更高版本中，调试器将尝试自动默认为 IP 版本 6，这使得此选项不必要。

<span id="ServerTransport"></span><span id="servertransport"></span><span id="SERVERTRANSPORT"></span>ServerTransport  
指定客户端连接到 repeater 时将使用的协议设置。 可能的协议语法是：

```dbgcmd
npipe:pipe=PipeName[,hidden][,password=Password][,IcfEnable] 
tcp:port=Socket[,hidden][,password=Password][,IcfEnable] 
tcp:port=Socket,clicon=Client[,password=Password] 
com:port=COMPort,baud=BaudRate,channel=COMChannel[,hidden][,password=Password] 
```

协议参数具有以下含义：

<span id="________pipe_________PipeName"></span><span id="________pipe_________pipename"></span><span id="________PIPE_________PIPENAME"></span> **pipe=** *PipeName*  
当使用 NPIPE 或 SPIPE 协议时， *PipeName*是一个字符串，将作为管道的名称。 每个管道名称应标识唯一 repeater。 如果您尝试重复使用的管道名称，将收到一条错误消息。 *PipeName*不能包含空格或引号。 *PipeName*可以包含数值**printf**的样式设置代码格式，如 **%x**或 **%d**。 Repeater 将替换为此进程 ID DbEngPrx。 第二个此类代码将替换为线程 ID DbEngPrx。

<span id="________port_________Socket"></span><span id="________port_________socket"></span><span id="________PORT_________SOCKET"></span> **port=** *Socket*  
当使用 TCP 或 SSL 协议时，*套接字*是套接字端口号。

还有可能要指定一系列由冒号分隔的端口。 DbEngPrx 将检查在此范围内，以查看它是否是免费的每个端口。 如果它找到了可用端口，并且不会发生错误，将创建 repeater。 客户端必须指定用于连接到 repeater 的实际端口。 若要确定实际端口，请搜索 repeater;此 repeater 显示时，该端口将遵循由分号分隔的两个数字。 第一个数字将使用; 的实际端口可以忽略第二个。 例如，如果该端口指定为**端口 = 51:60**，和实际使用端口 53，搜索结果将显示"端口 = 53:60"。 (如果使用的**clicon**参数，以建立反向连接，客户端可以指定一系列端口以这种方式，而 repeater 必须指定使用的实际端口。)

<span id="clicon_Client"></span><span id="clicon_client"></span><span id="CLICON_CLIENT"></span>**clicon=**<em>Client</em>  
在使用 TCP 或 SSL 协议时， **clicon**指定参数，则*反向连接*将打开。 这意味着 repeater 将尝试连接到客户端，而不是让客户端启动联系人。 这可以是防火墙阻止中常规方向的连接的情况下很有用。 *客户端*指定网络名称或客户端在其存在或将创建的计算机的 IP 地址。 这两个初始反斜杠 (\\ \)都是可选的。

由于 repeater 寻找一个特定的客户端，您不能多个客户端连接到 repeater 如果使用此方法。 如果连接被拒绝或已损坏，必须重启 repeater。

当**clicon**是使用，最好是启动客户端之前创建 repeater，虽然还允许常规顺序 (repeater 之前客户端)。

<span id="port_________COMPort"></span><span id="port_________comport"></span><span id="PORT_________COMPORT"></span>**port=** *COMPort*  
当使用 COM 协议时， *COMPort*指定要使用的 COM 端口。 前缀"COM"是可选的--例如，"com2"和"2"是可接受。 不能使用中的同一个 COM 端口*ClientTransport*并*服务器传送*。

<span id="baud_________BaudRate"></span><span id="baud_________baudrate"></span><span id="BAUD_________BAUDRATE"></span>**baud=** *BaudRate*  
当使用 COM 协议时， *BaudRate*指定连接将在其中运行的波特率。 允许使用任何支持的硬件的波特率。 如果您使用的 COM 协议中均*ClientTransport*并*服务器传送*可以指定不同的波特率，但自然的速度较慢速率将速度在客户端和服务器上的限制可以与彼此通信。

<span id="channel_________COMChannel"></span><span id="channel_________comchannel"></span><span id="CHANNEL_________COMCHANNEL"></span>**channel=** *COMChannel*  
如果使用 COM 协议，则*COMChannel*指定与客户端的通信中使用的 COM 通道。 这可以是 0 和 254 之间 （含） 之间的任何值。 有关使用不同的频道号的多个连接，可以使用一个 COM 端口。 （这与调试电缆的 COM 端口用于不同--在这种情况下无法在 COM 端口使用通道。）

<span id="hidden"></span><span id="HIDDEN"></span>**hidden**  
可防止服务器出现时另一个调试器将显示所有活动服务器。

<span id="________password_________Password"></span><span id="________password_________password"></span><span id="________PASSWORD_________PASSWORD"></span> **password=** *Password*  
要求客户端提供指定的密码以连接到调试会话。 *密码*可以是任意字母数字字符串。

<span id="IcfEnable"></span><span id="icfenable"></span><span id="ICFENABLE"></span>**IcfEnable**  
使调试器以启用必要的端口连接的 TCP 或命名的管道通信，Internet 连接防火墙处于活动状态时。 默认情况下，Internet 连接防火墙禁用这些协议使用的端口。 当**IcfEnable**使用与 TCP 连接，调试器会导致 Windows 以打开指定的端口*套接字*参数。 当**IcfEnable**使用通过命名的管道连接，调试器会导致 Windows 打开端口用于命名管道 （端口 139 和 445）。 在连接终止后，调试器不会关闭这些端口。

### <a name="span-idstepthreestartingtheclientspanspan-idstepthreestartingtheclientspanstep-three-starting-the-client"></a><span id="step_three__starting_the_client"></span><span id="STEP_THREE__STARTING_THE_CLIENT"></span>第三步：在启动客户端

客户端应调试客户端或智能客户端--准对应于你的服务器类型。 有关详细信息，请参阅[**激活调试客户端**](activating-a-debugging-client.md)， [**激活智能客户端**](activating-a-smart-client.md)，或[ **激活智能客户端 （内核模式）**](activating-a-smart-client--kernel-mode-.md)。

如果服务器将拒绝连接 （例如，如果提供了错误的密码），repeater 和客户端将关闭。 你将需要重新启动这两个文件以重新建立与服务器联系。

 

 





