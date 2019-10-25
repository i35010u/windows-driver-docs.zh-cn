---
title: 电池微型类驱动程序的 AddDevice 例程
description: 电池微型类驱动程序的 AddDevice 例程
ms.assetid: 1b34e223-e238-4547-bd44-754be2e6749c
keywords:
- AddDevice 例程 WDK 电池
- 电池 miniclass 驱动程序 WDK，例程
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3ddbfc3ea8a22318cf78316a91e2d3574f47742b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832230"
---
# <a name="adddevice-routine-of-a-battery-miniclass-driver"></a>电池微型类驱动程序的 AddDevice 例程


## <span id="ddk_adddevice_routine_of_battery_miniclass_driver_dg"></span><span id="DDK_ADDDEVICE_ROUTINE_OF_BATTERY_MINICLASS_DRIVER_DG"></span>


每个电池 miniclass 驱动程序必须具有[*AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)例程，该例程初始化特定于电池的状态。 PnP 管理器通过此 miniclass 驱动程序控制的每个电池设备调用*AddDevice*例程。

除了 PnP *AddDevice*例程所需的任务外，还必须执行以下操作：用于电池 miniclass 驱动程序的*AddDevice*例程：

1.  为电池创建 FDO，并将 FDO 连接到控制器的设备堆栈。

2.  初始化[**电池\_微型端口\_信息**](https://docs.microsoft.com/windows/desktop/api/batclass/ns-batclass-battery_miniport_info)结构并调用[**BatteryClassInitializeDevice**](https://docs.microsoft.com/windows/desktop/api/batclass/nf-batclass-batteryclassinitializedevice) ，将 miniclass 驱动程序注册到电池类驱动程序。

3.  执行设备所需的任何其他初始化。

 

 




