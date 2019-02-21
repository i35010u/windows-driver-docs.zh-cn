---
title: 激活进程服务器
description: 若要激活进程服务器，打开提升的命令提示符窗口 （以管理员身份运行），并输入 dbgsrv 命令。
ms.assetid: 566a4f64-8a14-469b-b50c-20e3c00aa2f8
keywords:
- 激活调试进程服务器 Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- Activating a Process Server
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ecdda091634cab38db94f82ebcf2faf702898e45
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56540942"
---
# <a name="activating-a-process-server"></a>激活进程服务器


有关 Windows 调试工具中包括的进程服务器称为 DbgSrv (dbgsrv.exe)。 若要激活进程服务器，打开提升的命令提示符窗口 （以管理员身份运行），并输入**dbgsrv**命令。

**请注意**  可以激活进程服务器，无需具有提升的权限，并调试客户端将能够连接到服务器。 但是，客户端将不能发现进程服务器，除非它已激活使用提升的权限。 有关如何发现调试服务器的信息，请参阅[搜索的进程服务器](searching-for-process-servers.md)。

 

DbgSrv 支持多个传输协议： 命名管道 (NPIPE)，TCP、 COM 端口、 安全管道 (SPIPE) 和安全套接字层 (SSL)。

```console
dbgsrv -t npipe:pipe=PipeName[,hidden][,password=Password][,IcfEnable] [[-sifeo Executable] -c[s] AppCmdLine] [-x | -pc] 

dbgsrv -t tcp:port=Socket[,hidden][,password=Password][,ipversion=6][,IcfEnable] [[-sifeo Executable] -c[s] AppCmdLine] [-x | -pc] 

dbgsrv -t tcp:port=Socket,clicon=Client[,password=Password][,ipversion=6] [[-sifeo Executable] -c[s] AppCmdLine] [-x | -pc] 

dbgsrv -t com:port=COMPort,baud=BaudRate,channel=COMChannel[,hidden][,password=Password] [[-sifeo Executable] -c[s] AppCmdLine] [-x | -pc] 

dbgsrv -t spipe:proto=Protocol,{certuser=Cert|machuser=Cert},pipe=PipeName[,hidden][,password=Password] [[-sifeo Executable] -c[s] AppCmdLine] [-x | -pc] 

dbgsrv -t ssl:proto=Protocol,{certuser=Cert|machuser=Cert},port=Socket[,hidden][,password=Password] [[-sifeo Executable] -c[s] AppCmdLine] [-x | -pc] 

dbgsrv -t ssl:proto=Protocol,{certuser=Cert|machuser=Cert},port=Socket,clicon=Client[,password=Password] [[-sifeo Executable] -c[s] AppCmdLine] [-x | -pc] 
```

## <span id="ddk_activating_a_process_server_dbg"></span><span id="DDK_ACTIVATING_A_PROCESS_SERVER_DBG"></span>


上述命令中的参数具有以下可能值：

<span id="________pipe_________PipeName"></span><span id="________pipe_________pipename"></span><span id="________PIPE_________PIPENAME"></span> **pipe=** *PipeName*  
当使用 NPIPE 或 SPIPE 协议时， *PipeName*是一个字符串，将作为管道的名称。 每个管道名称应标识唯一进程服务器。 如果您尝试重复使用的管道名称，将收到一条错误消息。 *PipeName*不能包含空格或引号。 *PipeName*可以包含数值**printf**的样式设置代码格式，如 **%x**或 **%d**。 进程服务器将替换为此进程 ID DbgSrv。 第二个此类代码将替换为线程 ID DbgSrv。

**请注意**  可能需要启用文件和打印机共享正在运行的进程服务器的计算机上。 在控制面板中，导航到**网络和 Internet&gt;网络和共享中心&gt;高级共享设置**。 选择**启用文件和打印机共享**。

 

<span id="________port_________Socket"></span><span id="________port_________socket"></span><span id="________PORT_________SOCKET"></span> **port=** *Socket*  
当使用 TCP 或 SSL 协议时，*套接字*是套接字端口号。

