---
title: .server（创建调试服务器）
description: .Server 命令启动调试服务器，从而允许为当前调试会话的远程连接。
ms.assetid: 39979a53-d6e7-4660-8884-3044da0b60de
keywords:
- 创建调试服务器 (.server) 命令
- 通过调试程序，创建调试服务器 (.server) 命令的远程调试
- .server （创建调试服务器） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .server (Create Debugging Server)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: bbdc4d1fdf3d16e42e98cb61a0d036ff67d6a5b4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63338838"
---
# <a name="server-create-debugging-server"></a>.server（创建调试服务器）


**.Server**命令启动调试服务器，从而允许为当前调试会话的远程连接。

```dbgcmd
.server npipe:pipe=PipeName[,hidden][,password=Password][,IcfEnable] 
.server tcp:port=Socket[,hidden][,password=Password][,ipversion=6][,IcfEnable] 
.server tcp:port=Socket,clicon=Client[,password=Password][,ipversion=6] 
.server com:port=COMPort,baud=BaudRate,channel=COMChannel[,hidden][,password=Password] 
.server spipe:proto=Protocol,{certuser=Cert|machuser=Cert},pipe=PipeName[,hidden][,password=Password] 
.server ssl:proto=Protocol,{certuser=Cert|machuser=Cert},port=Socket[,hidden][,password=Password] 
.server ssl:proto=Protocol,{certuser=Cert|machuser=Cert},port=Socket,clicon=Client[,password=Password] 
```

## <a name="span-idddkmetacreatedebuggingserverdbgspanspan-idddkmetacreatedebuggingserverdbgspanparameters"></a><span id="ddk_meta_create_debugging_server_dbg"></span><span id="DDK_META_CREATE_DEBUGGING_SERVER_DBG"></span>参数


<span id="_______PipeName______"></span><span id="_______pipename______"></span><span id="_______PIPENAME______"></span> *PipeName*   
当使用 NPIPE 或 SPIPE 协议时， *PipeName*是一个字符串，将作为管道的名称。 每个管道名称应标识唯一的调试服务器。 如果您尝试重复使用的管道名称，将收到一条错误消息。 *PipeName*不能包含空格或引号。 *PipeName*可以包含数值**printf**-样式格式代码，例如 %x 或 %d。 调试器将替换此调试器的进程 ID。 第二个此类代码将替换为在调试器的线程 ID。

<span id="_______Socket______"></span><span id="_______socket______"></span><span id="_______SOCKET______"></span> *Socket*   
当使用 TCP 或 SSL 协议时，*套接字*是套接字端口号。

还有可能要指定一系列由冒号分隔的端口。 调试器将检查在此范围内，以查看它是否是免费的每个端口。 如果它找到了可用端口，并且不会发生错误，将创建调试服务器。 调试客户端必须指定用于连接到服务器的实际端口。 若要确定实际端口，请使用任何一种方法中所述[**搜索调试服务器**](searching-for-debugging-servers.md); 当显示此调试服务器时，该端口将后跟分号分隔的两个数字。 第一个数字将使用; 的实际端口可以忽略第二个。 例如，如果该端口指定为端口 = 51:60，和实际使用端口 53，搜索结果将显示"端口 = 53:60"。 (如果使用的**clicon**参数，以建立反向连接，调试客户端可以指定一系列端口以这种方式，而服务器必须指定使用的实际端口。)

<span id="clicon_Client"></span><span id="clicon_client"></span><span id="CLICON_CLIENT"></span>**clicon=**<em>Client</em>  
在使用 TCP 或 SSL 协议时， **clicon**指定参数，则*反向连接*将打开。 这意味着调试服务器将尝试连接到调试客户端，而不是让客户端启动联系人。 这可以是防火墙阻止中常规方向的连接的情况下很有用。 *客户端*指定的计算机在其调试客户端存在，或将创建的网络名称。 这两个初始反斜杠 (\\ \)都是可选的。

