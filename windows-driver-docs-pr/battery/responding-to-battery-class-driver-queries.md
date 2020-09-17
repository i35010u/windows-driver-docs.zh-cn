---
title: 响应电池类驱动程序查询
description: 响应电池类驱动程序查询
ms.assetid: 00b24b37-d312-46ee-8218-2bd7a9453d13
keywords:
- 电池 miniclass 驱动程序 WDK，例程
- 例程 WDK 电池
- 电池 miniclass 驱动程序 WDK，状态报告
- 状态信息 WDK 电池
- 查询 WDK 电池
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 55caae53a077a81d8f87d479fc38a0a8df258337
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90716590"
---
# <a name="responding-to-battery-class-driver-queries"></a>响应电池类驱动程序查询


## <span id="ddk_responding_to_battery_class_driver_queries_dg"></span><span id="DDK_RESPONDING_TO_BATTERY_CLASS_DRIVER_QUERIES_DG"></span>


Miniclass 驱动程序必须提供以下三个[BatteryMini*Xxx* ](/windows-hardware/drivers/ddi/_battery/)例程，以报告电池状态：

[*BatteryMiniQueryTag*](/windows/win32/api/batclass/nc-batclass-bclass_query_tag_callback)

[*BatteryMiniQueryInformation*](/windows/win32/api/batclass/nc-batclass-bclass_query_information_callback)

[*BatteryMiniQueryStatus*](/windows/win32/api/batclass/nc-batclass-bclass_query_status_callback)

类驱动程序中的 [**BatteryClassIoctl**](/windows/win32/api/batclass/nf-batclass-batteryclassioctl) 例程在收到 IOCTLs 请求有关电池的信息时调用这些 miniclass 驱动程序例程。

 

