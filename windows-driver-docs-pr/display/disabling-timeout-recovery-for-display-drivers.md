---
title: 禁用显示器驱动程序的超时恢复
description: 禁用显示器驱动程序的超时恢复
ms.assetid: 71fa0273-be21-4603-8491-09078a38cdf2
keywords:
- 显示驱动程序 WDK Windows 2000 中，超时恢复
- 超时恢复 WDK Windows 2000 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 72d81deeb25086e6847ef7cecfefe3423be7b9db
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534314"
---
# <a name="disabling-timeout-recovery-for-display-drivers"></a>禁用显示器驱动程序的超时恢复


在 Microsoft Windows XP SP1 和更高版本操作系统中，GDI 使用监视程序计时器来监视线程中显示器驱动程序执行所花费的时间。 监视器定义的时间阈值。 如果线程在花费的显示驱动程序中的时间比指定的阈值，监视器将尝试通过切换到 VGA 图形模式下恢复。 如果该尝试失败，监视器将生成 bug 检查 0xEA，线程\_STUCK\_IN\_设备\_驱动程序。

超时的恢复代码很复杂，因为它可能会导致与显示器驱动程序不兼容。 若要解决的兼容性问题，可以禁用超时恢复。

若要禁用超时恢复，请创建以下注册表\_DWORD 项在注册表中，并将其值设置为 0:

```registry
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Watchdog\Display\EaRecovery
```

 

 