当**clicon**是使用，最好是启动调试客户端，然后创建调试服务器后，虽然还允许常规顺序 （客户端之前的服务器）。 另一个调试器显示所有活动服务器时，不会出现的反向连接服务器。

<span id="_______COMPort______"></span><span id="_______comport______"></span><span id="_______COMPORT______"></span> *COMPort*   
当使用 COM 协议时， *COMPort*指定要使用的 COM 端口。 前缀 COM 是可选的 （例如，"com2"和"2"是可接受）。

<span id="_______BaudRate______"></span><span id="_______baudrate______"></span><span id="_______BAUDRATE______"></span> *BaudRate*   
当使用 COM 协议时， *BaudRate*指定连接将在其中运行的波特率。 允许使用任何支持的硬件的波特率。

<span id="_______COMChannel______"></span><span id="_______comchannel______"></span><span id="_______COMCHANNEL______"></span> *COMChannel*   
如果使用 COM 协议，则*COMChannel*指定与调试客户端的通信中使用的 COM 通道。 这可以是 0 和 254 之间 （含） 之间的任何值。

<span id="_______Protocol______"></span><span id="_______protocol______"></span><span id="_______PROTOCOL______"></span> *Protocol*   
如果使用 SSL 或 SPIPE 协议，则*协议*指定安全通道 （S-通道） 协议。 这可以是字符串 tls1、 pct1、 ssl2 或 ssl3 的任何一个。

<span id="_______Cert______"></span><span id="_______cert______"></span><span id="_______CERT______"></span> *Cert*   
如果使用 SSL 或 SPIPE 协议，则*Cert*指定的证书。 这可以是证书名称或证书的指纹 （给定证书的管理单元的十六进制数字的字符串）。 如果语法**certuser =**<em>Cert</em>是使用，调试器将查找系统存储 （默认存储） 中的证书。 如果语法**machuser =**<em>Cert</em>是使用，调试器将查找计算机存储区中的证书。 指定的证书必须支持服务器身份验证。

<span id="_______hidden______"></span><span id="_______HIDDEN______"></span> **hidden**   
可防止服务器出现时另一个调试器将显示所有活动服务器。

<span id="password_Password"></span><span id="password_password"></span><span id="PASSWORD_PASSWORD"></span>**password=**<em>Password</em>  
需要调试客户端提供指定的密码才能连接到调试会话。 *密码*可以是任何字母数字字符串，最多 12 个字符的长度。

<span id="_______ipversion_6______"></span><span id="_______IPVERSION_6______"></span> **ipversion=6**   
(调试工具的 Windows 6.6.07，之前仅)强制将 IP 版本 6 调试器而不是版本 4 时使用 TCP 连接到 Internet。 在 Windows Vista 和更高版本中，调试器将尝试自动默认为 IP 版本 6，这使得此选项不必要。

<span id="_______IcfEnable______"></span><span id="_______icfenable______"></span><span id="_______ICFENABLE______"></span> **IcfEnable**   
使调试器以启用必要的端口连接的 TCP 或命名的管道通信，Internet 连接防火墙处于活动状态时。 默认情况下，Internet 连接防火墙禁用这些协议使用的端口。 当**IcfEnable**使用与 TCP 连接，调试器会导致 Windows 套接字参数指定的端口打开。 当**IcfEnable**使用通过命名的管道连接，调试器会导致 Windows 打开端口用于命名管道 （端口 139 和 445）。 在连接终止后，调试器不会关闭这些端口。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>模式</strong></p></td>
<td align="left"><p>用户模式下，内核模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>实时、 崩溃转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关如何启动调试服务器的完整详细信息，请参阅[**激活调试服务器**](activating-a-debugging-server.md)。 有关示例，请参阅[客户端和服务器示例](client-and-server-examples.md)。

<a name="remarks"></a>备注
-------

此命令将当前调试器为调试服务器。 这使您可以启动服务器后调试器已在运行，而-server[命令行选项](command-line-options.md)才会启动调试器时发出。

这允许调试客户端连接到当前调试会话。 请注意，可以启动多个服务器使用不同的选项，允许不同的调试客户端要加入会话。

 

 





