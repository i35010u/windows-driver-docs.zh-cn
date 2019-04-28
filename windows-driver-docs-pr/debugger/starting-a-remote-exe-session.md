---
title: 启动 Remote.exe 会话
description: 启动 Remote.exe 会话
ms.assetid: 2b70e54e-ab02-46f1-9af1-e7379c89cf3c
keywords:
- 通过 remote.exe，启动会话的远程调试
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: c2dfd1da6a4f1aa9c24a97dacc3d0c3ac0089dc0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335536"
---
# <a name="starting-a-remoteexe-session"></a>启动 Remote.exe 会话


## <span id="ddk_starting_a_remote_exe_session_dbg"></span><span id="DDK_STARTING_A_REMOTE_EXE_SESSION_DBG"></span>


有两种方法来启动与 KD 或 CDB remote.exe 会话。 仅第二种方法适用于 NTSD。

### <a name="span-idcustomizingyourcommandpromptwindowspanspan-idcustomizingyourcommandpromptwindowspancustomizing-your-command-prompt-window"></a><span id="customizing_your_command_prompt_window"></span><span id="CUSTOMIZING_YOUR_COMMAND_PROMPT_WINDOW"></span>自定义命令提示符窗口

Remote.exe 客户端和 Remote.exe 服务器在命令提示符窗口中运行。

若要准备远程会话，您应自定义此窗口以提高其可用性。 打开“命令提示符”窗口。 右键单击标题栏并选择**属性**。 选择**布局**选项卡。转到标题为"屏幕缓冲区大小"和类型的部分**90**中**宽度**框和之间的值**4000**并**9999**中**高度**框。 这样在内核调试程序的远程会话中，滚动条。

如果你想要更改形状的命令提示符，请更改高度和宽度的"Windows 大小"部分的值。 选择**选项**选项卡。启用**编辑选项**quickedit 模式和插入模式。 这允许您剪切并粘贴在命令提示符会话中的信息。 单击“确定”以应用更改。 选择选项以将更改应用于所有将来的会话出现提示时。

### <a name="span-idstartingtheremoteexeserverfirstmethodspanspan-idstartingtheremoteexeserverfirstmethodspanstarting-the-remoteexe-server-first-method"></a><span id="starting_the_remote_exe_server__first_method"></span><span id="STARTING_THE_REMOTE_EXE_SERVER__FIRST_METHOD"></span>启动 Remote.exe 服务器：第一种方法

启动 Remote.exe 服务器的常规语法如下所示：

```console
remote /s "Command_Line" Unique_Id [/f Foreground_Color] [/b Background_Color] 
```

这可以用于 KD 或 CDB 启动的远程计算机上，如以下示例所示：

```console
remote /s "KD [options]" MyBrokenBox 

remote /s "CDB [options]" MyBrokenApp 
```

这将在命令提示符窗口中，启动 Remote.exe 服务器并启动调试器。

不能使用此方法直接启动 NTSD 因为 NTSD 进程在其中一个调用它时不同的窗口中运行。

### <a name="span-idstartingtheremoteexeserversecondmethodspanspan-idstartingtheremoteexeserversecondmethodspanstarting-the-remoteexe-server-second-method"></a><span id="starting_the_remote_exe_server__second_method"></span><span id="STARTING_THE_REMOTE_EXE_SERVER__SECOND_METHOD"></span>启动 Remote.exe 服务器：第二种方法

没有可以启动 Remote.exe 服务器的备用方法。 此方法涉及第一次启动调试器，，然后使用[ **.remote (创建 Remote.exe Server)** ](-remote--create-remote-exe-server-.md)命令以启动服务器。

由于 **.remote**发出命令，启动调试器后，此方法同样适用于 KD、 CDB 和 NTSD。

下面是一个示例。 首先，启动调试器以正常方式：

```console
KD [options] 
```

调试器开始运行后，使用 **.remote**命令：

```dbgcmd
.remote MyBrokenBox 
```

这会导致与第一种方法完全相同也是 Remote.exe 服务器 id 为"MyBrokenBox"KD 过程。

此方法的一个优点是，不需要提前决定，如果你想要使用远程调试。 如果你使用一个控制台调试器进行调试，然后决定你想要接管的远程位置中的某人，则可以使用 **.remote**命令，然后它们可以连接到你的会话。

### <a name="span-idstartingtheremoteexeclientspanspan-idstartingtheremoteexeclientspanstarting-the-remoteexe-client"></a><span id="starting_the_remote_exe_client"></span><span id="STARTING_THE_REMOTE_EXE_CLIENT"></span>在启动 Remote.exe 客户端

用于启动 Remote.exe 客户端的常规语法如下所示：

```console
remote /c ServerNetBIOSName Unique_ID [/l Lines_to_Get] [/f Foreground_Color] [/b Background_Color] 
```dbgcmd

For example, if the "MyBrokenBox" session, described above, was started on a local host computer whose network name was "Server2", you can connect to it with the command:

```console
remote /c server2 MyBrokenBox 
```

网络上具有相应权限的任何人都可以连接到此调试会话，，只要他们知道您的计算机名称和会话 id。

### <a name="span-idissuingcommandsspanspan-idissuingcommandsspanissuing-commands"></a><span id="issuing_commands"></span><span id="ISSUING_COMMANDS"></span>发出命令

命令通过 Remote.exe 客户端颁发并发送到 Remote.exe 服务器。 如果因为你正在直接到调试器中输入它，可以将任何命令输入客户端。

若要退出 remote.exe 会话 Remote.exe 客户端上，输入<strong>@Q</strong>命令。 这将使 Remote.exe 服务器和运行调试器。

若要结束服务器会话，请输入<strong>@K</strong> Remote.exe 服务器上的命令。

 

 