还有可能要指定一系列由冒号分隔的端口。 DbgSrv 将检查在此范围内，以查看它是否是免费的每个端口。 如果它找到了可用端口，并且不会发生错误，将创建进程服务器。 智能客户端必须指定用于连接到服务器的实际端口。 若要确定实际端口，请使用任何一种方法中所述[**搜索的进程服务器**](searching-for-process-servers.md); 时显示此进程服务器，则该端口将后跟分号分隔的两个数字。 第一个数字将使用; 的实际端口可以忽略第二个。 例如，如果该端口指定为**端口 = 51:60**，和实际使用端口 53，搜索结果将显示"端口 = 53:60"。 (如果使用的**clicon**参数，以建立反向连接，智能客户端可以指定一系列端口以这种方式，而进程服务器必须指定使用的实际端口。)

<span id="________clicon_________Client"></span><span id="________clicon_________client"></span><span id="________CLICON_________CLIENT"></span> **clicon=** *Client*  
在使用 TCP 或 SSL 协议时， **clicon**指定参数，则*反向连接*将打开。 这意味着，进程服务器将尝试连接到智能客户端，而不是让客户端启动联系人。 这可以是防火墙阻止中常规方向的连接的情况下很有用。 *客户端*指定网络名称或智能客户端在其存在或将创建的计算机的 IP 地址。 这两个初始反斜杠 (\\ \)都是可选的。

由于进程服务器正在寻找一个特定的客户端，因此不能多个客户端连接到服务器如果使用此方法。 如果连接被拒绝或已损坏，必须重启进程服务器。 当有人使用时，将不会出现反向连接进程服务器 **-QR**命令行选项以显示所有活动服务器。

**请注意**  时**clicon**是使用，最好是启动智能客户端，然后创建进程服务器，尽管还允许常规顺序 （客户端之前的服务器）。

 

<span id="port_________COMPort"></span><span id="port_________comport"></span><span id="PORT_________COMPORT"></span>**port=** *COMPort*  
当使用 COM 协议时， *COMPort*指定要使用的 COM 端口。 前缀"COM"是可选的--例如，"com2"和"2"是可接受。

<span id="baud_________BaudRate"></span><span id="baud_________baudrate"></span><span id="BAUD_________BAUDRATE"></span>**baud=** *BaudRate*  
当使用 COM 协议时， *BaudRate*指定连接将在其中运行的波特率。 允许使用任何支持的硬件的波特率。

<span id="channel_________COMChannel"></span><span id="channel_________comchannel"></span><span id="CHANNEL_________COMCHANNEL"></span>**channel=** *COMChannel*  
如果使用 COM 协议，则*COMChannel*指定与调试客户端的通信中使用的 COM 通道。 这可以是 0 和 254 之间 （含） 之间的任何值。 有关使用不同的频道号的多个连接，可以使用一个 COM 端口。 （这与调试电缆的 COM 端口用于不同--在这种情况下无法在 COM 端口使用通道。）

<span id="________proto_________Protocol"></span><span id="________proto_________protocol"></span><span id="________PROTO_________PROTOCOL"></span> **proto=** *Protocol*  
如果使用 SSL 或 SPIPE 协议，则*协议*指定安全通道 （S-通道） 协议。 这可以是字符串 tls1、 pct1、 ssl2 或 ssl3 的任何一个。

<span id="Cert"></span><span id="cert"></span><span id="CERT"></span>*Cert*  
如果使用 SSL 或 SPIPE 协议，则*Cert*指定的证书。 这可以是证书名称或证书的指纹 （给定证书的管理单元的十六进制数字的字符串）。 如果语法**certuser =**<em>Cert</em>是使用，调试器将查找系统存储 （默认存储） 中的证书。 如果语法**machuser =**<em>Cert</em>是使用，调试器将查找计算机存储区中的证书。 指定的证书必须支持服务器身份验证。

<span id="________hidden"></span><span id="________HIDDEN"></span> **hidden**  
可防止出现当有人使用进程服务器 **-QR**命令行选项以显示所有活动服务器。

