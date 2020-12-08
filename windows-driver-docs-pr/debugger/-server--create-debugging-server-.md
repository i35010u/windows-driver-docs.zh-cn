---
title: .server（创建调试服务器）
description: 服务器命令启动调试服务器，允许远程连接到当前的调试会话。
keywords:
- " ( server) 命令创建调试服务器"
- 通过调试器远程调试，创建调试服务器 () 命令
- 。服务器 (创建调试服务器) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .server (Create Debugging Server)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 2dfe35701a6540a059752f54fe222c5d1e529f49
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96802081"
---
# <a name="server-create-debugging-server"></a>.server（创建调试服务器）


**服务器** 命令启动调试服务器，允许远程连接到当前的调试会话。

```dbgcmd
.server npipe:pipe=PipeName[,hidden][,password=Password][,IcfEnable] 
.server tcp:port=Socket[,hidden][,password=Password][,ipversion=6][,IcfEnable] 
.server tcp:port=Socket,clicon=Client[,password=Password][,ipversion=6] 
.server com:port=COMPort,baud=BaudRate,channel=COMChannel[,hidden][,password=Password] 
.server spipe:proto=Protocol,{certuser=Cert|machuser=Cert},pipe=PipeName[,hidden][,password=Password] 
.server ssl:proto=Protocol,{certuser=Cert|machuser=Cert},port=Socket[,hidden][,password=Password] 
.server ssl:proto=Protocol,{certuser=Cert|machuser=Cert},port=Socket,clicon=Client[,password=Password] 
```

## <a name="span-idddk_meta_create_debugging_server_dbgspanspan-idddk_meta_create_debugging_server_dbgspanparameters"></a><span id="ddk_meta_create_debugging_server_dbg"></span><span id="DDK_META_CREATE_DEBUGGING_SERVER_DBG"></span>参数


<span id="_______PipeName______"></span><span id="_______pipename______"></span><span id="_______PIPENAME______"></span>*PipeName*   
如果使用 NPIPE 或 SPIPE 协议，则 *PipeName* 是将充当管道名称的字符串。 每个管道名称都应标识唯一的调试服务器。 如果尝试重用管道名称，您将收到一条错误消息。 *PipeName* 不得包含空格或引号。 *PipeName* 可以包含数字 **printf** 样式格式代码，如% x 或% d。 调试器会将此替换为调试器的进程 ID。 第二个这样的代码将替换为调试器的线程 ID。

<span id="_______Socket______"></span><span id="_______socket______"></span><span id="_______SOCKET______"></span>*套接字*   
使用 TCP 或 SSL 协议时， *套接字* 为套接字端口号。

还可以指定由冒号分隔的一系列端口。 调试器将检查此范围内的每个端口，查看其是否可用。 如果它找到一个可用端口而不发生错误，则将创建调试服务器。 调试客户端将必须指定用于连接到服务器的实际端口。 若要确定实际端口，请使用 [**搜索调试服务器**](searching-for-debugging-servers.md)中所述的任何方法;当显示此调试服务器时，端口后跟两个数字，由冒号分隔。 第一个数字将是使用的实际端口;可以忽略第二个。 例如，如果将端口指定为 port = 51：60，并实际使用端口53，搜索结果将显示 "port = 53： 60"。  (如果使用 **clicon** 参数建立反向连接，则调试客户端可以通过这种方式指定一定范围的端口，而服务器必须指定使用的实际端口。 ) 

<span id="clicon_Client"></span><span id="clicon_client"></span><span id="CLICON_CLIENT"></span>**clicon =**<em>客户端</em>  
使用 TCP 或 SSL 协议并指定 **clicon** 参数时，将打开 *反向连接* 。 这意味着，调试服务器将尝试连接到调试客户端，而不是让客户端启动该联系人。 如果防火墙阻止连接正常，这会很有用。 *客户端* 指定在其上存在或将创建调试客户端的计算机的网络名称。  (的两个初始反斜杠 \\ \) 是可选的。

