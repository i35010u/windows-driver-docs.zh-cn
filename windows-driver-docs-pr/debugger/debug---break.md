---
title: 调试中断
description: 调试中断
ms.assetid: fc17d0b2-3ef5-4e10-a6a3-51f7011fddcf
keywords:
- 调试中断
- 控制目标，调试中断
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: b28b6aaf40ae0dde309755303c61321ca8cc7b3b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374372"
---
# <a name="debug--break"></a>调试 | 中断


## <span id="ddk_debug_break_dbg"></span><span id="DDK_DEBUG_BREAK_DBG"></span>


单击**中断**上**调试**菜单以终止的目标执行并返回到调试器。

在用户模式下，此命令停止进程和线程，您可以重新获取调试器的控制。 在内核模式下，此命令将分成在目标计算机。

在调试器处于活动状态时，还可以使用此命令。 在此情况下，该命令将长时间截断[调试器命令窗口](debugger-command-window.md)显示。

**中断**命令等效于按 CTRL + BREAK 或单击**中断 (Ctrl + Break)** 按钮 (![中断按钮的屏幕截图](images/tbbreak.png)) 工具栏上。

### <a name="span-idaltdelspanspan-idaltdelspanaltdel"></a><span id="ALT_DEL"></span><span id="alt_del"></span>ALT+DEL

可以使用**ALT + DEL**发送**中断**。 **ALT + DEL**的工作方式相同**中断 (Ctrl + Break)。**

### <a name="span-idusermodeeffectsspanspan-idusermodeeffectsspanuser-mode-effects"></a><span id="user_mode_effects"></span><span id="USER_MODE_EFFECTS"></span>用户模式下的效果

在用户模式下**中断**命令导致目标应用程序进入调试器。 目标应用程序会停止，调试器将变为活动状态，并且可以输入的调试器命令。

如果调试器已处于活动状态，**中断**不会影响目标应用程序。 但是，此命令可用于终止调试器命令。 例如，如果已请求很长并且不想看到的再**中断**将结束显示并使你返回到调试器命令提示符下。

当您在执行使用 WinDbg 进行远程调试时，你可以主计算机的键盘上按 Break 键。 如果你想要发出从目标计算机的键盘中断，请在基于 x86 的计算机上使用 CTRL + C。

可以按 F12 键以打开命令提示符下，当正在调试的应用程序繁忙时。 单击其中一个目标应用程序的 windows，在目标计算机上按 F12。

### <a name="span-idkernelmodeeffectsspanspan-idkernelmodeeffectsspankernel-mode-effects"></a><span id="kernel_mode_effects"></span><span id="KERNEL_MODE_EFFECTS"></span>内核模式的效果

在内核模式下**中断**命令将导致目标计算机进入调试器。 此命令将锁定目标计算机并唤醒调试器。

调试仍在运行的系统时，您必须按 Break 键主机键盘上打开初始的命令提示符。

如果调试器已处于活动状态，**中断**不会影响目标计算机。 但是，此命令可用于终止调试器命令。 例如，如果已请求很长并且不想看到的再**中断**将结束显示并使你返回到调试器命令提示符下。

此外可以使用**中断**若要打开命令提示符下，调试器命令生成很长或当目标计算机是繁忙时。 调试基于 x86 的计算机时，您还可以具有相同的效果目标键盘上按 CTRL + C。

SYSRQ 密钥 （或增强型键盘上的按 ALT + SYSRQ） 是类似。 从任何处理器上的主机或目标键盘此密钥适用。 但是，此密钥仅适用于您通过按 CTRL + C 之前至少一次打开提示符。

可以通过编辑注册表禁用 SYSRQ 密钥。 在 HKEY\_本地\_机\\系统\\CurrentControlSet\\Services\\i8042prt\\参数注册表项，请创建一个名为值**BreakOnSysRq**并将其设置为等于 DWORD 0x0。 然后重启计算机。 在重新启动计算机后，可以将目标计算机的键盘上按 SYSRQ 密钥并不会中断内核调试程序。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

KD 和 CDB 中对应的项是[ **CTRL + C**](ctrl-c--break-.md)。 控制程序执行的其他方法的详细信息，请参阅[控制目标](controlling-the-target.md)。

 

 





