---
title: 远程工具示例
description: 远程工具示例
ms.assetid: 624f1a78-04da-45c2-8f8d-a593d557be7d
keywords:
- 远程工具示例
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: becf699b2abf896261d58426343abccbf7d28a1d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63353620"
---
# <a name="remote-tool-examples"></a>远程工具示例


## <span id="ddk_remote_tool_examples_dtools"></span><span id="DDK_REMOTE_TOOL_EXAMPLES_DTOOLS"></span>


在本部分中的示例演示了如何使用远程工具，并显示示例输入和输出。

### <a name="span-idbasicservercommandspanspan-idbasicservercommandspanbasic-server-command"></a><span id="basic_server_command"></span><span id="BASIC_SERVER_COMMAND"></span>基本服务器命令

以下命令在计算机上启动远程会话。

该命令使用 **/s**参数以指示服务器端的命令。 它使用该命令中， **cmd**，以启动 Windows 命令 shell (Cmd.exe)，并将其命名会话**test1**。

```console
remote /s cmd test1
```

在响应中，远程工具启动会话，并显示客户端将用于连接到该会话的命令。

```console
**************************************
***********     REMOTE    ************
***********     SERVER    ************
**************************************
To Connect: Remote /C SERVER06 "test1"

Microsoft Windows XP [Version 5.1.2600]
(C) Copyright 1985-2001 Microsoft Corp.
```

### <a name="span-idbasicclientcommandspanspan-idbasicclientcommandspanbasic-client-command"></a><span id="basic_client_command"></span><span id="BASIC_CLIENT_COMMAND"></span>基本的客户端命令

以下命令连接到 Server01 计算机上的远程会话。 该命令使用 **/c**参数以指示客户端的命令。 指定要将服务器计算机名称**Server01**，并在该计算机上的会话的名称**test1**。

```console
remote /c server01 test1
```

在响应中，远程工具会显示一条消息，报告客户端计算机连接到服务器计算机上的会话。 所显示的消息的服务器计算机和本地用户的名称 (**Server04 user1**)。

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

客户端连接到服务器后，客户端和服务器计算机上的命令提示符处键入的命令显示这两个显示器上...

例如，如果键入**dir**在客户端计算机的命令提示符下，目录显示在客户端和服务器计算机上的命令提示符窗口中显示。

### <a name="span-idusingserveroptionsspanspan-idusingserveroptionsspanusing-server-options"></a><span id="using_server_options"></span><span id="USING_SERVER_OPTIONS"></span>使用 Server 选项

下面的服务器端的命令使用的是 NTSD 调试器启动远程会话。

该命令使用 **/s**参数以指示服务器端的命令。 下一个参数 **"ntsd-d-v"**，是控制台命令，启动调试器，以及调试器选项。 因为控制台命令中包含空格，括在引号中。 该命令包含会话的名称**debugit**。

该命令使用 **/u**参数，以允许仅在计算机和特定用户，User03 Domain01，若要连接到该会话中的管理员。 它使用 **/f**并**b </b**选项，以指定在白色背景黑色文本 （前景）。

最后，该命令使用 **/v**参数，以使会话看不到用户查询。 调试器会话是默认情况下可见。

```console
remote /s "ntsd -d -v" DebugIt /u Administrators /u Domain01\User03 
/f black /b white /-v
```

在响应中，远程工具创建名为 DebugIt 的会话，并使用指定的参数启动 NTSD。 该消息指示指定的用户有权连接。 它还会指定的颜色更改命令窗口。

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

### <a name="span-idusingclientoptionsspanspan-idusingclientoptionsspanusing-client-options"></a><span id="using_client_options"></span><span id="USING_CLIENT_OPTIONS"></span>使用客户端选项

以下命令连接到远程会话使用的是 NTSD 调试器启动在前面的示例。

该命令使用 **/c**参数以指示客户端的命令。 指定要将服务器计算机名称**server06**，和远程会话中，名称**debugit**。

该命令还包括 **/k**参数来指定关键字颜色文件的位置。

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

此文本以红色文本白色背景上指示远程工具来显示蓝色背景白色文本中的单词"注册表"（不区分大小写） 开头的输出的行并显示单词"标记"使用输出的行。

