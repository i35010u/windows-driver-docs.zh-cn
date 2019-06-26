---
title: 电池微型类驱动程序的 Unload 例程
description: 电池微型类驱动程序的 Unload 例程
ms.assetid: f0acbf94-95d1-4a9d-aafd-1f868c5560cc
keywords:
- 电池 miniclass 驱动程序 WDK，例程
- 卸载例程
- 验证设备中卸载
- 卸载设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f7e6ed192b23ad69e1000ff4b37257877061ab99
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364722"
---
# <a name="unload-routine-of-a-battery-miniclass-driver"></a>电池微型类驱动程序的 Unload 例程


## <span id="ddk_unload_routine_of_battery_miniclass_driver_dg"></span><span id="DDK_UNLOAD_ROUTINE_OF_BATTERY_MINICLASS_DRIVER_DG"></span>


*Unload*例程电池 miniclass 驱动程序，确保所有驱动程序的设备已被删除并释放 miniclass 驱动程序已分配的任何资源。

*Unload*例程应首先检查以确保所有设备已被删除并且，如果没有，请执行以下操作为每个剩余的设备：

1.  调用[ **BatteryClassUnload** ](https://docs.microsoft.com/windows/desktop/api/batclass/nf-batclass-batteryclassunload)以通知的类驱动程序 miniclass 驱动程序正在卸载设备。

2.  禁用来自较低的驱动程序，如 ACPI 驱动程序，使用该驱动程序接口的任何设备通知。

3.  删除设备的设备对象通过调用[ **IoDeleteDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iodeletedevice)，按如下所示：

    ```cpp
        IoDeleteDevice (NewBatt->DeviceObject);
    ```

所有 miniclass 驱动程序的设备将被卸载之后, *Unload*例程应释放 miniclass 驱动程序分配的任何资源。

Miniclass 驱动*Unload*后已删除的驱动程序的所有设备随时可以调用例程。 PnP 管理器调用*Unload*例程的 IRQL 在系统线程上下文中 = 被动\_级别。

 

 




