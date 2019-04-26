---
title: 处理对存储外设的电源请求
description: 处理对存储外设的电源请求
ms.assetid: 3cc7b885-27ad-4384-aeec-4d76f9ad4f1c
keywords:
- 外围设备 WDK 存储、 电源请求
- 存储外围设备 WDK、 电源请求
- power 请求 WDK 存储
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 447676b22443a19eb4565e95a14355210eb66a82
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325943"
---
# <a name="handling-power-requests-to-storage-peripherals"></a>处理对存储外设的电源请求


## <span id="ddk_handling_power_requests_to_storage_peripherals_kg"></span><span id="DDK_HANDLING_POWER_REQUESTS_TO_STORAGE_PERIPHERALS_KG"></span>


存储类驱动程序将负责发出特定于设备的命令来处理电源请求。 大多数情况下，存储类驱动程序：

-   到其设备以响应查询能耗请求阻止 I/O (IRP\_MJ\_具有 POWER [ **IRP\_MN\_查询\_POWER**](https://msdn.microsoft.com/library/windows/hardware/ff551699)) 如果处理此类 I/O 可能会阻止驱动程序中合理的时间内成功集 power 请求

-   在对集 power 请求的响应中设置其设备的电源状态 (IRP\_MJ\_具有 POWER [ **IRP\_MN\_设置\_POWER**](https://msdn.microsoft.com/library/windows/hardware/ff551744))

-   将 I/O 重新启动到其设备以响应集 power 请求，以在设备接通电源

-   Power 将请求转发到下一步低驱动程序。

请注意，驱动程序必须调用[ **PoStartNextPowerIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff559776)并[ **PoCallDriver**](https://msdn.microsoft.com/library/windows/hardware/ff559654)，而不**IoCallDriver**，以发送电源请求。

除非具有存储类驱动程序[ **StartIo** ](https://msdn.microsoft.com/library/windows/hardware/ff563858)例程，它应锁定存储端口驱动程序的特定于 LU 的队列 (IRP\_MJ\_SRB 使用 SCSI\_函数\_锁\_队列) 之前设置设备的电源状态 （这可能涉及几个步骤） 电源操作完成之前阻止未同步的操作。 为处理电源操作而发出任何 Srb 应设置 SRB\_标志\_绕过\_锁定\_队列以确保到达端口驱动程序。 该驱动程序完成设置电源状态后，它应解锁队列 (IRP\_MJ\_SRB 使用 SCSI\_函数\_解锁\_队列和 SRB\_标志\_绕过\_锁定\_队列)，以便端口驱动程序可以向设备发送排队的 Irp，一旦启动后恢复。

如果存储类驱动程序具有*StartIo*例程，该例程处理同步因此类驱动程序不需要显式锁定和解锁端口驱动程序的特定于 LU 的队列。

类驱动程序不应尝试绕过其他驱动程序被锁定的队列。

 

 




