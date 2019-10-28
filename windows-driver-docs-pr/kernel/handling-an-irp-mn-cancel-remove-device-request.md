---
title: 处理 IRP_MN_CANCEL_REMOVE_DEVICE 请求
description: 处理 IRP_MN_CANCEL_REMOVE_DEVICE 请求
ms.assetid: 3382c47d-6ac8-409e-b558-ad2f2ae83715
keywords:
- IRP_MN_CANCEL_REMOVE_DEVICE
- 虚假取消-删除请求 WDK PnP
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 96a9c06ef0d83e5b64ff26aa597e347f0f65c514
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836603"
---
# <a name="handling-an-irp_mn_cancel_remove_device-request"></a>处理 IRP\_MN\_取消\_删除\_设备请求





为了响应[**IRP\_MN\_取消\_删除\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-cancel-remove-device)请求，设备的驱动程序必须将设备恢复为接收**IRP\_MN\_查询\_删除 @no__ 之前的状态。t_10_ 设备**请求。 通常，驱动程序会将设备恢复到 "已启动" 状态。

除了发送**irp\_MN\_取消\_删除设备\_设备**，PnP 管理器会将 IRP 发送到设备的删除关系（如果有）。 PnP 管理器还会将取消-删除 IRP 发送到设备的子项。

当**IRP\_MN\_取消\_删除\_设备**请求完成后，PnP 管理器会调用任何**EventCategoryTargetDeviceChange**通知回调。 此类回调是通过调用[**IoRegisterPlugPlayNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterplugplaynotification)在设备上注册的。 PnP 管理器还通过调用**RegisterDeviceNotification**调用为此类通知注册的任何用户模式组件。

**IRP\_MN\_取消\_删除\_设备**请求必须首先由设备的父总线驱动程序处理，然后由设备堆栈中的每个更高的驱动程序处理。 驱动程序会在其[*DispatchPnP*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)例程中处理删除 irp。

驱动程序处理**IRP\_MN\_CANCEL\_删除\_设备**请求，并在其*DispatchPnP*例程中使用如下所示的过程：

1.  在函数或筛选器驱动程序中，推迟重新启动设备，直到驱动程序完成其重新启动操作。

    函数或筛选器驱动程序设置[*IoCompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)例程，传递**IRP\_MN\_取消\_删除设备堆栈\_设备**，并推迟其重启操作，直到所有较低版本的驱动程序都完成了IRP. （请参阅[推迟 PNP IRP 处理，直到驱动程序的驱动程序完成](postponing-pnp-irp-processing-until-lower-drivers-finish.md)。）

2.  在较低的驱动程序完成后，将设备恢复为其以前的 PnP 状态。

    驱动程序将设备恢复到在接收**IRP\_MN\_查询之前的状态，\_删除\_设备**请求。 通常，驱动程序会将设备恢复到 "已启动" 状态。 具体操作取决于设备和驱动程序。

    如果先前为设备启用了唤醒，则设备电源策略所有者（通常是函数驱动程序）应发送[**IRP\_MN\_等待\_唤醒**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-wait-wake)请求重新启动。 有关详细信息，请参阅[电源管理](implementing-power-management.md)。

3.  将**irp&gt;IoStatus**设置为 STATUS\_SUCCESS，并通过[**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)完成 Irp。

    与任何 PnP IRP 一样，总线驱动程序完成 IRP。

    函数或筛选器驱动程序还完成 IRP，在这种情况下，原因是驱动程序的*IoCompletion*例程通过返回\_状态来中断完成处理\_需要更多的\_处理。

    驱动程序必须成功此 IRP。 如果任何驱动程序未通过此 IRP，则设备处于不一致状态。

设备启动并处于活动状态时，驱动程序可能会收到虚假的取消删除请求。 例如，如果驱动程序（或设备堆栈中较高版本的驱动程序）无法进行**IRP\_MN\_QUERY\_删除\_设备**请求，则可能会发生这种情况。 设备启动并处于活动状态时，驱动程序只是对设备成功执行虚假的取消删除请求。

 

 




