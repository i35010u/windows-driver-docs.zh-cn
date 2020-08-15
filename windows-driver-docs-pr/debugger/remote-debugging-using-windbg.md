---
title: 使用 WinDbg 进行远程调试
description: 远程调试涉及两个在两个不同位置运行的调试器。
ms.assetid: 3030CEE4-DF10-4F84-A32D-38613D7EE072
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0d198aa1ba343484ed853e66b01932edcc958cab
ms.sourcegitcommit: f610410e1500f0b0a4ca008b52679688ab51033d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/15/2020
ms.locfileid: "88253053"
---
# <a name="remote-debugging-using-windbg"></a>使用 WinDbg 进行远程调试


远程调试涉及两个在两个不同位置运行的调试器。 执行调试的调试器称为 *调试服务器*。 第二个调试器（称为 *调试客户端*）从远程位置控制调试会话。 若要建立远程会话，必须首先设置调试服务器，然后激活调试客户端。

正在调试的代码可以在运行调试服务器的同一台计算机上运行，也可以在单独的计算机上运行。 如果调试服务器正在执行用户模式调试，则正在调试的进程可以与调试服务器在同一台计算机上运行。 如果调试服务器正在执行内核模式调试，则所调试的代码通常会在单独的目标计算机上运行。

下图说明了一个远程会话，在该会话中运行的调试服务器在主计算机上执行的是对在单独的目标计算机上运行的代码进行内核模式调试。

![显示远程计算机、主机计算机和目标计算机的关系图](images/clientservertarget.png)

远程调试连接可以使用几种传输协议： TCP、NPIPE、SPIPE、SSL 和 COM 端口。 假设您已选择使用 TCP 作为协议，并且您已选择使用 WinDbg 作为调试客户端和调试服务器。 你可以使用以下过程建立远程内核模式调试会话：

1. 在主计算机上，打开 WinDbg 并建立与目标计算机的内核模式调试会话。  (参阅 [使用 WinDbg 进行实时内核模式调试](performing-kernel-mode-debugging-using-windbg.md)。 ) 
2. 通过选择 "**调试**" 菜单中的 "**中断**" 或按 CTRL + break 来中断。
3. 在 [调试器命令窗口](debugger-command-window.md)中，输入以下命令。

   **。 server tcp： port = 5005**

   **注意**  端口号5005是任意的。 端口号是你的选择。

     

4. WinDbg 将响应与下面类似的输出。

   ```dbgcmd
   Server started.  Client can connect with any of these command lines
   0: <debugger> -remote tcp:Port=5005,Server=YourHostComputer
   ```

5. 在远程计算机上，打开 WinDbg，然后从 "**文件**" 菜单中选择 "**连接到远程会话**"。
6. 在 " **连接字符串**" 下，输入以下字符串。

   **tcp： Port = 5005，Server =**<em>YourHostComputer</em>

   其中， *YourHostComputer* 是运行调试服务器的主计算机的名称。

   选择“确定”。

## <a name="span-idusing_the_command_linespanspan-idusing_the_command_linespanspan-idusing_the_command_linespanusing-the-command-line"></a><span id="Using_the_Command_Line"></span><span id="using_the_command_line"></span><span id="USING_THE_COMMAND_LINE"></span>使用命令行


作为上述部分中给定过程的替代方法，可以在命令行中设置远程调试会话。 假设你已设置为在主计算机和目标计算机之间通过通道32上的1394电缆建立内核模式调试会话。 你可以使用以下过程建立远程调试会话：

1. 在主计算机上的命令提示符窗口中输入以下命令。

   **windbg-server tcp： port = 5005-k 1394：通道 = 32**

2. 在远程计算机上的命令提示符窗口中输入以下命令。

   **windbg-远程 tcp： Port = 5005，Server =**<em>YourHostComputer</em>

   其中， *YourHostComputer* 是运行调试服务器的主计算机的名称。

## <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息


除了本主题中所示的其他方法，还可以通过多种方式建立远程调试。 有关在 WinDbg [调试器命令窗口](debugger-command-window.md)中设置调试服务器的完整信息，请参阅 [**。服务器 (创建调试服务器) **](-server--create-debugging-server-.md)。 有关启动 WinDbg (并在命令行中建立远程调试) 的完整信息，请参阅 [**WinDbg 命令行选项**](windbg-command-line-options.md)。

 

 





