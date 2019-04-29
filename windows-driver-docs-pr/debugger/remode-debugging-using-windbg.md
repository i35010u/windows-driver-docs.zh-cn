---
title: 使用 WinDbg 进行远程调试
description: 远程调试涉及两个调试器运行在两个不同的位置。
ms.assetid: 3030CEE4-DF10-4F84-A32D-38613D7EE072
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5c4ec56f7332a46adc31879859fcf0e0d1703438
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63353601"
---
# <a name="remote-debugging-using-windbg"></a>使用 WinDbg 进行远程调试


远程调试涉及两个调试器运行在两个不同的位置。 调用调试器执行的调试*调试服务器*。 第二个调试器中，称为*调试客户端*，控制从远程位置的调试会话。 若要建立的远程会话，必须首先设置调试服务器并随后激活调试客户端。

正在调试的代码可能正在运行的调试服务器在同一计算机上运行，或它可能在单独的计算机上运行。 如果调试服务器执行用户模式下调试，则正在调试的进程可以在调试服务器所在的计算机上运行。 如果在调试服务器执行的内核模式调试，然后在单独的目标计算机上通常运行正在调试的代码。

下图说明了当内核模式调试的单独的目标计算机运行的代码执行的主机计算机上，运行的调试服务器的远程会话。

![图示显示远程、 主机和目标计算机](images/clientservertarget.png)

有多个可用于远程调试连接的传输协议：TCP、 NPIPE、 SPIPE、 SSL 和 COM 端口。 假设你已选择使用 TCP 作为协议，并且已选择要用作 WinDbg 调试客户端和调试服务器。 可以使用以下过程来建立远程内核模式调试会话：

1. 主计算机上打开 WinDbg 和建立与目标计算机的内核模式调试会话。 (请参阅[实时内核模式调试使用 WinDbg](performing-kernel-mode-debugging-using-windbg.md)。)
2. 通过选择中断**中断**从**调试**菜单或通过按 ctrl + Break。
3. 在中[调试器命令窗口](debugger-command-window.md)，输入以下命令。

   **.server tcp:port=5005**

   **请注意**5005 的端口号是任意的。 你选择的端口号。

     

4. WinDbg 将使用与以下类似的输出响应。

   ```dbgcmd
   Server started.  Client can connect with any of these command lines
   0: <debugger> -remote tcp:Port=5005,Server=YourHostComputer
   ```

5. 在远程计算机上打开的 WinDbg 中，然后选择**连接到远程会话**从**文件**菜单。
6. 下**连接字符串**，输入下面的字符串。

   **tcp:Port=5005,Server=**<em>YourHostComputer</em>

   其中*YourHostComputer*是您正在运行调试服务器的主机计算机的名称。

   单击 **“确定”**。

## <a name="span-idusingthecommandlinespanspan-idusingthecommandlinespanspan-idusingthecommandlinespanusing-the-command-line"></a><span id="Using_the_Command_Line"></span><span id="using_the_command_line"></span><span id="USING_THE_COMMAND_LINE"></span>使用命令行


作为上一节中给出的过程的替代方法，您可以设置在命令行远程调试会话。 假设您的设置若要通过通道 32 上的 1394年电缆建立主计算机和目标计算机之间的内核模式调试会话。 可以使用以下过程来建立远程调试会话：

1. 主机计算机上，在命令提示符窗口中输入以下命令。

   **windbg -server tcp:port=5005 -k 1394:channel=32**

2. 在远程计算机上，在命令提示符窗口中输入以下命令。

   **windbg -remote tcp:Port=5005,Server=**<em>YourHostComputer</em>

   其中*YourHostComputer*是您正在运行调试服务器的主机计算机的名称。

## <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息


有许多方法来建立远程调试其他比本主题中所示。 有关设置在 WinDbg 中调试服务器的完整信息[调试器命令窗口](debugger-command-window.md)，请参阅[ **.server （创建调试服务器）**](-server--create-debugging-server-.md)。 有关启动 WinDbg （建立远程调试） 在命令行的完整信息，请参阅[ **WinDbg 命令行选项**](windbg-command-line-options.md)。

 

 





