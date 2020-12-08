---
title: 用户空间和系统空间
description: 用户空间和系统空间
keywords:
- 系统空间
- 系统空间，地址
- 系统空间，断点
- 内核空间
- 内核空间，地址
- 内核空间，断点
- 用户空间
- 用户空间，地址
- 用户空间，断点
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: d94f58aa17463ce82c2ea8f948ccc6911f860637
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803207"
---
# <a name="user-space-and-system-space"></a>用户空间和系统空间


Windows 为每个用户模式应用程序提供一个虚拟地址块。 这称为应用程序的 *用户空间* 。 应用程序不能直接访问其他大型地址块（称为 *系统空间* 或 *内核空间*）。

当 WinDbg 或 CDB 在用户空间中设置 [断点](using-breakpoints.md) 时，将在单个进程的用户空间的指定地址处设置此断点。 在用户模式调试过程中，当前进程确定虚拟地址的含义。 有关详细信息，请参阅 [控制进程和线程](controlling-processes-and-threads.md)。

在 "内核模式" 中，可以在用户空间中用 **bp**、 **bu** 和 **Ba** 命令或者通过 " **断点** " 对话框来设置断点。 首先，必须使用 *过程上下文* 来指定拥有该地址空间的用户模式进程，方法是使用 **. process/i** (或某些内核空间函数) 上特定于进程的断点，将目标切换为正确的 [进程上下文](changing-contexts.md#process-context)。

用户空间中的断点总是与设置断点时进程上下文处于活动状态的进程关联。 如果用户模式调试器正在调试此进程，并且如果内核调试器正在调试正在其上运行该进程的计算机，则此断点将中断到用户模式调试器，即使断点实际上是从内核调试器设置的。 此时，你可以从内核调试器中断系统，或使用 breakin (从用户模式调试器 [**中断到内核调试器)**](-breakin--break-to-the-kernel-debugger-.md) 命令，将控制转移到内核调试器。

### <a name="span-iddetermining_the_range_of_user_space_and_system_spacespanspan-iddetermining_the_range_of_user_space_and_system_spacespandetermining-the-range-of-user-space-and-system-space"></a><span id="determining_the_range_of_user_space_and_system_space"></span><span id="DETERMINING_THE_RANGE_OF_USER_SPACE_AND_SYSTEM_SPACE"></span>确定用户空间和系统空间的范围

如果需要确定目标计算机上的用户空间和系统空间的范围，可以使用 [**dp (显示**](d--da--db--dc--dd--dd--df--dp--dq--du--dw--dw--dyb--dyd--display-memor.md) 内核调试器中的内存) 命令，以显示 Windows 全局变量 **MmHighestUserAddress**。 此变量包含用户空间顶部的地址。 由于系统空间地址始终高于用户空间地址，因此此值允许您确定任何给定的地址是在用户空间中还是在内核空间内。

例如，在具有 x86 处理器和标准启动参数的32位目标计算机上，此命令将显示以下结果：

```dbgcmd
kd> dp nt!mmhighestuseraddress L1 
81f71864  7ffeffff 
```

这表示用户空间范围从地址0x00000000 到0x7FFEFFFF，系统空间因此从0x80000000 到最高可能的地址范围（) 的标准32位 Windows 安装为0xFFFFFFFF） (。

使用64位目标计算机时，会发生不同的值。 例如，此命令可能会显示以下内容：

```dbgcmd
0: kd> dp nt!mmhighestuseraddress L1 
fffff800`038b4010  000007ff`fffeffff 
```

这表示用户空间范围从 0x00000000 \` 00000000 到 0x000007FF \` FFFEFFFF。 因此，系统空间包含 0x00000800 00000000 的所有地址 \` 。

有关 Windows 内存管理的详细信息，请参阅 David 所罗门群岛的 *Microsoft Windows 内部机制* 和标记 Russinovich (第四版，microsoft 按，2005) 。

 

 





