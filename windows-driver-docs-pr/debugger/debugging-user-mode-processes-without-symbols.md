---
title: 不使用符号调试用户模式进程
description: 不使用符号调试用户模式进程
keywords:
- 符号，无符号调试
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: b7692da6a35dc7fbc1e6b3be7fcc647789bb5383
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96819843"
---
# <a name="debugging-user-mode-processes-without-symbols"></a>不使用符号调试用户模式进程


## <span id="ddk_debugging_user_mode_processes_without_symbols_dbg"></span><span id="DDK_DEBUGGING_USER_MODE_PROCESSES_WITHOUT_SYMBOLS_DBG"></span>


在启动调试器以执行用户模式故障之前，必须在出错的计算机上具有符号。 但是，有时启动调试器时没有符号。 如果此问题很容易重现，只需复制符号并重新运行。 然而，如果该问题可能不会再次出现，则某些信息仍可能会搜集故障：

1.  若要确定地址的含义，需要一个与错误匹配的计算机。 它应该具有相同的平台 (x86 或 x64) 并使用相同版本的 Windows 进行加载。

2.  配置计算机后，将用户模式的符号和要调试的二进制文件复制到新计算机上。

3.  在无符号计算机上启动 CDB 或 WinDbg。

4.  如果在无符号计算机上不知道哪个应用程序失败，请) 命令发出 [**| (进程状态**](---process-status-.md) 。 如果这不提供名称，请在无符号计算机上中断 KD 并执行 [**！ process 0 0**](-process.md)，查找 CDB 命令给定的进程 ID。

5.  如果设置了两个调试程序-一个具有未命中错误的符号，另一个已命中错误但没有符号，则发出 k (在无符号计算机上 [**) 命令发出 k 显示堆栈 Backtrace**](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md) 。

6.  在带有符号的计算机上，发出 [**u (Unassemble)**](u--unassemble-.md) 命令，适用于在无符号堆栈上给出的每个地址。 这会在无符号计算机上提供错误的堆栈跟踪。

7.  通过查看堆栈跟踪，可以查看调用中涉及的模块和函数名称。

 

 





