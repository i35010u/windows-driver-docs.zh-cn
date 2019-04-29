---
title: 禁用 EA 恢复
description: 禁用 EA 恢复
ms.assetid: a414f1b0-acfc-4617-bf68-202bdef829ce
keywords:
- 显示驱动程序 WDK Windows 2000 中，调试
- 显示调试驱动程序 WDK Windows 2000
- EA 恢复 WDK Windows 2000 显示
- 已禁用的 EA 恢复 WDK Windows 2000 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e30b288731f61677866225bedd5466c4f2012885
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367383"
---
# <a name="disabling-ea-recovery"></a>禁用 EA 恢复


## <span id="ddk_disabling_ea_recovery_gg"></span><span id="DDK_DISABLING_EA_RECOVERY_GG"></span>


在 Microsoft Windows XP SP1 和更高版本操作系统中，GDI 使用监视程序计时器来监视线程中显示器驱动程序执行所花费的时间。 监视器定义的时间阈值。 如果线程在花费的显示驱动程序中的时间比指定的阈值，监视器将尝试通过切换到 VGA 图形模式下恢复。 如果该尝试失败，监视器将生成 bug 检查 0xEA，线程\_STUCK\_IN\_设备\_驱动程序。

然后再尝试恢复，监视器会中断任何调试程序附加到计算机。 只要第一个已禁用 EA 恢复，然后可以调试代码-。

设置全局变量，在 Windows XP SP1 中，禁用 EA 恢复**WdDisableRecovery**，位于*watchdog.sys*，为 1。 若要执行此操作，可以输入以下**WinDbg**命令：

```cmd
ed watchdog!WdDisableRecovery 1
```

设置全局变量，在 Microsoft Windows Server 2003 中，禁用 EA 恢复**VpDisableRecovery**，位于*videoprt.sys*，为 1。 若要执行此操作，可以输入以下**WinDbg**命令：

```cmd
ed videoprt!VpDisableRecovery 1
```

已禁用 EA 恢复后，您怀疑循环代码，显示驱动程序中放置断点，并恢复执行。

 

 





