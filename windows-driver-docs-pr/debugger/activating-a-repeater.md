---
title: 激活中继器
description: 若要激活 repeater 连接，通常需要首先启动服务器，然后启动中继器，然后启动客户端。还可以首先启动中继器，然后再启动服务器。
keywords:
- 激活中继器 Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- Activating a Repeater
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 01edad66566c46b273f059e861e5f5a9d001123e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838377"
---
# <a name="activating-a-repeater"></a>激活中继器


若要激活 repeater 连接，通常需要首先启动服务器，然后启动中继器，然后启动客户端。

还可以首先启动中继器，然后再启动服务器。 但除非使用 **clicon** 参数来建立反向连接，否则客户端必须始终是最后一次启动。

## <a name="span-idstep_one__starting_the_serverspanspan-idstep_one__starting_the_serverspanstep-one-starting-the-server"></a><span id="step_one__starting_the_server"></span><span id="STEP_ONE__STARTING_THE_SERVER"></span>第一步：启动服务器


服务器可以是调试服务器、进程服务器或 KD 连接服务器。 你可以像平常一样启动，只不过传输协议设置将用于连接到中继器，而不是客户端。 有关详细信息，请参阅 [**激活调试服务器**](activating-a-debugging-server.md)、 [**激活进程服务器**](activating-a-process-server.md)或 [**激活 KD 连接服务器**](activating-a-kd-connection-server.md)。

如果在创建服务器时使用了密码，则在客户端附加时（而不是在创建中继器时），将需要此密码。

如果使用 **hidden** 参数，服务器将照常隐藏。 中继器本身始终处于隐藏状态。

## <a name="span-idstep_two__starting_the_repeaterspanspan-idstep_two__starting_the_repeaterspanstep-two-starting-the-repeater"></a><span id="step_two__starting_the_repeater"></span><span id="STEP_TWO__STARTING_THE_REPEATER"></span>步骤2：启动中继器


