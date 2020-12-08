---
title: 初始断点
description: 初始断点
keywords:
- 初始断点
- 断点，初始断点
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: ccd504cbdc94f2b89530c7c409e1705082232480
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838819"
---
# <a name="initial-breakpoint"></a>初始断点


当调试器启动新的目标应用程序时，在调用任何 DLL 初始化例程之前，会自动在主映像和所有静态链接的 Dll 之后加载初始断点。

调试器附加到现有用户模式应用程序时，将立即出现初始 [断点](using-breakpoints.md) 。

**-G** 命令行选项会使 WINDBG 或 CDB 忽略初始断点。 此时，你可以自动执行命令。 有关此情况的详细信息，请参阅 [控制异常和事件](controlling-exceptions-and-events.md)。

如果要在实际应用程序的执行即将开始时启动新目标并将其中断，请不要使用 **-g** 选项。 而是让初始断点发生。 调试程序处于活动状态后，在 **main** 或 **winmain** 例程上设置断点，然后使用 [**g (中转)**](g--go-.md) 命令。 然后，所有初始化过程都将运行，应用程序在即将开始执行主应用程序时停止。

有关内核模式下自动断点的详细信息，请参阅 [崩溃和重新启动目标计算机](crashing-and-rebooting-the-target-computer.md)。

 

 





