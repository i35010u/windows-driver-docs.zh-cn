---
title: Bug 检查 0x1D5 DRIVER_PNP_WATCHDOG
description: DRIVER_PNP_WATCHDOG bug 检查的值为0x000001D5。 系统范围的监视程序已过期。 这表明驱动程序在特定时间内未能完成 PnP 操作。
keywords:
- Bug 检查 0x1D5 DRIVER_PNP_WATCHDOG
- DRIVER_PNP_WATCHDOG
ms.date: 01/11/2019
topic_type:
- apiref
api_name:
- DRIVER_PNP_WATCHDOG
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 308a2385b635cee0119e28c95aef81ed2b736682
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534830"
---
# <a name="bug-check-0x1d5-driver_pnp_watchdog"></a>Bug 检查0x1D5：驱动程序 \_ PNP \_ 监视器

驱动程序 \_ PNP \_ 监视器 bug 检查的值为0x000001D5。 这表明驱动程序在特定时间内未能完成 PnP 操作。

> [!IMPORTANT]
> 本主题适用于程序员。 如果你是在使用计算机时收到蓝屏错误代码的客户，请参阅[排查蓝屏错误](https://www.windows.com/stopcode)。

 

## <a name="driver_pnp_watchdog-parameters"></a>驱动程序 \_ PNP \_ 监视器参数

|参数|说明|
|-------- |---------- |
|1| 与 devnode 关联的服务的前几个字符。|
|2| 指向 nt！Win10 RS4 和更高版本上的 TRIAGE_PNP_WATCHDOG。 |
|3| 负责 PnP 监视程序的线程。|
|4| 监视监视以来经过的时间（毫秒）。 |


## <a name="cause"></a>原因
-----

这表明驱动程序在特定时间内未能完成 PnP 操作。 [**！分析**](-analyze.md)调试扩展显示有关 bug 检查的信息，可帮助确定根本原因。


## <a name="see-also"></a>另请参阅
----------

[Bug 检查代码参考](bug-check-code-reference2.md)

