---
title: 测试显示驱动程序时禁用监视计时器
description: 测试显示驱动程序时禁用监视计时器
keywords:
- 显示驱动程序 WDK Windows 2000，调试
- 调试驱动程序 WDK Windows 2000 显示
- 监视器计时器 WDK Windows 2000 显示
- 计时器，WDK Windows 2000 显示
- VGA WDK Windows 2000 显示器
- 切换到 VGA 模式，WDK Windows 2000 显示
- 线程监视计时器，WDK Windows 2000 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fd58bd90d585cf6bce1430dd95ed6df311194d97
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96809283"
---
# <a name="disabling-the-watchdog-timer-while-testing-display-drivers"></a>测试显示驱动程序时禁用监视计时器


## <span id="ddk_disabling_the_watchdog_timer_while_testing_display_drivers_gg"></span><span id="DDK_DISABLING_THE_WATCHDOG_TIMER_WHILE_TESTING_DISPLAY_DRIVERS_GG"></span>


在 Microsoft Windows XP SP1 和更高版本的操作系统中，GDI 使用监视程序计时器来监视线程在显示驱动程序中执行的时间。 监视器定义时间阈值。 如果某个线程在显示器驱动程序中花费的时间超过了阈值，则监视器将通过切换到 VGA 图形模式来尝试恢复。 如果尝试失败，监视器会生成 bug 检查0xEA，线程 \_ \_ 在 \_ 设备 \_ 驱动程序中停滞。

如果在调试和测试过程中，您将使用软件模拟来呈现显示适配器最终将执行的呈现，则您可能需要增加监视器时间阈值。 否则，与硬件相比，呈现速度要慢得多的模拟代码会超出阈值。

若要为显示驱动程序指定监视程序时间阈值，请 \_ 在注册表中创建以下 REG DWORD 条目：

```registry
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Watchdog\Display\BreakPointDelay
```

将 **BreakPointDelay** 的值设置为 "监视时间" 阈值，以10秒为单位。 例如，值200指定阈值2000秒。

如果在没有附加调试器的情况下测试显示器驱动程序，则可以防止监视程序计时器生成 bug 检查。 为此，请 \_ 在注册表中创建以下 REG DWORD 项，并将其值设置为1：

```registry
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Watchdog\Display\DisableBugCheck
```

本主题中所述的技术仅用于调试和测试。 请不要释放创建或更改 **BreakPointDelay** 或 **DisableBugCheck** 的驱动程序。

 

 





