---
title: 处理对存储外设的电源请求
description: 处理对存储外设的电源请求
ms.assetid: 3cc7b885-27ad-4384-aeec-4d76f9ad4f1c
keywords:
- 外围设备 WDK 存储，电源请求
- 存储外围设备 WDK，电源请求
- power requests WDK 存储
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1b62cf17e23342fb413208bff02cde295f664ba8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826291"
---
# <a name="handling-power-requests-to-storage-peripherals"></a>处理对存储外设的电源请求


## <span id="ddk_handling_power_requests_to_storage_peripherals_kg"></span><span id="DDK_HANDLING_POWER_REQUESTS_TO_STORAGE_PERIPHERALS_KG"></span>


存储类驱动程序负责发出用于处理电源请求的特定于设备的命令。 最常见的存储类驱动程序：

-   如果处理此类 i/o 可能会阻止驱动程序在合理的数量中出现 MN 请求，则会阻止其设备响应查询电源请求（IRP\_MJ\_POWER with [**irp\_\_查询\_power**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-power)）时间

-   设置设备的电源状态，以响应设置电源请求（IRP\_MJ\_POWER with [**irp\_MN\_集\_电源**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power)）

-   重新启动其设备的 i/o，以响应设置电源请求以打开设备

-   将电源请求转发到下一个较低的驱动程序。

请注意，驱动程序必须调用[**PoStartNextPowerIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-postartnextpowerirp)和[**PoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver)，而不是**IoCallDriver**来发送 power 请求。

除非存储类驱动程序具有[**StartIo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio)例程，否则应在设置设备的电源状态之前，先将存储端口驱动程序的 LU 特定队列（IRP\_MJ\_SCSI 与 SRB\_函数\_锁定\_队列），用于阻止未同步的操作，直到电源操作（可能涉及几个步骤）完成。 发出的用于处理电源操作的任何 SRBs 都应将 SRB\_标志设置\_绕过\_锁定\_队列，以确保它们达到端口驱动程序。 驱动程序完成设置电源状态后，它应解锁队列（IRP\_MJ\_SCSI 与 SRB\_函数\_解锁\_QUEUE 和 SRB\_标志\_绕过\_锁定\_队列）设备启动后，端口驱动程序可以继续将已排队的 Irp 发送到设备。

如果存储类驱动程序具有*StartIo*例程，该例程会处理同步，因此类驱动程序不必显式锁定和解锁端口驱动程序的 LU 特定队列。

类驱动程序不应尝试绕过其他驱动程序锁定的队列。

 

 




