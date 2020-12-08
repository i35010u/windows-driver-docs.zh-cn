---
title: 使用 KD 进行远程调试
description: 了解如何使用 KD 进行远程调试。 远程调试涉及两个在两个不同位置运行的调试器。
ms.date: 05/03/2018
ms.localizationpriority: medium
ms.openlocfilehash: a75ffbfac3a7d25b84ffe1b136e625b2c96b96c1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96786953"
---
# <a name="remote-debugging-using-kd"></a>使用 KD 进行远程调试


远程调试涉及两个在两个不同位置运行的调试器。 执行调试的调试器称为 *调试服务器*。 第二个调试器（称为 *调试客户端*）从远程位置控制调试会话。 若要建立远程会话，必须首先设置调试服务器，然后激活调试客户端。

如果您想要让其他人在计算机上进行调试，则可以使用远程调试。

正在调试的代码可以在运行调试服务器的同一台计算机上运行，也可以在单独的计算机上运行。 如果调试服务器正在执行用户模式调试，则正在调试的进程可以与调试服务器在同一台计算机上运行。 如果调试服务器正在执行内核模式调试，则所调试的代码通常会在单独的目标计算机上运行。

下图说明了一个远程会话，在该会话中运行的调试服务器在主计算机上执行的是对在单独的目标计算机上运行的代码进行内核模式调试。

![显示远程计算机、主机计算机和目标计算机的关系图](images/clientservertarget.png)

远程调试连接可以使用几种传输协议： TCP、NPIPE、SPIPE、SSL 和 COM 端口。 假设您已选择使用 TCP 作为协议，并且您已选择将 KD 用作调试客户端和调试服务器。 你可以使用以下过程建立远程内核模式调试会话：

1. 在主计算机上，打开 KD 并建立与目标计算机的内核模式调试会话。  (参阅 [使用 KD 执行 Kernel-Mode 调试](performing-kernel-mode-debugging-using-kd.md)。 ) 
2. 按 CRTL 中断。
3. 输入以下命令。

   **。 server tcp： port = 5005**

   **注意**  端口号5005是任意的。 端口号是你的选择。

     

4. KD 将响应与下面类似的输出。

   ```dbgcmd
   Server started.  Client can connect with any of these command lines
   0: <debugger> -remote tcp:Port=5005,Server=YourHostComputer
   ```

5. 在远程计算机上，打开命令提示符窗口，然后输入以下命令。

   **kd-remote tcp： Port = 5005，Server =**<em>YourHostComputer</em>

   其中， *YourHostComputer* 是运行调试服务器的主计算机的名称。

## <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息


有关启动 KD (并在命令行中建立远程调试) 的完整信息，请参阅 [**KD Command-Line 选项**](kd-command-line-options.md)。

 

 





