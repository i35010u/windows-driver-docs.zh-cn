---
title: 使用 KD 进行远程调试
description: 远程调试涉及两个调试器运行在两个不同的位置。
ms.assetid: 274CAB1D-DD3B-4ACD-919C-8B8C253BCE50
ms.date: 05/03/2018
ms.localizationpriority: medium
ms.openlocfilehash: cb9663cd1b172140bb461d55cc2e1748645facb4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63353545"
---
# <a name="remote-debugging-using-kd"></a>使用 KD 进行远程调试


远程调试涉及两个调试器运行在两个不同的位置。 调用调试器执行的调试*调试服务器*。 第二个调试器中，称为*调试客户端*，控制从远程位置的调试会话。 若要建立的远程会话，必须首先设置调试服务器并随后激活调试客户端。

当你想要涉及中查看的问题，一台 PC 进行调试的其他人时，远程调试很有用。

正在调试的代码可能正在运行的调试服务器在同一计算机上运行，或它可能在单独的计算机上运行。 如果调试服务器执行用户模式下调试，则正在调试的进程可以在调试服务器所在的计算机上运行。 如果在调试服务器执行的内核模式调试，然后在单独的目标计算机上通常运行正在调试的代码。

下图说明了当内核模式调试的单独的目标计算机运行的代码执行的主机计算机上，运行的调试服务器的远程会话。

![图示显示远程、 主机和目标计算机](images/clientservertarget.png)

有多个可用于远程调试连接的传输协议：TCP、 NPIPE、 SPIPE、 SSL 和 COM 端口。 假设你已选择使用 TCP 作为协议，并且已选择要用作 KD 调试客户端和调试服务器。 可以使用以下过程来建立远程内核模式调试会话：

1. 主计算机上打开 KD 并建立与目标计算机的内核模式调试会话。 (请参阅[执行内核模式调试使用 KD](performing-kernel-mode-debugging-using-kd.md)。)
2. 在中中断通过按 CRTL 中断。
3. 输入以下命令。

   **.server tcp:port=5005**

   **请注意**5005 的端口号是任意的。 你选择的端口号。

     

4. KD 将使用与以下类似的输出响应。

   ```dbgcmd
   Server started.  Client can connect with any of these command lines
   0: <debugger> -remote tcp:Port=5005,Server=YourHostComputer
   ```

5. 在远程计算机上打开命令提示符窗口，并输入以下命令。

   **kd -remote tcp:Port=5005,Server=**<em>YourHostComputer</em>

   其中*YourHostComputer*是您正在运行调试服务器的主机计算机的名称。

## <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息


有关启动 KD （建立远程调试） 在命令行的完整信息，请参阅[ **KD 命令行选项**](kd-command-line-options.md)。

 

 





