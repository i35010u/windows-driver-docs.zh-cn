---
title: 调试内核连接周期初始中断
description: 调试内核连接周期初始中断
ms.assetid: e4dbb810-d9b3-4721-89ec-af4b5e244cc0
keywords:
- 调试内核连接周期初始中断
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: a4f520cd1c3d1fb6ae882ddacbd0de8d41380050
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374355"
---
# <a name="debug--kernel-connection--cycle-initial-break"></a>调试 | 内核连接 | 循环初始中断


## <span id="ddk_debug_kernel_connection_cycle_initial_break_dbg"></span><span id="DDK_DEBUG_KERNEL_CONNECTION_CYCLE_INITIAL_BREAK_DBG"></span>


指向**内核连接**，然后单击**周期初始中断**上**调试**菜单来更改在其，调试器将自动中断到目标的条件计算机。

此命令相当于按下 CTRL + ALT + K。 （您可以同时按 CTRL + K KD 中。）

此命令会使内核调试程序，以下三种状态之间循环：

<span id="No_break"></span><span id="no_break"></span><span id="NO_BREAK"></span>**无分隔符**  
到目标计算机不会中断调试器，除非你按[CTRL + BREAK](debug---break.md)或调试 |中断。

<span id="Break_on_reboot"></span><span id="break_on_reboot"></span><span id="BREAK_ON_REBOOT"></span>**在重新启动时中断**  
内核初始化后，调试器将中断重启的目标计算机。 此命令相当于使用-b 启动 WinDbg [**命令行选项**](windbg-command-line-options.md)。

<span id="Break_on_first_module_load"></span><span id="break_on_first_module_load"></span><span id="BREAK_ON_FIRST_MODULE_LOAD"></span>**第一个模块加载时中断**  
第一个内核模块加载之后，调试器将中断重启的目标计算机。 (此操作会导致要比前面**上重新启动中断**状态。)此命令相当于使用-d 启动 WinDbg [**命令行选项**](windbg-command-line-options.md)。

当你使用**周期初始中断**命令时，显示新的中断状态。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关相关的命令和重新启动过程将如何影响调试器的说明的详细信息，请参阅[崩溃和重新启动目标计算机](crashing-and-rebooting-the-target-computer.md)。

 

 





