---
title: 处理 IRP_MN_CANCEL_STOP_DEVICE 请求 (Windows 98/Me)
description: 处理 IRP_MN_CANCEL_STOP_DEVICE 请求 (Windows 98/Me)
ms.assetid: 04365c65-a68a-48fc-9f7a-bb005518be5b
keywords:
- IRP_MN_CANCEL_STOP_DEVICE
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: a2b9d746f2b33a3ec3b2964d5d8fad2c7a1a184b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836608"
---
# <a name="handling-an-irp_mn_cancel_stop_device-request-windows-98me"></a>处理 IRP\_MN\_取消\_停止\_设备请求（Windows 98/Me）





[**IRP\_MN\_CANCEL\_停止\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-cancel-stop-device)请求必须首先由设备的父总线驱动程序处理，然后再由设备堆栈中的每个较高的驱动程序处理。 驱动程序处理其[*DispatchPnP*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)例程中的停止 irp。

为了响应**IRP\_MN\_CANCEL\_停止\_设备**请求，驱动程序必须将设备恢复到其已启动状态并恢复正常操作。 驱动程序必须成功完成取消-停止 IRP。

驱动程序处理**IRP\_MN\_CANCEL\_停止\_设备**请求，步骤如下：

1.  在较低的驱动程序完成其重新启动操作之前，请推迟重新启动设备。 （请参阅[推迟 PNP IRP 处理，直到驱动程序的驱动程序完成](postponing-pnp-irp-processing-until-lower-drivers-finish.md)。）

2.  在较低的驱动程序完成后，将设备恢复到其启动状态。

    具体操作取决于设备和驱动程序。

3.  重新启动 i/o。

4.  完成 IRP with [**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)。

    -   在函数或筛选器驱动程序中：

        驱动程序的*IoCompletion*例程返回状态\_\_需要更多的\_处理，如[推迟 PnP IRP 处理直到较低的驱动程序完成](postponing-pnp-irp-processing-until-lower-drivers-finish.md)，因此驱动程序的*DispatchPnP*例程必须调用**IoCompleteRequest**恢复 i/o 完成处理。

        驱动程序将**Irp&gt;IoStatus**的状态设置为 STATUS\_SUCCESS，调用**IoCompleteRequest** ，并且优先级提升为 IO\_no\_增量，并从其*DISPATCHPNP*例程返回状态\_SUCCESS。

        驱动程序不能使此操作失败。 如果驱动程序未能重新启动 IRP，则设备处于不一致状态，并且不会正常运行。

    -   在父总线驱动程序中：

        驱动程序将**Irp&gt;IoStatus**设置为 STATUS\_SUCCESS，并调用**IOCOMPLETEREQUEST**来指定 IO\_无\_增量的优先级提升。 总线驱动程序从其*DispatchPnP*例程返回状态\_成功。

        总线驱动程序不能使此操作失败。 如果驱动程序未能重新启动 IRP，则设备处于不一致状态，并且不会正常运行。

设备启动并处于活动状态时，驱动程序可能会收到虚假的取消-停止请求。 例如，如果驱动程序（或设备堆栈中较高版本的驱动程序）无法进行[**IRP\_MN\_QUERY\_停止\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-stop-device)请求，则可能会发生这种情况。 设备启动并处于活动状态时，驱动程序可以安全地成功为设备执行虚假的取消停止请求。

 

 




