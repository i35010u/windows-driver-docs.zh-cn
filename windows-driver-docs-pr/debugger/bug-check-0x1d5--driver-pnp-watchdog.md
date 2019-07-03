---
title: Bug 检查 0x1D5 DRIVER_PNP_WATCHDOG
description: DRIVER_PNP_WATCHDOG bug 检查具有 0x000001D5 值。 系统宽监视器已过期。 这表示该驱动程序未成功完成特定的时间内的即插即用操作。
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
ms.openlocfilehash: a184b3b62bf46131b7254f7f13f698c422534652
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2019
ms.locfileid: "67519648"
---
# <a name="bug-check-0x1d5-driverpnpwatchdog"></a>Bug 检查 0x1D5：驱动程序\_PNP\_监视器

该驱动程序\_PNP\_监视器 bug 检查的值为 0x000001D5。 这表示一个驱动程序未能完成特定的时间内的即插即用操作。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://www.windows.com/stopcode)。

 

## <a name="driverpnpwatchdog-parameters"></a>驱动程序\_PNP\_监视程序参数

|参数|描述|
|-------- |---------- |
|1| Devnode 与关联的服务的第一个几个字符。|
|2| 指向 nt ！TRIAGE_PNP_WATCHDOG 上 Win10 RS4 及更高版本。 |
|3| 线程负责即插即用监视器。|
|4| 监视器已有后经过的毫秒数。 |


## <a name="cause"></a>原因
-----

这表示一个驱动程序未能完成特定的时间内的即插即用操作。


## <a name="see-also"></a>请参阅
----------

[Bug 检查代码参考](bug-check-code-reference2.md)