<span id="________password_________Password"></span><span id="________password_________password"></span><span id="________PASSWORD_________PASSWORD"></span> **password=** *Password*  
需要智能客户端才能连接到进程服务器提供指定的密码。 *密码*可以是任何字母数字字符串，最多 12 个字符的长度。

**警告**  使用 TCP、 NPIPE 或 COM 协议使用密码只提供少量的保护，因为未加密密码。 当使用 SSL 或 SPIPE 协议使用密码时，对其进行加密。 如果你想要建立安全的远程会话，必须使用 SSL 或 SPIPE 协议。

 

<span id="________ipversion_6"></span><span id="________IPVERSION_6"></span> **ipversion=6**  
(调试工具的 Windows 6.6.07，之前仅)强制将 IP 版本 6 调试器而不是版本 4 时使用 TCP 连接到 Internet。 在 Windows Vista 和更高版本中，调试器将尝试自动默认为 IP 版本 6，这使得此选项不必要。

<span id="________IcfEnable"></span><span id="________icfenable"></span><span id="________ICFENABLE"></span> **IcfEnable**  
使调试器以启用必要的端口连接的 TCP 或命名的管道通信，Internet 连接防火墙处于活动状态时。 默认情况下，Internet 连接防火墙禁用这些协议使用的端口。 当**IcfEnable**使用与 TCP 连接，调试器会导致 Windows 以打开指定的端口*套接字*参数。 当**IcfEnable**使用通过命名的管道连接，调试器会导致 Windows 打开端口用于命名管道 （端口 139 和 445）。 在连接终止后，调试器不会关闭这些端口。

<span id="-sifeo__________Executable"></span><span id="-sifeo__________executable"></span><span id="-SIFEO__________EXECUTABLE"></span>**-sifeo** *可执行文件*  
挂起给定图像的图像文件执行选项 （ifeo 需要） 值。 *可执行文件*应包括可执行映像，包括文件扩展名的文件名称。 **-Sifeo**选项允许 DbgSrv 要设置为创建的映像 ifeo 需要调试器 **-c**选项，而不会导致因 ifeo 需要设置而递归调用。 可以使用此选项，仅当 **-c**使用。

<span id="________-c"></span><span id="________-C"></span> **-c**  
若要创建新的进程的原因 DbgSrv。 您可以用于创建你想要调试的进程。 这是类似于从调试器中，生成新的进程，只不过在创建时，此过程将不进行调试。 若要调试此进程，确定其 PID，并使用 **-p**选项启动智能客户端要调试该进程时。

<span id="s"></span><span id="S"></span>**s**  
将导致新创建过程将立即挂起。 如果使用此选项，则建议作为智能客户端，使用 CDB 和开始使用智能客户端 **-pb**命令行选项，结合 **-p PID**。 如果包括 **-pb**命令行，在过程上的选项将恢复时将调试器附加到它; 否则，您可以恢复与进程[  **~ \*m**](-m--resume-thread-.md)命令。

<span id="AppCmdLine"></span><span id="appcmdline"></span><span id="APPCMDLINE"></span>*AppCmdLine*  
指定要创建的进程的完整命令行。 *AppCmdLine*可以是 Unicode 或 ASCII 字符串，并且可以包含任何可打印字符。 之后，在出现的所有文本 **-c\[s\]** 将被参数以便构成的字符串*AppCmdLine*。

<span id="-x"></span><span id="-X"></span>**-x**  
导致要忽略的命令行的其余部分。 此选项非常有用，如果从应用程序可能不需要的文本追加到其命令行启动 DbgSrv。

<span id="________-pc"></span><span id="________-PC"></span> **-pc**  
导致要忽略的命令行的其余部分。 此选项非常有用，如果从应用程序可能不需要的文本追加到其命令行启动 DbgSrv。 如果会导致语法错误**pc**是 DbgSrv 命令行上的最后一个元素。 此限制，除了**pc**等同于 **-x**。

可以在一台计算机上启动任意数量的进程服务器。 但是，这是通常不必要的因为一个进程服务器可由任意数量的智能客户端 （每个参与不同的调试会话中）。

 

 





