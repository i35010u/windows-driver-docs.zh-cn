---
title: 禁用 EA 恢复
description: 禁用 EA 恢复
keywords:
- 显示驱动程序 WDK Windows 2000，调试
- 调试驱动程序 WDK Windows 2000 显示
- EA recovery WDK Windows 2000 显示
- 禁用的 EA recovery WDK Windows 2000 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 15b88ce3fc495ed44ac06d41d2ba8ebbd1890fe6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96809291"
---
# <a name="disabling-ea-recovery"></a>禁用 EA 恢复


## <span id="ddk_disabling_ea_recovery_gg"></span><span id="DDK_DISABLING_EA_RECOVERY_GG"></span>


在 Microsoft Windows XP SP1 和更高版本的操作系统中，GDI 使用监视程序计时器来监视线程在显示驱动程序中执行的时间。 监视器定义时间阈值。 如果某个线程在显示器驱动程序中花费的时间超过了阈值，则监视器将通过切换到 VGA 图形模式来尝试恢复。 如果尝试失败，监视器会生成 bug 检查0xEA，线程 \_ \_ 在 \_ 设备 \_ 驱动程序中停滞。

尝试恢复之前，监视程序将中断连接到计算机的任何调试器。 然后，只要已禁用 EA 恢复，就可以调试代码。

在 Windows XP SP1 中，通过将 *watchdog.sys* 中的全局变量 **WdDisableRecovery** 设置为1来禁用 EA 恢复。 为此，可以输入以下 **WinDbg** 命令：

```cmd
ed watchdog!WdDisableRecovery 1
```

在 Microsoft Windows Server 2003 中，通过将 *videoprt.sys* 中的全局变量 **VpDisableRecovery** 设置为1来禁用 EA 恢复。 为此，可以输入以下 **WinDbg** 命令：

```cmd
ed videoprt!VpDisableRecovery 1
```

禁用 EA 恢复后，将断点放置在您怀疑代码循环的显示驱动程序中，然后再继续执行。

 

 





