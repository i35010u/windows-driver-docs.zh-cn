---
title: 响应电池类驱动程序查询
description: 响应电池类驱动程序查询
ms.assetid: 00b24b37-d312-46ee-8218-2bd7a9453d13
keywords:
- 电池 miniclass 驱动程序 WDK，例程
- 例程 WDK 电池
- 电池 miniclass 驱动程序 WDK，状态报告
- WDK 电池的状态信息
- 查询 WDK 电池
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ffd97504e09fbed7ac9b259ad55cb2f8f810777a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566748"
---
# <a name="responding-to-battery-class-driver-queries"></a>响应电池类驱动程序查询


## <span id="ddk_responding_to_battery_class_driver_queries_dg"></span><span id="DDK_RESPONDING_TO_BATTERY_CLASS_DRIVER_QUERIES_DG"></span>


Miniclass 驱动程序必须提供以下三种[BatteryMini*Xxx* ](https://msdn.microsoft.com/library/windows/hardware/ff536286)例程，电池的状态报告：

[*BatteryMiniQueryTag*](https://msdn.microsoft.com/library/windows/hardware/ff536275)

[*BatteryMiniQueryInformation*](https://msdn.microsoft.com/library/windows/hardware/ff536273)

[*BatteryMiniQueryStatus*](https://msdn.microsoft.com/library/windows/hardware/ff536274)

[ **BatteryClassIoctl** ](https://msdn.microsoft.com/library/windows/hardware/ff536267)例程中的类驱动程序收到 Ioctl 请求有关电池的信息时调用这些 miniclass 驱动程序例程。

 

 




