---
title: 使用 KD 调试用户模式故障
description: 使用 KD 调试用户模式故障
ms.assetid: c7ef3c04-45bf-4e7b-bcc6-35fe2ffa43d1
keywords:
- KD，用户模式下使用 KD 进行调试
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 541c91a37fc69e98be83c93c20fb7c424e400f59
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324588"
---
# <a name="debugging-a-user-mode-failure-with-kd"></a>使用 KD 调试用户模式故障


## <span id="ddk_debugging_user_mode_failures_with_kd_dbg"></span><span id="DDK_DEBUGGING_USER_MODE_FAILURES_WITH_KD_DBG"></span>


若要正确地调试用户模式故障，您需要 CDB 或 WinDbg。 但是，有时用户模式异常将中断到 KD 因为没有任何用户模式下调试程序存在。 此外，还有有时是很有帮助监视特定的用户模式进程正在执行哪些操作内核模式问题进行调试时。

默认情况下，内核调试程序尝试加载与指定的地址相匹配的第一个用户模式符号 (对于**k**， **u**，或**ln**命令)。

遗憾的是，用户模式下的符号通常未指定符号路径中或第一个符号不正确。 如果符号不存在，或者将它们复制到符号路径或使用[ **.sympath （设置符号路径）** ](-sympath--set-symbol-path-.md)命令来指向完整符号树中，然后使用[ **.reload（重新加载模块）** ](-reload--reload-module-.md)命令。 如果加载错误的符号，则可以通过执行显式加载符号 **.reload &lt;binary.ext&gt;**。

因此，它们的加载在不同的地址，但有例外情况，大部分 Windows Dll 是重新设定基址。 视频适配器是最常见的异常。 有许多相同的基址是 KD 将几乎始终在所有负载都找到的 ati.dll （按字母顺序的第一个视频符号） 的视频适配器。 有关视频，还有一个.sys 文件加载，可以通过使用标识[ **！ 驱动程序**](-drivers.md)扩展。 借助该信息，可以发出 **.reload**若要获取正确的视频 Dll。 也有的时间，调试器获取困惑并重新加载特定符号将有助于为提供正确的堆栈。 反汇编符号查看正确的函数。

类似于视频的 Dll，几乎所有可执行文件加载在相同的地址，因此 KD 会报告访问权限。 如果看到访问中的堆栈跟踪，请执行[ **！ 过程**](-process.md) ，然后 **.reload**的给定的可执行文件名称。 如果可执行文件的符号路径中没有的符号，可以将它们复制并执行 **.reload**试。

有时 KD 或 WinDbg 具有完整符号树是中的符号路径时甚至加载正确的用户模式下符号的问题。 在这种情况下，ntdll.dll 和 kernel32.dll 是两个需要的最常见符号。 对于调试从 KD CSRSS，winsrv.dll 和 csrsrv.dll 也是常见的 Dll 加载。

 

 





