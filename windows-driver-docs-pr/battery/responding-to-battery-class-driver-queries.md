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
ms.openlocfilehash: e6d89d4ec11fbf7c850ee11c5bf2a39bb681eaa3
ms.sourcegitcommit: 7a7e61b4147a4aa86bf820fd0b0c7681fe17e544
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89056887"
---
# <a name="responding-to-battery-class-driver-queries"></a>响应电池类驱动程序查询


## <span id="ddk_responding_to_battery_class_driver_queries_dg"></span><span id="DDK_RESPONDING_TO_BATTERY_CLASS_DRIVER_QUERIES_DG"></span>


Miniclass 驱动程序必须提供以下三个[BatteryMini*Xxx* ](/windows-hardware/drivers/ddi/_battery/)例程，以报告电池状态：

[*BatteryMiniQueryTag*](/windows/desktop/api/batclass/nc-batclass-bclass_query_tag_callback)

[*BatteryMiniQueryInformation*](/windows/desktop/api/batclass/nc-batclass-bclass_query_information_callback)

[*BatteryMiniQueryStatus*](/windows/desktop/api/batclass/nc-batclass-bclass_query_status_callback)

类驱动程序中的 [**BatteryClassIoctl**](/windows/desktop/api/batclass/nf-batclass-batteryclassioctl) 例程在收到 IOCTLs 请求有关电池的信息时调用这些 miniclass 驱动程序例程。

 

