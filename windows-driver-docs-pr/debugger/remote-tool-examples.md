---
title: 远程工具示例
description: 远程工具示例
keywords:
- 远程工具，示例
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: e270397b11a0508f2c1124e892bb8b97fd07773d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96816941"
---
# <a name="remote-tool-examples"></a>远程工具示例


## <span id="ddk_remote_tool_examples_dtools"></span><span id="DDK_REMOTE_TOOL_EXAMPLES_DTOOLS"></span>


本节中的示例演示如何使用远程工具，并显示示例输入和输出。

### <a name="span-idbasic_server_commandspanspan-idbasic_server_commandspanbasic-server-command"></a><span id="basic_server_command"></span><span id="BASIC_SERVER_COMMAND"></span>基本服务器命令

下面的命令启动计算机上的远程会话。

该命令使用 **/s** 参数来指示服务器端命令。 它使用命令 **cmd.exe** 启动 Windows 命令行界面 ( # A0) ，并为会话 **test1** 命名。

```console
remote /s cmd test1
```

在响应中，远程工具启动会话，并显示客户端将用于连接到会话的命令。

```console
**************************************
***********     REMOTE    ************
***********     SERVER    ************
**************************************
To Connect: Remote /C SERVER06 "test1"

Microsoft Windows XP [Version 5.1.2600]
(C) Copyright 1985-2001 Microsoft Corp.
```

### <a name="span-idbasic_client_commandspanspan-idbasic_client_commandspanbasic-client-command"></a><span id="basic_client_command"></span><span id="BASIC_CLIENT_COMMAND"></span>基本客户端命令

以下命令将连接到 Server01 计算机上的远程会话。 该命令使用 **/c** 参数来指示客户端命令。 它指定服务器计算机的名称 **Server01** 和该计算机上的会话名称 **test1**。

```console
remote /c server01 test1
```

在响应中，远程工具显示一条消息，报告客户端计算机已连接到服务器计算机上的会话。 该消息将显示服务器计算机的名称以及 (**Server04 user1**) 的本地用户。

```console
**************************************
***********     REMOTE    ************
***********     CLIENT    ************
**************************************
Connected...

Microsoft Windows XP [Version 5.1.2600]
(C) Copyright 1985-2001 Microsoft Corp.

C:\Program Files\Debugging Tools for Windows>
**Remote: Connected to SERVER04 user1 [Tue 9:39 AM]
```

客户端连接到服务器后，在客户端和服务器计算机上的命令提示符下键入的命令将显示在这两个显示器上。

例如，如果在客户端计算机的命令提示符下键入 **dir** ，则目录显示将显示在客户端和服务器计算机上的 "命令提示符" 窗口中。

### <a name="span-idusing_server_optionsspanspan-idusing_server_optionsspanusing-server-options"></a><span id="using_server_options"></span><span id="USING_SERVER_OPTIONS"></span>使用服务器选项

以下服务器端命令使用 NTSD 调试器启动远程会话。

该命令使用 **/s** 参数来指示服务器端命令。 下一个参数 **"ntsd-d-v"** 是启动调试器的控制台命令，以及调试器选项。 由于控制台命令包含空格，因此用引号将其引起来。 该命令包括会话名称 **debugit**。

该命令使用 **/u** 参数只允许计算机的管理员和 Domain01 中 User03 的特定用户连接到该会话。 它使用 **/f** 和 **/b** 选项在白色背景上指定黑色文本 (前景) 。

最后，该命令使用 **/-v** 参数将会话与用户查询不可见。 默认情况下，调试器会话可见。

```console
remote /s "ntsd -d -v" DebugIt /u Administrators /u Domain01\User03 
/f black /b white /-v
```

在响应中，远程工具创建一个名为 DebugIt 的会话，并启动具有指定参数的 NTSD。 此消息指示只有指定的用户有权进行连接。 它还会将 "命令" 窗口更改为指定的颜色。

```console
**************************************
***********     REMOTE    ************
***********     SERVER    ************
**************************************

Protected Server!  Only the following users or groups can connect:
    Administrators
    Domain01\User03
To Connect: Remote /C SERVER06 "debugit"

Microsoft Windows XP [Version 5.1.2600]
(C) Copyright 1985-2001 Microsoft Corp.
```

### <a name="span-idusing_client_optionsspanspan-idusing_client_optionsspanusing-client-options"></a><span id="using_client_options"></span><span id="USING_CLIENT_OPTIONS"></span>使用客户端选项

以下命令与在上一示例中启动的 NTSD 调试器连接到远程会话。

该命令使用 **/c** 参数来指示客户端命令。 它指定服务器计算机的名称 **server06.constoso.com** 和远程会话的名称 **debugit**。

该命令还包括 **/k** 参数以指定关键字颜色文件的位置。

```console
remote /c server06 debugit /k c:\remote_client.txt
```

颜色文件包含以下文本：

```console
Registry
white, blue
Token
red, white
```

此文本指示远程工具显示带有 "registry" 一词的输出行， (蓝色背景中的白色文本区分大小写) ，并在白色背景上以红色文本显示带有 "token" 字样的输出行。

在响应中，远程工具会将客户端连接到服务器会话，并显示以下消息。

```console
**************************************
***********     REMOTE    ************
***********     CLIENT    ************
**************************************
Connected...

Microsoft Windows XP [Version 5.1.2600]
(C) Copyright 1985-2001 Microsoft Corp.
```

客户端现在可以将命令发送到服务器计算机上的 NTSD 调试器。 命令的输出显示在客户端和服务器计算机上。

带有单词 "registry" 的输出行在客户端计算机上以白色文本显示在蓝色背景上，在白色背景上以红色文本显示带有 "内核" 字样的输出行。

### <a name="span-idquerying_a_sessionspanspan-idquerying_a_sessionspanquerying-a-session"></a><span id="querying_a_session"></span><span id="QUERYING_A_SESSION"></span>查询会话

远程工具包括一个查询参数 (**/q**) ，用于显示特定计算机上的远程会话的列表。 此显示内容仅包括显示的会话， (在没有 **/-v** 参数的情况下启动调试器会话，并且通过 **/v** 参数) 启动非调试器会话。

您可以查询来自服务器或客户端计算机的会话。 即使在本地计算机上查询会话，也必须指定计算机名称。

以下命令查询本地计算机上的会话 **Server04**。

```console
remote /q Server04
```

在响应中，远程工具会报告在本地计算机上没有运行任何远程会话。

```console
Querying server \\Server04
No Remote servers running on \\Server04
```

与此相反，若要响应有关另一台计算机上的会话（ **server06.constoso.com**）的查询，远程工具会列出该计算机上运行的会话。

```console
Querying server \\Server06

Visible sessions on server Server06:

ntsd                            [Remote /C SERVER06 "debug"] visible
cmd                             [Remote /C SERVER06 "test"] visible
```

此显示将列出可见会话、在这些会话上运行的控制台程序 (NTSD 和命令提示符窗口) ，以及连接到该会话的命令。 会话名称将在命令语法中用引号引起来。

此显示不会显示为这些会话（如果有）建立的权限。 因此，显示可能包括您没有加入的会话。

### <a name="span-idusing_the_session_commandsspanspan-idusing_the_session_commandsspanusing-the-session-commands"></a><span id="using_the_session_commands"></span><span id="USING_THE_SESSION_COMMANDS"></span>使用会话命令

在远程会话期间，你可以随时使用远程会话命令。

以下命令将消息发送到连接到该会话的所有计算机。

```console
@M I think I found the problem.
```

因此，该消息将出现在会话中所有计算机的命令提示符窗口中。 消息包括计算机名称和消息的日期和时间。

```console
@m I think I found the problem.     [SERVER01       Wed 11:53 AM]
```

从服务器计算机发送消息时，"本地" 将出现在标签中，而不是计算机名称中。

```console
@m I think I found the problem.     [Local       Wed 11:52 AM]
```

以下命令将生成一个弹出消息，该消息显示在服务器计算机上。 在会话中的所有客户端计算机上，它会在命令提示符窗口中写入一条消息。

```console
@P Did you see that?
```

在客户端计算机上，弹出消息显示在命令窗口中。

```console
From SERVER02  [Wed 11:58 AM]

 Did you see that?
```

消息标签中显示的时间始终为服务器计算机上的时间，即使发送该消息的客户端计算机在不同的时区中也是如此。

### <a name="span-idending_a_remote_sessionspanspan-idending_a_remote_sessionspanending-a-remote-session"></a><span id="ending_a_remote_session"></span><span id="ENDING_A_REMOTE_SESSION"></span>结束远程会话

下面的示例演示如何使用远程会话命令断开客户端计算机与会话的连接并结束远程会话。 只有启动了远程会话的服务器计算机才能结束。

要断开客户端计算机与远程会话的连接，请在客户端计算机上键入 <strong>@q</strong> 。

作为响应，将在断开连接的客户端计算机上显示以下消息。

```console
**_ SESSION OVER _*_
```

在会话中的所有其他计算机上，远程工具会使用计算机的名称和断开连接的用户以及断开连接的日期和时间来发送消息。

```console
_*Remote:  Disconnected from SERVER04 User01  [Wed 12:01 PM]
```

若要结束远程会话，请在服务器计算机上键入 <strong>@k</strong> 。 此命令会自动断开客户端连接，然后结束会话。

 

 





