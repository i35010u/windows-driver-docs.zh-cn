---
title: 处理对存储外设的电源请求
description: 处理对存储外设的电源请求
keywords:
- 外围设备 WDK 存储，电源请求
- 存储外围设备 WDK，电源请求
- power requests WDK 存储
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eee06f8eb9c53b415be99cfb1e04613d66a7acaa
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96804527"
---
# <a name="handling-power-requests-to-storage-peripherals"></a>处理对存储外设的电源请求


## <span id="ddk_handling_power_requests_to_storage_peripherals_kg"></span><span id="DDK_HANDLING_POWER_REQUESTS_TO_STORAGE_PERIPHERALS_KG"></span>


存储类驱动程序负责发出用于处理电源请求的特定于设备的命令。 最常见的存储类驱动程序：

-   阻止对其设备的 i/o，以响应查询-电源请求 (IRP \_ MJ \_ Power with [**irp \_ MN \_ query \_ power**](../kernel/irp-mn-query-power.md)) 如果处理此类 i/o 可能会阻止驱动程序在合理的时间内成功处理集电源请求

-   设置其设备的电源状态，以响应 (IRP \_ MJ \_ Power with [**irp \_ MN \_ 设置 \_ power**](../kernel/irp-mn-set-power.md)) 的设置电源请求

-   重新启动其设备的 i/o，以响应设置电源请求以打开设备

-   将电源请求转发到下一个较低的驱动程序。

请注意，驱动程序必须调用 [**PoStartNextPowerIrp**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-postartnextpowerirp) 和 [**PoCallDriver**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver)，而不是 **IoCallDriver** 来发送 power 请求。

除非存储类驱动程序具有 [**StartIo**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio) 例程，否则它应在设置设备的电源状态之前，将存储端口驱动程序的 LU 特定的队列 (IRP \_ MJ \_ SCSI \_) 锁定 \_ \_ ，以阻止未同步的操作，直到电源操作 (其中可能涉及几个步骤) 完成。 发出的用于处理电源操作的任何 SRBs 应将 SRB \_ 标志设置 \_ 为绕过 \_ 锁定 \_ 队列，确保它们到达端口驱动程序。 驱动程序完成设置电源状态后，它应将队列解锁 (IRP \_ MJ \_ SCSI with SRB \_ FUNCTION \_ unlock \_ queue，并使用 SRB \_ FLAGS \_ 旁路 \_ 锁定 \_) 队列，以使端口驱动程序可以在设备通电后恢复向设备发送已排队的 irp。

如果存储类驱动程序具有 *StartIo* 例程，该例程会处理同步，因此类驱动程序不必显式锁定和解锁端口驱动程序的 LU 特定队列。

类驱动程序不应尝试绕过其他驱动程序锁定的队列。

 

