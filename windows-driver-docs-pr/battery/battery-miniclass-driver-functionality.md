---
title: 电池微型类驱动程序功能
description: 电池微型类驱动程序功能
ms.assetid: f8da63fd-0bf9-4085-88c2-022c4ddc7caa
keywords:
- 电池 miniclass 驱动程序 WDK，功能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fd197e30cd27f60aef492ffee1f936d33c131ef8
ms.sourcegitcommit: 7a7e61b4147a4aa86bf820fd0b0c7681fe17e544
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89056931"
---
# <a name="battery-miniclass-driver-functionality"></a>电池微型类驱动程序功能


## <span id="ddk_battery_miniclass_driver_functionality_dg"></span><span id="DDK_BATTERY_MINICLASS_DRIVER_FUNCTIONALITY_DG"></span>


电池 miniclass 驱动程序负责以下操作：

-   为其设备创建 FDO，并在关联的设备扩展中存储设备特定的信息

-   分配和维护当前电池的电池标记

-   跟踪电池容量、充电和电源状态

-   响应来自类驱动程序的电池状态信息的请求

-   在电池电源状态发生变化时通知电池类驱动程序

-   请求充电或放电特定电池

电池 miniclass 驱动程序为其他操作（如处理 IOCTLs）调用电池类驱动程序的支持例程，如 [电池类驱动程序功能](battery-class-driver-functionality.md)中所述。

每个电池 miniclass 驱动程序都提供一组[BatteryMini*Xxx* ](/windows-hardware/drivers/ddi/_battery/)例程。 电池类驱动程序调用这些例程来请求 miniclass 驱动程序执行特定于设备的任务。 此外，miniclass 驱动程序还必须具有其他例程，如 [提供所需的电池 Miniclass 驱动程序功能](supplying-required-battery-miniclass-driver-functionality.md)中所述。

 