当使用 **clicon** 时，最好在创建调试服务器之前启动调试客户端，不过，在客户端) 之前通常 (服务器的顺序也是允许的。 当另一个调试器显示所有活动的服务器时，将不会显示反向连接服务器。

<span id="_______COMPort______"></span><span id="_______comport______"></span><span id="_______COMPORT______"></span>*COMPort*   
使用 COM 协议时， *COMPort* 指定要使用的 com 端口。 前缀 COM 是可选的 (例如，"com2" 和 "2" 都是可接受的) 。

<span id="_______BaudRate______"></span><span id="_______baudrate______"></span><span id="_______BAUDRATE______"></span>*波特率*   
使用 COM 协议时， *波特率* 指定连接的运行波特率。 允许硬件支持的任何波特率。

<span id="_______COMChannel______"></span><span id="_______comchannel______"></span><span id="_______COMCHANNEL______"></span>*COMChannel*   
如果使用 COM 协议，则 *COMChannel* 指定要用于与调试客户端进行通信的 com 通道。 该值可以是0到254之间的任何值（含0和）。

<span id="_______Protocol______"></span><span id="_______protocol______"></span><span id="_______PROTOCOL______"></span>*协议*   
如果使用 SSL 或 SPIPE 协议，则 *协议* 指定 (S 通道) 协议的安全通道。 这可以是字符串是 tls1、是 pct1、是 ssl2 或 ssl3 中的任何一个。

<span id="_______Cert______"></span><span id="_______cert______"></span><span id="_______CERT______"></span>*证书*   
如果使用 SSL 或 SPIPE 协议，则 *Cert* 指定证书。 这可以是证书名称，也可以是证书的指纹 (由证书的管理单元) 指定的十六进制数字的字符串。 如果使用语法 **certuser =**<em>Cert</em> ，则调试器将在默认存储)  (系统存储中查找证书。 如果使用语法 **machuser =**<em>Cert</em> ，则调试器将在计算机存储中查找证书。 指定的证书必须支持服务器身份验证。

<span id="_______hidden______"></span><span id="_______HIDDEN______"></span>**隐藏**   
当另一个调试器显示所有活动的服务器时，禁止显示服务器。

<span id="password_Password"></span><span id="password_password"></span><span id="PASSWORD_PASSWORD"></span>**密码 =**<em>密码</em>  
需要调试客户端提供指定的密码才能连接到调试会话。 *密码* 可以是任意字母数字字符串，长度最多为12个字符。

<span id="_______ipversion_6______"></span><span id="_______IPVERSION_6______"></span>**ipversion = 6**   
适用于 Windows 6.6.07 和更早版本的 (调试工具仅) 强制调试器在使用 TCP 连接到 Internet 时使用 IP 版本6而不是版本4。 在 Windows Vista 和更高版本中，调试器会尝试自动默认为 IP 版本6，这不需要此选项。

<span id="_______IcfEnable______"></span><span id="_______icfenable______"></span><span id="_______ICFENABLE______"></span>**IcfEnable**   
当 Internet 连接防火墙处于活动状态时，使调试器为 TCP 或命名管道通信启用必要的端口连接。 默认情况下，Internet 连接防火墙禁用这些协议使用的端口。 当 **IcfEnable** 与 TCP 连接一起使用时，调试器会使 Windows 打开 Socket 参数指定的端口。 当 **IcfEnable** 与命名管道连接一起使用时，调试器会使 Windows 打开用于命名管道 (端口139和 445) 的端口。 在连接终止后，调试器不会关闭这些端口。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>交货</strong></p></td>
<td align="left"><p>用户模式，内核模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>实时，故障转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>all</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关如何启动调试服务器的完整详细信息，请参阅 [**激活调试服务器**](activating-a-debugging-server.md)。 有关示例，请参阅 [客户端和服务器示例](client-and-server-examples.md)。

<a name="remarks"></a>备注
-------

此命令会将当前调试器转换为调试服务器。 这允许您在调试器已经运行后启动服务器，而只有在启动调试器时才会发出-server [命令行选项](command-line-options.md) 。

这允许调试客户端连接到当前的调试会话。 请注意，可以使用不同的选项启动多个服务器，允许不同类型的调试客户端加入会话。

 

 





