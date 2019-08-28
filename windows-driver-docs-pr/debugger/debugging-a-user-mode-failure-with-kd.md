---
title: 使用 KD 调试用户模式故障
description: 使用 KD 调试用户模式故障
ms.assetid: c7ef3c04-45bf-4e7b-bcc6-35fe2ffa43d1
keywords:
- KD, KD 的用户模式调试
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 52738f6b3c2bd3fefcbeaee7a54d1830b9b0149a
ms.sourcegitcommit: 238308264c1ee2c74ec0c8c303258dc00c79b902
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2019
ms.locfileid: "70063914"
---
# <a name="debugging-a-user-mode-failure-with-kd"></a>使用 KD 调试用户模式故障


## <span id="ddk_debugging_user_mode_failures_with_kd_dbg"></span><span id="DDK_DEBUGGING_USER_MODE_FAILURES_WITH_KD_DBG"></span>


若要正确调试用户模式故障, 需要 CDB 或 WinDbg。 但有时, 用户模式异常将中断到 KD, 因为不存在用户模式调试器。 在调试内核模式问题时, 还可以监视特定的用户模式进程正在执行的操作。

默认情况下, 内核调试器尝试加载与指定地址匹配的第一个用户模式符号 (对于**k**、 **u**或**ln**命令)。

遗憾的是, 用户模式符号通常不在符号路径中指定, 或者第一个符号不是正确的。 如果符号不存在, 请将它们复制到符号路径中, 或使用[**sympath (设置符号路径)** ](-sympath--set-symbol-path-.md)命令指向完整的符号树, 然后使用[**reload.sql (重新加载模块)** ](-reload--reload-module-.md)命令。 如果加载了错误的符号, 则可以通过执行**重载&lt;&gt;** 来显式加载符号。

大多数 Windows Dll 都是变基的, 因此它们在不同的地址加载, 但有一些例外情况。 视频适配器是最常见的异常。 有数十个视频适配器, 它们都在相同的基址负载, 因此 KD 几乎始终会找到 ati (第一个视频符号, 按字母顺序排列)。 对于视频, 还加载了可使用[**lm**](lm--list-loaded-modules-.md)命令标识的 sys.databases 文件。 使用该信息, 可以发出**reload.sql** , 以获取正确的视频 dll。 此外, 当调试器变混乱并重新加载特定符号时, 将有助于提供正确的堆栈。 Unassemble 函数以查看符号是否正确。

与视频 Dll 类似, 几乎所有的可执行文件都在同一地址加载, 因此 KD 将报告访问权限。 如果在 access 中看到堆栈跟踪, 请执行[ **! 进程**](-process.md), 然后**重新加载**给定的可执行文件名称。 如果可执行文件在符号路径中没有符号, 请将其复制到其中, 然后重新**加载。**

有时, 即使在符号路径中有完整的符号树, KD 或 WinDbg 仍无法加载正确的用户模式符号。 在这种情况下, ntdll.dll 和 kernel32.dll 是所需的两个最常见的符号。 如果从 KD 调试 CSRSS, 则 winsrv 和 csrsrv 也是常用的 Dll 加载。

 

 





