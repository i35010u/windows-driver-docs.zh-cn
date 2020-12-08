---
title: 调试中断
description: 调试中断
keywords:
- 调试中断
- 控制目标、调试中断
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4e69b6ed9a70ace9d768899489a87c2af6eefe4b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823453"
---
# <a name="debug--break"></a>调试 | 中断


## <span id="ddk_debug_break_dbg"></span><span id="DDK_DEBUG_BREAK_DBG"></span>


单击 "**调试**" 菜单上的 "**中断**"，停止目标的执行并将控制返回到调试器。

在用户模式下，此命令将停止进程及其线程，使你能够重新获得调试器的控制权。 在内核模式下，此命令将进入目标计算机。

还可以在调试器处于活动状态时使用此命令。 在这种情况下，该命令会截断长时间 [调试器命令窗口](debugger-command-window.md) 显示。

**Break** 命令等效于按 CTRL + break，或单击工具栏上的 "中断" 按钮)  (屏幕截图上的 "中断 **(ctrl + break)** 按钮 ![ ](images/tbbreak.png) 。

### <a name="span-idalt_delspanspan-idalt_delspanaltdel"></a><span id="ALT_DEL"></span><span id="alt_del"></span>ALT + DEL

可以使用 **ALT + DEL** 发送 **中断**。 **ALT + DEL** 的工作方式与 **中断 (Ctrl + break) 相同。**

### <a name="span-iduser_mode_effectsspanspan-iduser_mode_effectsspanuser-mode-effects"></a><span id="user_mode_effects"></span><span id="USER_MODE_EFFECTS"></span>用户模式效果

在用户模式下， **break** 命令使目标应用程序中断到调试器。 目标应用程序停止，调试器将变为活动状态，你可以输入调试器命令。

如果调试器已处于活动状态，则 **中断** 不会影响目标应用程序。 但是，你可以使用此命令来终止调试器命令。 例如，如果您请求了长时间的显示，并且不希望看到更多的显示，则 **Break** 将结束显示并返回到调试器命令提示符。

当你通过 WinDbg 执行远程调试时，可以按下主计算机键盘上的 Break 键。 如果要从目标计算机的键盘发出中断，请在基于 x86 的计算机上使用 CTRL + C。

当正在调试的应用程序繁忙时，可以按 F12 键来打开命令提示符。 单击其中一个目标应用程序窗口，然后在目标计算机上按 F12。

### <a name="span-idkernel_mode_effectsspanspan-idkernel_mode_effectsspankernel-mode-effects"></a><span id="kernel_mode_effects"></span><span id="KERNEL_MODE_EFFECTS"></span>内核模式效果

在内核模式下， **break** 命令导致目标计算机中断到调试器。 此命令锁定目标计算机并唤醒调试器。

调试仍在运行的系统时，必须按主机键盘上的 Break 键才能打开初始命令提示符。

如果调试器已处于活动状态，则 **中断** 不会影响目标计算机。 但是，你可以使用此命令来终止调试器命令。 例如，如果您请求了长时间的显示，并且不希望看到更多的显示，则 **Break** 将结束显示并返回到调试器命令提示符。

当调试器命令正在生成长时间显示或目标计算机繁忙时，还可以使用 **Break** 来打开命令提示符。 调试基于 x86 的计算机时，还可以在目标键盘上按 CTRL + C 以获得相同效果。

增强型键盘上的 SYSRQ 键 (或按 ALT + SYSRQ) 类似。 此密钥适用于任何处理器上的主机或目标键盘。 但是，此键仅在您之前按下 CTRL + C 打开提示的情况下才起作用。

可以通过编辑注册表来禁用 SYSRQ 键。 在 HKEY \_ LOCAL \_ MACHINE \\ System \\ CurrentControlSet \\ Services \\ i8042prt \\ Parameters 注册表项中，创建一个名为 **BreakOnSysRq** 的值并将其设置为等于 DWORD 0x0。 然后重启计算机。 重新启动计算机后，可以按目标计算机键盘上的 SYSRQ 键，而不会中断内核调试器。

### <a name="span-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

KD 和 CDB 中的相应键为 [**CTRL + C**](ctrl-c--break-.md)。 有关控制程序执行的其他方法的详细信息，请参阅 [控制目标](controlling-the-target.md)。

 

 





