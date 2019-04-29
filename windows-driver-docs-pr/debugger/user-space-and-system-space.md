---
title: 用户空间和系统空间
description: 用户空间和系统空间
ms.assetid: 2d988178-cd19-4dc4-8dc1-39b9b6a1aaad
keywords:
- 系统空间
- 系统空间地址
- 系统空间断点
- 内核空间
- 内核空间地址
- 内核空间断点
- 用户空间
- 用户空间地址
- 用户空间断点
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: afa8db8bef2370d36aa4d0038b6ec0d34c1f55ea
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63368097"
---
# <a name="user-space-and-system-space"></a>用户空间和系统空间


Windows 为每个用户模式应用程序提供虚拟地址的块。 这称为*用户空间*的该应用程序。 其他大块的地址，称为*系统空间*或*内核空间*，应用程序不能直接访问。

当 WinDbg 或 CDB 设置[断点](using-breakpoints.md)用户空间，在此断点设置在单个进程的用户空间中指定的地址。 在用户模式调试，当前进程确定虚拟地址的含义。 有关详细信息，请参阅[控制进程和线程](controlling-processes-and-threads.md)。

在内核模式下，您可以在用户空间中设置断点**bp**， **bu**，并**ba**命令或使用**断点**对话框。 必须先使用*进程上下文*以指定通过使用拥有该地址空间的用户模式进程 **.process /i** （或某些内核空间函数上的特定于进程的断点） 若要切换为正确的目标[进程上下文](changing-contexts.md#process-context)。

用户空间中的断点始终与相关联时设置断点，其过程上下文处于活动状态的过程。 如果用户模式下调试器为调试此进程，并且内核调试程序正在调试的计算机上运行进程，此断点中断用户模式下调试器，即使实际上从内核调试程序设置了断点。 可以在此情况下，分解成系统的内核调试程序，也可以使用[ **.breakin （中断添加到内核调试程序）** ](-breakin--break-to-the-kernel-debugger-.md)命令从用户模式下调试器将控制转移到内核调试程序。

### <a name="span-iddeterminingtherangeofuserspaceandsystemspacespanspan-iddeterminingtherangeofuserspaceandsystemspacespandetermining-the-range-of-user-space-and-system-space"></a><span id="determining_the_range_of_user_space_and_system_space"></span><span id="DETERMINING_THE_RANGE_OF_USER_SPACE_AND_SYSTEM_SPACE"></span>确定范围的用户空间和系统空间

如果您需要确定用户空间和目标计算机上的系统空间的范围，则可以使用[ **dp （显示内存）** ](d--da--db--dc--dd--dd--df--dp--dq--du--dw--dw--dyb--dyd--display-memor.md)内核调试程序以显示 Windows 全局变量命令**MmHighestUserAddress**。 此变量包含的用户空间顶部的地址。 由于系统空间地址始终高于用户空间地址，此值可以确定任何给定的地址是在用户空间还是在内核空间。

例如，在具有 x86 的 32 位目标计算机上处理器和标准引导参数，此命令将显示以下结果：

```dbgcmd
kd> dp nt!mmhighestuseraddress L1 
81f71864  7ffeffff 
```

这表示用户空间范围从 0x00000000 到 0x7FFEFFFF 的地址，因此范围最多 （这是标准的 32 位 Windows 安装上 0xFFFFFFFF） 的最高可能地址 0x80000000 为系统空间。

与 64 位目标计算机，将发生不同的值。 例如，此命令可能会显示以下信息：

```dbgcmd
0: kd> dp nt!mmhighestuseraddress L1 
fffff800`038b4010  000007ff`fffeffff 
```

这表示用户空间范围从 0x00000000\`00000000 到 0x000007FF\`FFFEFFFF。 因此，系统空间包括所有地址从 0x00000800\`向上 00000000。

有关 Windows 内存管理的详细信息，请参阅*Microsoft Windows Internals*由 David Solomon 和 Mark Russinovich （第四个版本，Microsoft Press，2005年）。

 

 





