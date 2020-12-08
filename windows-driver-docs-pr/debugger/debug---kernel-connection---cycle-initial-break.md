---
title: 调试内核连接循环初始中断
description: 调试内核连接循环初始中断
keywords:
- 调试内核连接循环初始中断
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: b60077087f073b7b2c980869898a0b0d8ddcb721
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823409"
---
# <a name="debug--kernel-connection--cycle-initial-break"></a>调试 | 内核连接 | 循环初始中断


## <span id="ddk_debug_kernel_connection_cycle_initial_break_dbg"></span><span id="DDK_DEBUG_KERNEL_CONNECTION_CYCLE_INITIAL_BREAK_DBG"></span>


指向 "**内核连接**"，然后单击 "**调试**" 菜单上的 "**循环初始断点**"，以更改调试器自动中断到目标计算机的条件。

此命令等效于按 CTRL + ALT + K。  (还可以在 KD 中按 CTRL + K ) 

此命令会导致内核调试器遍历以下三种状态：

<span id="No_break"></span><span id="no_break"></span><span id="NO_BREAK"></span>**无中断**  
调试器不会中断目标计算机，除非按 [CTRL + break](debug---break.md) 或 Debug |分.

<span id="Break_on_reboot"></span><span id="break_on_reboot"></span><span id="BREAK_ON_REBOOT"></span>**重新启动时中断**  
在内核初始化后，调试器将进入重启的目标计算机。 此命令等效于通过-b [**命令行选项**](windbg-command-line-options.md)启动 WinDbg。

<span id="Break_on_first_module_load"></span><span id="break_on_first_module_load"></span><span id="BREAK_ON_FIRST_MODULE_LOAD"></span>**第一次模块加载时中断**  
加载第一个内核模块后，调试器将进入重启的目标计算机。  (此操作将导致中断在 **重新启动** 状态之前中断。 ) 此命令等效于通过-d [**命令行选项**](windbg-command-line-options.md)启动 WinDbg。

使用 " **循环初始中断** " 命令时，将显示新的中断状态。

### <a name="span-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关相关命令的详细信息以及重新启动过程如何影响调试器的说明，请参阅 [崩溃并重新启动目标计算机](crashing-and-rebooting-the-target-computer.md)。

 

 





