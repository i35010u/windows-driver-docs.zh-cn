---
title: 初始断点
description: 初始断点
ms.assetid: c7fda1f0-bbfb-41d8-b3c9-568f2f0a74e1
keywords:
- 初始断点
- 断点，初始断点
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 393e0bb94aa8788310f944fe99ca8fad747e5094
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575253"
---
# <a name="initial-breakpoint"></a>初始断点


当调试器启动新的目标应用程序时，在主映像后自动发生初始断点和任何 DLL 的初始化例程在调用之前加载的所有静态链接的 Dll。

当调试器附加到现有用户模式应用程序，一个初始[断点](using-breakpoints.md)会立即发生。

**-G**命令行选项将使 WinDbg 或 CDB 忽略初始断点。 现在可以自动执行命令。 有关这种情况的详细信息，请参阅[控制异常和事件](controlling-exceptions-and-events.md)。

如果你想要启动新的目标并进入它将要开始执行实际的应用程序时，不要使用 **-g**选项。 相反，允许发生初始断点。 调试器为活动状态后上, 设置断点**主要**或**winmain**例程，然后使用[ **g （转向）** ](g--go-.md)命令。 然后运行所有的初始化过程，并且该应用程序停止时执行的主应用程序即将开始。

有关在内核模式下自动断点的详细信息，请参阅[崩溃和重新启动目标计算机](crashing-and-rebooting-the-target-computer.md)。

 

 





