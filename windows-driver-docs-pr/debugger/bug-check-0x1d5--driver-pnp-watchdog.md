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
ms.openlocfilehash: c2a7e051f6bfadd0c607cc500784468008d566f7
ms.sourcegitcommit: 8e8aa927cf4ab56d0af652fa5e988a8ed6967904
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/25/2019
ms.locfileid: "72916230"
---
# <a name="bug-check-0x1d5-driver_pnp_watchdog"></a>Bug 检查0x1D5：驱动程序\_PNP\_监视器

驱动程序\_PNP\_监视器 bug 检查的值为0x000001D5。 这表明驱动程序在特定时间内未能完成 PnP 操作。

> [!IMPORTANT]
> 本主题面向程序员。 如果你是在使用计算机时收到蓝屏错误代码的客户，请参阅[排查蓝屏错误](https://www.windows.com/stopcode)。

 

## <a name="driver_pnp_watchdog-parameters"></a>驱动程序\_PNP\_监视器参数

|参数|描述|
|-------- |---------- |
|1| 与 devnode 关联的服务的前几个字符。|
|2| 指向 nt！Win10 RS4 和更高版本上的 TRIAGE_PNP_WATCHDOG。 |
|3| 负责 PnP 监视程序的线程。|
|4| 监视监视以来经过的时间（毫秒）。 |


## <a name="cause"></a>原因
-----

这表明驱动程序在特定时间内未能完成 PnP 操作。 [ **！分析**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-analyze)调试扩展显示有关 bug 检查的信息，可帮助确定根本原因。


## <a name="see-also"></a>另请参阅
----------

[Bug 检查代码引用](bug-check-code-reference2.md)

