---
title: 启动 Remote.exe 会话
description: 启动 Remote.exe 会话
keywords:
- 通过 remote.exe 远程调试，启动会话
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3a9a044640e6d81d23e8823e78321921310ea096
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96828829"
---
# <a name="starting-a-remoteexe-session"></a>启动 Remote.exe 会话


## <span id="ddk_starting_a_remote_exe_session_dbg"></span><span id="DDK_STARTING_A_REMOTE_EXE_SESSION_DBG"></span>


可以通过两种方式启动使用 KD 或 CDB 的 remote.exe 会话。 只有这两个方法与 NTSD 一起使用。

### <a name="span-idcustomizing_your_command_prompt_windowspanspan-idcustomizing_your_command_prompt_windowspancustomizing-your-command-prompt-window"></a><span id="customizing_your_command_prompt_window"></span><span id="CUSTOMIZING_YOUR_COMMAND_PROMPT_WINDOW"></span>自定义命令提示符窗口

Remote.exe 客户端和 Remote.exe 服务器在命令提示符窗口中运行。

若要准备远程会话，你应该自定义此窗口以提高其可用性。 打开命令提示符窗口。 右键单击标题栏，然后选择 " **属性**"。 选择 "**布局**" 选项卡。中转到标题为 "屏幕缓冲区大小" 的部分，在 "**宽度**" 框中键入 **90** ，在 "**高度**" 框中键入 **4000** 和 **9999** 之间的值。 这会在内核调试器上的远程会话中启用滚动条。

如果要改变命令提示符的形状，请更改 "Windows 大小" 部分的高度和宽度值。 选择 " **选项** " 选项卡。启用 **编辑选项** "快速编辑" 模式和插入模式。 这允许您在命令提示符会话中剪切和粘贴信息。 单击“确定”应用更改。 选择相应的选项，以便在出现提示时将更改应用于所有将来的会话。

### <a name="span-idstarting_the_remote_exe_server__first_methodspanspan-idstarting_the_remote_exe_server__first_methodspanstarting-the-remoteexe-server-first-method"></a><span id="starting_the_remote_exe_server__first_method"></span><span id="STARTING_THE_REMOTE_EXE_SERVER__FIRST_METHOD"></span>启动 Remote.exe 服务器：第一种方法

启动 Remote.exe 服务器的常规语法如下所示：

```console
remote /s "Command_Line" Unique_Id [/f Foreground_Color] [/b Background_Color] 
```

这可用于在远程计算机上启动 KD 或 CDB，如以下示例中所示：

```console
remote /s "KD [options]" MyBrokenBox 

remote /s "CDB [options]" MyBrokenApp 
```

这会在命令提示符窗口中启动 Remote.exe 服务器，并启动调试器。

你不能使用此方法直接启动 NTSD，因为 NTSD 进程在与调用它的窗口不同的窗口中运行。

### <a name="span-idstarting_the_remote_exe_server__second_methodspanspan-idstarting_the_remote_exe_server__second_methodspanstarting-the-remoteexe-server-second-method"></a><span id="starting_the_remote_exe_server__second_method"></span><span id="STARTING_THE_REMOTE_EXE_SERVER__SECOND_METHOD"></span>启动 Remote.exe 服务器：第二种方法

还有一种可以启动 Remote.exe 服务器的替代方法。 此方法涉及首次启动调试器，然后使用 [**remote (Create Remote.exe server)**](-remote--create-remote-exe-server-.md) 命令来启动服务器。

由于 **remote** 命令是在启动调试器后发出的，因此此方法同样适用于 KD、CDB 和 NTSD。

示例如下。 首先，以正常方式启动调试器：

```console
KD [options] 
```

调试器运行后，请使用 **remote** 命令：

```dbgcmd
.remote MyBrokenBox 
```

这将导致 KD 进程，该进程也是 ID 为 "MyBrokenBox" 的 Remote.exe 服务器，与第一种方法完全相同。

此方法的一个优点是，如果要使用远程调试，就不必提前决定。 如果正在使用控制台调试器之一进行调试，并决定希望远程位置中的某个用户接管，则可以使用 **远程** 命令，然后即可连接到会话。

### <a name="span-idstarting_the_remote_exe_clientspanspan-idstarting_the_remote_exe_clientspanstarting-the-remoteexe-client"></a><span id="starting_the_remote_exe_client"></span><span id="STARTING_THE_REMOTE_EXE_CLIENT"></span>启动 Remote.exe 客户端

启动 Remote.exe 客户端的常规语法如下所示：

```console
remote /c ServerNetBIOSName Unique_ID [/l Lines_to_Get] [/f Foreground_Color] [/b Background_Color] 
```dbgcmd

For example, if the "MyBrokenBox" session, described above, was started on a local host computer whose network name was "Server2", you can connect to it with the command:

```console
remote /c server2 MyBrokenBox 
```

具有相应权限的网络上的任何人都可以连接到此调试会话，前提是他们知道你的计算机名和会话 ID。

### <a name="span-idissuing_commandsspanspan-idissuing_commandsspanissuing-commands"></a><span id="issuing_commands"></span><span id="ISSUING_COMMANDS"></span>发出命令

命令通过 Remote.exe 客户端发出并发送到 Remote.exe 服务器。 您可以在客户端中输入任何命令，就像您直接将它输入到调试器中一样。

若要退出 Remote.exe 客户端上的 remote.exe 会话，请输入 <strong>@Q</strong> 命令。 这会使 Remote.exe 服务器和调试程序运行。

若要结束服务器会话，请 <strong>@K</strong> 在 Remote.exe 服务器上输入命令。

 

 





