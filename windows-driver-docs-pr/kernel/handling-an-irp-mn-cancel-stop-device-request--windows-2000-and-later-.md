---
title: 处理 IRP_MN_CANCEL_STOP_DEVICE 请求（Windows 2000 和更高版本）
description: 处理 IRP_MN_CANCEL_STOP_DEVICE 请求（Windows 2000 和更高版本）
ms.assetid: 2e5e835f-d327-4bde-bdfd-8a71a47b0ac0
keywords:
- IRP_MN_CANCEL_STOP_DEVICE
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: a00352d48f30fa25d8715f1f5e0ba161881ff458
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359808"
---
# <a name="handling-an-irpmncancelstopdevice-request-windows-2000-and-later"></a>处理 IRP\_MN\_取消\_停止\_设备请求 (Windows 2000 及更高版本)





[ **IRP\_MN\_取消\_停止\_设备**](https://msdn.microsoft.com/library/windows/hardware/ff550826)按设备父总线驱动程序，然后按每个下一步必须首先处理请求更高版本设备堆栈中的驱动程序。 驱动程序句柄停止 Irp 中的其[ *DispatchPnP* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程。

以响应**IRP\_MN\_取消\_停止\_设备**请求时，驱动程序必须将设备恢复为其已启动状态并继续正常操作。 驱动程序必须成功取消停止 IRP。

驱动程序处理**IRP\_MN\_取消\_停止\_设备**请求的过程如下所示：

1.  推迟重新启动设备，直到低级驱动程序已完成其重启操作。 (请参阅[低级驱动程序完成之前推迟 PnP IRP 处理](postponing-pnp-irp-processing-until-lower-drivers-finish.md)。)

2.  较低的驱动程序完成后，将设备恢复为其已启动状态。

    具体操作取决于设备和驱动程序。

3.  启动 Irp IRP 控股队列中。

    如果设备处于停止挂起状态时，驱动程序已保存请求，清除保留\_新建\_请求标志和启动 Irp IRP 控股队列中。 请参阅[持有传入 Irp 时设备暂停](holding-incoming-irps-when-a-device-is-paused.md)有关详细信息。

4.  完成与 IRP [ **IoCompleteRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548343)。

    -   在函数或筛选器驱动程序：

        在驱动程序[ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354)例程返回状态\_详细\_处理\_必需的如中所述[推迟 PnP IRP处理直到较低的驱动程序完成](postponing-pnp-irp-processing-until-lower-drivers-finish.md)，因此驱动程序的*DispatchPnP*例程必须调用**IoCompleteRequest**恢复 I/O 完成处理。

        驱动程序集**Irp-&gt;IoStatus.Status**于状态\_成功后，调用**IoCompleteRequest** IO 优先级提升与\_否\_增量，并返回状态\_成功从其*DispatchPnP*例程。

        驱动程序不得失败此操作。 如果驱动程序失败重启 IRP，设备处于不一致状态，并将无法正常运行。

    -   在父总线驱动程序：

        驱动程序集**Irp-&gt;IoStatus.Status**于状态\_成功和调用**IoCompleteRequest**指定的 IO 优先级提升\_否\_增量。 总线驱动程序将返回状态\_成功从其*DispatchPnP*例程。

        总线驱动程序不得失败此操作。 如果驱动程序失败重启 IRP，设备处于不一致状态，并将无法正常运行。

当设备启动并处于活动状态时，驱动程序可能会收到虚假取消停止请求。 此问题，例如，如果该驱动程序 （或更高版本设备堆栈中的驱动程序） 故障[ **IRP\_MN\_查询\_停止\_设备**](https://msdn.microsoft.com/library/windows/hardware/ff551725)请求。 设备已启动并处于活动状态时，驱动程序可以安全地成功设备的虚假取消停止的请求。

 

 




