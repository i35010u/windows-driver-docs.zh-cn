---
title: 不使用符号调试用户模式进程
description: 不使用符号调试用户模式进程
ms.assetid: ac742239-ed6b-4813-80d6-7b8eb84a0cb4
keywords:
- 不含符号进行调试的符号
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: ed71b1003b1a5f0667b8ae89bdf02ef0a18c40de
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346365"
---
# <a name="debugging-user-mode-processes-without-symbols"></a>不使用符号调试用户模式进程


## <span id="ddk_debugging_user_mode_processes_without_symbols_dbg"></span><span id="DDK_DEBUGGING_USER_MODE_PROCESSES_WITHOUT_SYMBOLS_DBG"></span>


请务必在开始调试程序，以便用户模式故障之前出错的计算机上具有符号。 但是，有时将启动调试器不包含符号。 如果比较容易再现该问题，您只需复制符号，然后重新运行。 如果，但是，问题可能不会再次发生，仍可以从此故障中收集一些信息：

1.  要找出地址的含义是什么，您需要错误相匹配的计算机。 它应具有相同的平台 （x86 或 x64），并使用相同版本的 Windows 加载。

2.  在必须配置的计算机，请将复制用户模式符号和你想要调试到新计算机上的二进制文件。

3.  无符号的计算机上启动 CDB 或 WinDbg。

4.  如果您不知道哪个应用程序无符号的计算机上的失败，则发出[ **|（进程状态）** ](---process-status-.md)命令。 如果，不会向你提供一个名称，分解成 KD 无符号的计算机上，执行[ **！ process 0 0**](-process.md)，他们寻求 CDB 命令提供的进程 ID。

5.  当你具有两个调试程序设置-一个使用尚未达到该错误的符号-，已达到该错误，但不包含符号的一个问题[ **k （显示堆栈回溯）** ](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)无符号的命令计算机。

6.  在计算机上使用符号，发出[ **u （反汇编）** ](u--unassemble-.md)命令用于授予无符号的堆栈上的每个地址。 这会为您的堆栈跟踪的无符号的计算机上的错误。

7.  通过查看堆栈跟踪您所见的调用中所涉及的模块和函数名称。

 

 