Windows 调试工具中包含的中继器称为 DbEngPrx ( # A0) 。

DbEngPrx 了解以下传输协议：命名管道 (NPIPE) 、TCP 和 COM 端口。

如果客户端和服务器使用安全套接字层 (SSL) 协议，则应使用 TCP 协议进行中继器。 如果客户端和服务器使用 (SPIPE) 协议的安全管道，则应使用 NPIPE 协议进行中继器。 中继器会传递它接收的任何数据，而不会对任何信息进行解释、加密或解密。 所有加密和解密都由客户端和服务器完成。

DbEnPrx 命令行的语法如下所示：

## <span id="ddk_activating_a_repeater_dbg"></span><span id="DDK_ACTIVATING_A_REPEATER_DBG"></span>


**dbengprx \[ - \]** *ClientTransport* **-s** *ServerTransport*

前面的命令中的参数具有以下可能值：

<span id="________-p"></span><span id="________-P"></span>**-p**  
导致 DbEngPrx 在删除所有连接后继续现有。

<span id="ClientTransport"></span><span id="clienttransport"></span><span id="CLIENTTRANSPORT"></span>*ClientTransport*  
指定要在连接到服务器时使用的协议设置。 协议应与创建服务器时使用的协议匹配。 协议语法如下所示：

```dbgcmd
npipe:server=Server,pipe=PipeName[,password=Password] 
tcp:server=Server,port=Socket[,password=Password][,ipversion=6] 
tcp:clicon=Server,port=Socket[,password=Password][,ipversion=6] 
com:port=COMPort,baud=BaudRate,channel=COMChannel[,password=Password] 
```

协议参数具有以下含义：

<span id="Server"></span><span id="server"></span><span id="SERVER"></span>*服务*  
这是在其上创建服务器的计算机的网络名称或 IP 地址。  (的两个初始反斜杠 \\ \) 是可选的。

<span id="________pipe_________PipeName"></span><span id="________pipe_________pipename"></span><span id="________PIPE_________PIPENAME"></span>**管道 =** *PipeName*  
如果使用 NPIPE 或 SPIPE 协议，则 *PipeName* 是在创建服务器时为管道提供的名称。

<span id="________port_________Socket"></span><span id="________port_________socket"></span><span id="________PORT_________SOCKET"></span>**端口 =** *套接字*  
如果使用 TCP 或 SSL 协议， *套接字* 就是创建服务器时所用的同一个套接字端口号。

<span id="clicon"></span><span id="CLICON"></span>**clicon**  
指定服务器将尝试通过反向连接连接到中继器。 当且仅当服务器使用 **clicon** 时， *ClientTransport* 才能使用 **clicon** 。 在大多数情况下，在使用反向连接时，会在服务器之前启动 repeater。

<span id="port_________COMPort"></span><span id="port_________comport"></span><span id="PORT_________COMPORT"></span>**端口 =** *COMPort*  
如果使用 COM 协议， *COMPort* 将指定要使用的 com 端口。 前缀 "COM" 是可选的，例如，"com2" 和 "2" 都是可接受的。

<span id="baud_________BaudRate"></span><span id="baud_________baudrate"></span><span id="BAUD_________BAUDRATE"></span>**波特 =** *波特率*  
如果使用 COM 协议， *波特率* 应与创建服务器时选择的波特率匹配。

<span id="channel_________COMChannel"></span><span id="channel_________comchannel"></span><span id="CHANNEL_________COMCHANNEL"></span>**通道 =** *COMChannel*  
如果使用 COM 协议，则 *COMChannel* 应与创建服务器时选择的通道号匹配。

<span id="________password_________Password"></span><span id="________password_________password"></span><span id="________PASSWORD_________PASSWORD"></span>**密码 =** *密码*  
如果在创建服务器时使用了密码，则必须提供 *密码* 才能创建调试客户端。 它必须与原始密码匹配。 密码是区分大小写的。 如果提供了错误的密码，错误消息会指定 "错误 0x80004005"。

<span id="________ipversion_6"></span><span id="________IPVERSION_6"></span>**ipversion = 6**  
适用于 Windows 6.6.07 和更早版本的 (调试工具仅) 强制调试器在使用 TCP 连接到 Internet 时使用 IP 版本6而不是版本4。 在 Windows Vista 和更高版本中，调试器会尝试自动默认为 IP 版本6，这不需要此选项。

<span id="ServerTransport"></span><span id="servertransport"></span><span id="SERVERTRANSPORT"></span>ServerTransport  
指定将在客户端连接到中继器时使用的协议设置。 可能的协议语法为：

```dbgcmd
npipe:pipe=PipeName[,hidden][,password=Password][,IcfEnable] 
tcp:port=Socket[,hidden][,password=Password][,IcfEnable] 
tcp:port=Socket,clicon=Client[,password=Password] 
com:port=COMPort,baud=BaudRate,channel=COMChannel[,hidden][,password=Password] 
```

协议参数具有以下含义：

<span id="________pipe_________PipeName"></span><span id="________pipe_________pipename"></span><span id="________PIPE_________PIPENAME"></span>**管道 =** *PipeName*  
如果使用 NPIPE 或 SPIPE 协议，则 *PipeName* 是将充当管道名称的字符串。 每个管道名称应标识唯一的中继器。 如果尝试重用管道名称，您将收到一条错误消息。 *PipeName* 不得包含空格或引号。 *PipeName* 可以包含数字 **printf** 样式格式代码，如 **% x** 或 **% d**。 中继器会将此替换为 DbEngPrx 的进程 ID。 第二个这样的代码将替换为 DbEngPrx 的线程 ID。

<span id="________port_________Socket"></span><span id="________port_________socket"></span><span id="________PORT_________SOCKET"></span>**端口 =** *套接字*  
使用 TCP 或 SSL 协议时， *套接字* 为套接字端口号。

还可以指定由冒号分隔的一系列端口。 DbEngPrx 将检查此范围内的每个端口，查看其是否可用。 如果它找到一个可用端口且不发生错误，则会创建中继器。 客户端必须指定用于连接到中继器的实际端口。 若要确定实际端口，请搜索中继器;当显示此中继器时，该端口后跟两个数字，由冒号分隔。 第一个数字将是使用的实际端口;可以忽略第二个。 例如，如果将端口指定为 **port = 51： 60**，并实际使用端口53，搜索结果将显示 "port = 53： 60"。  (如果你使用 **clicon** 参数建立反向连接，则客户端可以通过这种方式指定一定范围的端口，而中继器必须指定使用的实际端口。 ) 

<span id="clicon_Client"></span><span id="clicon_client"></span><span id="CLICON_CLIENT"></span>**clicon =**<em>客户端</em>  
使用 TCP 或 SSL 协议并指定 **clicon** 参数时，将打开 *反向连接* 。 这意味着 repeater 将尝试连接到客户端，而不是让客户端启动该联系人。 如果防火墙阻止连接正常，这会很有用。 *客户端* 指定客户端所在计算机的网络名称或 IP 地址，或将在该计算机上创建客户端。  (的两个初始反斜杠 \\ \) 是可选的。

由于中继器查找一个特定客户端，因此，如果使用此方法，则无法将多个客户端连接到中继器。 如果连接被拒绝或已损坏，则必须重新启动 repeater。

当使用 **clicon** 时，最好是在创建中继器之前启动客户端，不过，在客户端) 之前，也可以在客户端之前以通常顺序 (中继器。

<span id="port_________COMPort"></span><span id="port_________comport"></span><span id="PORT_________COMPORT"></span>**端口 =** *COMPort*  
使用 COM 协议时， *COMPort* 指定要使用的 com 端口。 前缀 "COM" 是可选的，例如，"com2" 和 "2" 都是可接受的。 不能在 *ClientTransport* 和 *ServerTransport* 中使用同一 COM 端口。

<span id="baud_________BaudRate"></span><span id="baud_________baudrate"></span><span id="BAUD_________BAUDRATE"></span>**波特 =** *波特率*  
使用 COM 协议时， *波特率* 指定连接的运行波特率。 允许硬件支持的任何波特率。 如果同时使用 *ClientTransport* 和 *SERVERTRANSPORT* 中的 COM 协议，则可以指定不同的波特率，但是，速度较慢的速率将是客户端和服务器之间的通信速度的限制。

<span id="channel_________COMChannel"></span><span id="channel_________comchannel"></span><span id="CHANNEL_________COMCHANNEL"></span>**通道 =** *COMChannel*  
如果使用 COM 协议， *COMChannel* 将指定要在与客户端通信时使用的 com 通道。 该值可以是0到254之间的任何值（含0和）。 你可以使用一个 COM 端口来实现使用不同通道号的多个连接。  (这不同于将 COM 端口用于调试电缆-在这种情况下，不能在 COM 端口中使用通道。 ) 

<span id="hidden"></span><span id="HIDDEN"></span>**消隐**  
当另一个调试器显示所有活动的服务器时，禁止显示服务器。

<span id="________password_________Password"></span><span id="________password_________password"></span><span id="________PASSWORD_________PASSWORD"></span>**密码 =** *密码*  
要求客户端提供指定的密码才能连接到调试会话。 *密码* 可以是任何字母数字字符串。

<span id="IcfEnable"></span><span id="icfenable"></span><span id="ICFENABLE"></span>**IcfEnable**  
当 Internet 连接防火墙处于活动状态时，使调试器为 TCP 或命名管道通信启用必要的端口连接。 默认情况下，Internet 连接防火墙禁用这些协议使用的端口。 当 **IcfEnable** 与 TCP 连接一起使用时，调试器会使 Windows 打开 *Socket* 参数指定的端口。 当 **IcfEnable** 与命名管道连接一起使用时，调试器会使 Windows 打开用于命名管道 (端口139和 445) 的端口。 在连接终止后，调试器不会关闭这些端口。

### <a name="span-idstep_three__starting_the_clientspanspan-idstep_three__starting_the_clientspanstep-three-starting-the-client"></a><span id="step_three__starting_the_client"></span><span id="STEP_THREE__STARTING_THE_CLIENT"></span>步骤3：启动客户端

客户端应为调试客户端或智能客户端（无论哪一项对应于你的服务器类型）。 有关详细信息，请参阅 [**激活调试客户端**](activating-a-debugging-client.md)、 [**激活智能客户端**](activating-a-smart-client.md)或 [**(内核模式激活智能客户端)**](activating-a-smart-client--kernel-mode-.md)。

如果服务器拒绝连接 (例如，如果提供了不正确的密码) ，则中继器和客户端都将关闭。 您必须重新启动这两个服务以与服务器重新建立连接。

 

 





