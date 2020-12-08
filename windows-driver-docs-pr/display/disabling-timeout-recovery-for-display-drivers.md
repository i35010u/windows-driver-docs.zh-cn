---
title: 对显示驱动程序禁用超时恢复
description: 对显示驱动程序禁用超时恢复
keywords:
- 显示驱动程序 WDK Windows 2000，恢复超时
- timeout 恢复 WDK Windows 2000 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ca954867714e0e31c3c955e806b523bef143e5a1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96809275"
---
# <a name="disabling-timeout-recovery-for-display-drivers"></a>对显示驱动程序禁用超时恢复


在 Microsoft Windows XP SP1 和更高版本的操作系统中，GDI 使用监视程序计时器来监视线程在显示驱动程序中执行的时间。 监视器定义时间阈值。 如果某个线程在显示器驱动程序中花费的时间超过了阈值，则监视器将通过切换到 VGA 图形模式来尝试恢复。 如果尝试失败，监视器会生成 bug 检查0xEA，线程 \_ \_ 在 \_ 设备 \_ 驱动程序中停滞。

由于超时恢复代码很复杂，因此可能会导致与显示驱动程序不兼容。 若要解决兼容性问题，可以禁用超时恢复。

若要禁用超时恢复，请 \_ 在注册表中创建以下 REG DWORD 条目，并将其值设置为0：

```registry
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Watchdog\Display\EaRecovery
```

 

 