在响应中，远程工具客户端连接到服务器会话，并显示以下消息。

```console
**************************************
***********     REMOTE    ************
***********     CLIENT    ************
**************************************
Connected...

Microsoft Windows XP [Version 5.1.2600]
(C) Copyright 1985-2001 Microsoft Corp.
```

客户端现在可以将命令发送到服务器计算机上的 NTSD 调试器。 该命令的输出将显示在客户端和服务器计算机上。

使用 word"注册表"的输出行显示白色文本蓝色背景和白色背景上的红色文本中的"内核"一词的输出行中的客户端计算机上。

### <a name="span-idqueryingasessionspanspan-idqueryingasessionspanquerying-a-session"></a><span id="querying_a_session"></span><span id="QUERYING_A_SESSION"></span>查询会话

远程工具包括查询参数 (**/q**)，显示特定计算机上的远程会话的列表。 显示内容包括仅显示会话 (在不启动调试器会话 **/v**参数和非调试器会话入门 **/v**参数)。

您可以查询从服务器或客户端计算机的会话。 即使在查询的本地计算机上的会话时，必须指定计算机名称。

下面的查询命令的本地计算机上的会话**Server04**。

```console
remote /q Server04
```

在响应中，远程工具将报告没有在本地计算机上运行远程会话。

```console
Querying server \\Server04
No Remote servers running on \\Server04
```

与此相反，在另一台计算机上的会话的有关查询响应**Server06**，远程工具将列出该计算机上运行的会话。

```console
Querying server \\Server06

Visible sessions on server Server06:

ntsd                            [Remote /C SERVER06 "debug"] visible
cmd                             [Remote /C SERVER06 "test"] visible
```

仅显示可见的会话 （NTSD 和命令提示符窗口），这些会话和连接到该会话的命令上运行的控制台程序。 会话名称出现在引号中的命令语法。

如果有，显示不显示建立这些会话的权限。 因此，显示可能包括你无权加入的会话。

### <a name="span-idusingthesessioncommandsspanspan-idusingthesessioncommandsspanusing-the-session-commands"></a><span id="using_the_session_commands"></span><span id="USING_THE_SESSION_COMMANDS"></span>使用会话命令

可以在远程会话期间随时使用的远程会话命令。

以下命令将消息发送到连接到会话的所有计算机。

```console
@M I think I found the problem.
```

因此，消息会显示在所有计算机的命令提示符窗口中在会话中。 该消息包含计算机名称和的日期和时间的消息。

```console
@m I think I found the problem.     [SERVER01       Wed 11:53 AM]
```

从服务器计算机发送消息，"本地"中会出现标签而不是计算机名称。

```console
@m I think I found the problem.     [Local       Wed 11:52 AM]
```

下面的命令生成的服务器计算机显示一个弹出消息。 在会话中的所有客户端计算机，它将消息写入到命令提示符窗口。

```console
@P Did you see that?
```

客户端计算机上弹出消息出现在命令窗口中。

```console
From SERVER02  [Wed 11:58 AM]

 Did you see that?
```

消息标签中显示的时间始终是服务器计算机上的时间，即使发送消息的客户端计算机位于不同的时区。

### <a name="span-idendingaremotesessionspanspan-idendingaremotesessionspanending-a-remote-session"></a><span id="ending_a_remote_session"></span><span id="ENDING_A_REMOTE_SESSION"></span>结束远程会话

以下示例演示如何使用远程会话命令来从会话断开连接的客户端计算机，并以结束远程会话。 启动远程会话的服务器计算机可以结束它。

若要断开客户端计算机连接从远程会话中，在客户端计算机上，键入<strong>@q</strong>。

在响应中，在断开连接的客户端计算机上显示以下消息。

```console
*** SESSION OVER ***
```

所有其他计算机上的会话中，远程工具发布包含的计算机和用户都断开连接，名称的消息的一天和断开连接的时间。

```console
**Remote:  Disconnected from SERVER04 User01  [Wed 12:01 PM]
```

若要结束远程会话，请在服务器计算机上，键入<strong>@k</strong>。 此命令自动断开连接的客户端，然后结束会话。

 

 





