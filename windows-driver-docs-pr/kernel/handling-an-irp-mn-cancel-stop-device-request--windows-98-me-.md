---
title: 处理 IRP_MN_CANCEL_STOP_DEVICE 请求 (Windows 98/Me)
description: 处理 IRP_MN_CANCEL_STOP_DEVICE 请求 (Windows 98/Me)
ms.assetid: 04365c65-a68a-48fc-9f7a-bb005518be5b
keywords:
- IRP_MN_CANCEL_STOP_DEVICE
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 38793feb6e7d643aef4fe9ed36db2123cdb04952
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575496"
---
# <a name="handling-an-irpmncancelstopdevice-request-windows-98me"></a>处理 IRP\_MN\_取消\_停止\_设备请求 (Windows 98 / 我)





[ **IRP\_MN\_取消\_停止\_设备**](https://msdn.microsoft.com/library/windows/hardware/ff550826)按设备父总线驱动程序，然后按每个下一步必须首先处理请求更高版本设备堆栈中的驱动程序。 驱动程序句柄停止 Irp 中的其[ *DispatchPnP* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程。

以响应**IRP\_MN\_取消\_停止\_设备**请求时，驱动程序必须将设备恢复为其已启动状态并继续正常操作。 驱动程序必须成功取消停止 IRP。

驱动程序处理**IRP\_MN\_取消\_停止\_设备**请求的过程如下所示：

1.  推迟重新启动设备，直到低级驱动程序已完成其重启操作。 (请参阅[低级驱动程序完成之前推迟 PnP IRP 处理](postponing-pnp-irp-processing-until-lower-drivers-finish.md)。)

2.  较低的驱动程序完成后，将设备恢复为其已启动状态。

    具体操作取决于设备和驱动程序。

3.  重新启动 I/O。

4.  完成与 IRP [ **IoCompleteRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548343)。

    -   在函数或筛选器驱动程序：

        在驱动程序*IoCompletion*例程返回状态\_详细\_处理\_必需的如中所述[推迟 PnP IRP 处理直到较低的驱动程序完成](postponing-pnp-irp-processing-until-lower-drivers-finish.md)，因此驱动程序的*DispatchPnP*例程必须调用**IoCompleteRequest**恢复 I/O 完成处理。

        驱动程序集**Irp-&gt;IoStatus.Status**于状态\_成功后，调用**IoCompleteRequest** IO 优先级提升与\_否\_增量，并返回状态\_成功从其*DispatchPnP*例程。

        驱动程序不得失败此操作。 如果驱动程序失败重启 IRP，设备处于不一致状态，并将无法正常运行。

    -   在父总线驱动程序：

        驱动程序集**Irp-&gt;IoStatus.Status**于状态\_成功和调用**IoCompleteRequest**指定的 IO 优先级提升\_否\_增量。 总线驱动程序将返回状态\_成功从其*DispatchPnP*例程。

        总线驱动程序不得失败此操作。 如果驱动程序失败重启 IRP，设备处于不一致状态，并将无法正常运行。

当设备启动并处于活动状态时，驱动程序可能会收到虚假取消停止请求。 此问题，例如，如果该驱动程序 （或更高版本设备堆栈中的驱动程序） 故障[ **IRP\_MN\_查询\_停止\_设备**](https://msdn.microsoft.com/library/windows/hardware/ff551725)请求。 设备已启动并处于活动状态时，驱动程序可以安全地成功设备的虚假取消停止的请求。

 

 




