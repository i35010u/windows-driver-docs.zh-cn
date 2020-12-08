---
title: 文件连接到远程存根
description: 文件连接到远程存根
keywords:
- 文件连接到远程存根
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 298b5e95adbf14f35a41dc87d8dcf5a95c8bb7eb
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96833667"
---
# <a name="file--connect-to-remote-stub"></a>文件 | 连接到远程存根


单击 "**文件**" 菜单上的 "**连接到远程存根**"，使 WinDbg 成为智能客户端，并连接到进程服务器或 KD 连接服务器。

此命令等效于在用户模式下使用-premote 命令行选项，或使用内核模式下的-k kdsrv 传输协议命令行选项。 仅当 WinDbg 处于休眠模式时，才能使用此命令。

不能使用此命令连接到调试服务器;为此，请使用 [文件 |改为连接到远程会话](file---connect-to-remote-session.md) 。

### <a name="span-idconnect_to_remote_stub_server_dialog_boxspanspan-idconnect_to_remote_stub_server_dialog_boxspanconnect-to-remote-stub-server-dialog-box"></a><span id="connect_to_remote_stub_server_dialog_box"></span><span id="CONNECT_TO_REMOTE_STUB_SERVER_DIALOG_BOX"></span>"连接到远程存根服务器" 对话框

当你单击 " **连接到远程存根**" 时，将显示 " **连接到远程存根服务器** " 对话框。 您可以使用此对话框输入远程连接参数或浏览进程服务器和 KD 连接服务器的列表。

若要手动指定远程连接参数，请在 " **连接字符串** " 框中输入以下字符串之一：

```text
npipe:server=Server,pipe=PipeName[,password=Password] 

tcp:server=Server,port=Socket[,password=Password][,ipversion=6]

tcp:clicon=Server,port=Socket[,password=Password][,ipversion=6]

com:port=COMPort,baud=BaudRate,channel=COMChannel[,password=Password] 

spipe:proto=Protocol,{certuser=Cert|machuser=Cert},server=Server,pipe=PipeName[,password=Password] 

ssl:proto=Protocol,{certuser=Cert|machuser=Cert},server=Server,port=Socket[,password=Password]

ssl:proto=Protocol,{certuser=Cert|machuser=Cert},clicon=Server,port=Socket[,password=Password]
```

上述选项中的各种参数具有以下可能值：

<span id="Server"></span><span id="server"></span><span id="SERVER"></span>*服务*  
在其上创建进程服务器或 KD 连接服务器的计算机的网络名称。 不要在此名称之前加上反斜杠 (**\\\\**) 。

<span id="PipeName"></span><span id="pipename"></span><span id="PIPENAME"></span>*PipeName*  
如果使用 NPIPE 或 SPIPE 协议，则 *PipeName* 是在创建服务器时为管道提供的名称。

<span id="Socket"></span><span id="socket"></span><span id="SOCKET"></span>*片*  
如果使用 TCP 或 SSL 协议， *套接字* 就是创建服务器时所用的同一个套接字端口号。

<span id="COMPort"></span><span id="comport"></span><span id="COMPORT"></span>*COMPort*  
如果使用 COM 协议， *COMPort* 将指定要使用的 COM 端口。 "COM" 前缀是可选的 (例如，"com2" 和 "2" 都是正确的) 。

<span id="BaudRate"></span><span id="baudrate"></span><span id="BAUDRATE"></span>*波特率*  
如果使用 COM 协议， *波特率* 应与创建服务器时选择的波特速率匹配。

<span id="COMChannel"></span><span id="comchannel"></span><span id="COMCHANNEL"></span>*COMChannel*  
如果使用 COM 协议，则 *COMChannel* 应与创建服务器时选择的通道号匹配。

<span id="Protocol"></span><span id="protocol"></span><span id="PROTOCOL"></span>*协议*  
 (Windows 2000 和更高版本) 如果使用 SSL 或 SPIPE 协议，则 *协议* 应与创建服务器时使用的安全协议匹配。

<span id="Cert"></span><span id="cert"></span><span id="CERT"></span>*Cert*  
 (Windows 2000 和更高版本中) 如果使用 SSL 或 SPIPE 协议，则应使用创建服务器时所用的相同的 **certuser =**<em>cert</em> 或 **machuser =**<em>cert</em> 参数。

<span id="clicon"></span><span id="CLICON"></span>**clicon**  
指定进程服务器或 KD 连接服务器将尝试通过反向连接连接到客户端。 当且仅当服务器使用 **clicon** 时，客户端才能使用 **clicon** 。 在大多数情况下，当使用反向连接时，智能客户端会在服务器之前启动。

<span id="Password"></span><span id="password"></span><span id="PASSWORD"></span>*权限*  
如果在创建服务器时使用了密码，则必须提供 *密码* 才能创建智能客户端。 此值必须与原始密码匹配。 密码是区分大小写的。 如果提供了错误的密码，错误消息会指定 "错误 0x80004005"。

<span id="ipversion_6"></span><span id="IPVERSION_6"></span>**ipversion = 6**  
 (适用于 Windows 6.6.07 和更早版本的调试工具仅) 强制调试器在使用 TCP 连接到 Internet 时使用 IP 版本6而不是版本4。 在 Windows Vista 和更高版本中，调试器会尝试自动默认为 IP 版本6，这不需要此选项。

你可以按 "**连接到远程存根服务器**" 对话框中的 "**浏览**" 按钮，并使用 "**浏览远程服务器**" 对话框，而不是手动指定远程连接参数。

### <a name="span-idbrowse_remote_servers_dialog_boxspanspan-idbrowse_remote_servers_dialog_boxspanbrowse-remote-servers-dialog-box"></a><span id="browse_remote_servers_dialog_box"></span><span id="BROWSE_REMOTE_SERVERS_DIALOG_BOX"></span>"浏览远程服务器" 对话框

在 " **浏览远程服务器** " 对话框的 " **计算机** " 文本框中，输入进程服务器或 KD 连接服务器正在其上运行的计算机的名称。  (两个初始反斜杠是可选的： "MyBox" 和 " \\ \\ MyBox" 都是正确的。 ) 然后按 "**刷新**" 按钮。

" **服务器** " 区域列出了运行在该计算机上的所有进程服务器和 KD 连接服务器。 选择列出的任何服务器，然后按 ENTER 或单击 **"确定"**。  (您还可以双击其中一个列出的服务器。 ) 所选进程服务器的正确连接字符串现在会显示在 "**连接到远程存根服务器**" 对话框的 "**连接字符串**" 框中。

如果服务器受密码保护，则连接字符串将包含 **password = \\**<em>。必须将星号 (</em> * \* * * ) 替换为实际密码。

指定服务器和密码后，单击 **"确定"** 打开连接。

" **浏览远程服务器** " 对话框中的服务器列表还可以包含不再存在但已正常关闭的服务器。 如果连接到这些不存在的服务器之一，你将收到一条错误消息。

服务器列表不包含调试服务器。 若要查看这些服务器，请使用 [文件 |"连接到远程会话](file---connect-to-remote-session.md) " 命令。

### <a name="span-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关详细信息以及其他联接远程存根会话的方法，请参阅 [**激活智能客户端**](activating-a-smart-client.md) 和 [**激活智能客户端 (内核模式)**](activating-a-smart-client--kernel-mode-.md)。

 

 





