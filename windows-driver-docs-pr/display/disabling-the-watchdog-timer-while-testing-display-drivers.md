---
title: 测试显示驱动程序时禁用监视计时器
description: 测试显示驱动程序时禁用监视计时器
ms.assetid: dc0c9e64-044b-4b2c-8011-9bdbf121307c
keywords:
- 显示驱动程序 WDK Windows 2000 中，调试
- 显示调试驱动程序 WDK Windows 2000
- 显示监视器计时器 WDK Windows 2000
- 显示计时器 WDK Windows 2000
- VGA WDK Windows 2000 显示
- 切换到 VGA 模式 WDK Windows 2000 显示
- 显示线程监视程序计时器 WDK Windows 2000
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 661d919bdfa4fa9d0579f6b4e1866e33b3466522
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568124"
---
# <a name="disabling-the-watchdog-timer-while-testing-display-drivers"></a>测试显示驱动程序时禁用监视计时器


## <span id="ddk_disabling_the_watchdog_timer_while_testing_display_drivers_gg"></span><span id="DDK_DISABLING_THE_WATCHDOG_TIMER_WHILE_TESTING_DISPLAY_DRIVERS_GG"></span>


在 Microsoft Windows XP SP1 和更高版本操作系统中，GDI 使用监视程序计时器来监视线程中显示器驱动程序执行所花费的时间。 监视器定义的时间阈值。 如果线程在花费的显示驱动程序中的时间比指定的阈值，监视器将尝试通过切换到 VGA 图形模式下恢复。 如果该尝试失败，监视器将生成 bug 检查 0xEA，线程\_STUCK\_IN\_设备\_驱动程序。

如果在调试和测试，您对于显示适配器将最终执行的呈现使用软件模拟，您可能需要增加监视器时间阈值。 否则，很可能仿真代码来呈现明显比硬件，运行速度更慢，将超出了阈值。

若要指定显示器驱动程序的监视程序时间阈值，请创建以下注册表\_DWORD 注册表项：

```registry
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Watchdog\Display\BreakPointDelay
```

设置的值**BreakPointDelay**监视器时间阈值，以 10 秒为单位。 例如，值为 200 指定阈值为 2,000 秒。

如果测试显示驱动程序不附加调试器，可以防止生成的 bug 检查监视计时器。 若要执行此操作，创建以下注册表\_DWORD 项在注册表中，并将其值设置为 1:

```registry
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Watchdog\Display\DisableBugCheck
```

本主题中描述的方法仅适用于调试和测试。 不会创建或更改的驱动程序释放**BreakPointDelay**或**DisableBugCheck**。

 

 





