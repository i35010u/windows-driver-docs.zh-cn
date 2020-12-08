---
title: 响应电池类驱动程序查询
description: 响应电池类驱动程序查询
keywords:
- 电池 miniclass 驱动程序 WDK，例程
- 例程 WDK 电池
- 电池 miniclass 驱动程序 WDK，状态报告
- 状态信息 WDK 电池
- 查询 WDK 电池
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0c3329916361f44f1df31eacc77d6e40c7643e6b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96784325"
---
# <a name="responding-to-battery-class-driver-queries"></a>响应电池类驱动程序查询


## <span id="ddk_responding_to_battery_class_driver_queries_dg"></span><span id="DDK_RESPONDING_TO_BATTERY_CLASS_DRIVER_QUERIES_DG"></span>


Miniclass 驱动程序必须提供以下三个 [BatteryMini *Xxx*](/windows-hardware/drivers/ddi/_battery/)例程，以报告电池状态：

[*BatteryMiniQueryTag*](/windows/win32/api/batclass/nc-batclass-bclass_query_tag_callback)

[*BatteryMiniQueryInformation*](/windows/win32/api/batclass/nc-batclass-bclass_query_information_callback)

[*BatteryMiniQueryStatus*](/windows/win32/api/batclass/nc-batclass-bclass_query_status_callback)

类驱动程序中的 [**BatteryClassIoctl**](/windows/win32/api/batclass/nf-batclass-batteryclassioctl) 例程在收到 IOCTLs 请求有关电池的信息时调用这些 miniclass 驱动程序例程。

 

