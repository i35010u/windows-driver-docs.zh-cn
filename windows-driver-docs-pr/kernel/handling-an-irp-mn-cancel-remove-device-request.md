---
title: 处理 IRP_MN_CANCEL_REMOVE_DEVICE 请求
description: 处理 IRP_MN_CANCEL_REMOVE_DEVICE 请求
ms.assetid: 3382c47d-6ac8-409e-b558-ad2f2ae83715
keywords:
- IRP_MN_CANCEL_REMOVE_DEVICE
- 虚假的取消删除请求 WDK 即插即用
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3577ee383671247ae468f2c3a363a79a30252cf9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577270"
---
# <a name="handling-an-irpmncancelremovedevice-request"></a>处理 IRP\_MN\_取消\_删除\_设备请求





以响应[ **IRP\_MN\_取消\_删除\_设备**](https://msdn.microsoft.com/library/windows/hardware/ff550823)请求，驱动程序的设备必须将设备恢复为它所处的状态在接收之前**IRP\_MN\_查询\_删除\_设备**请求。 通常情况下，驱动程序将设备恢复为已启动状态。

除了发送**IRP\_MN\_取消\_删除\_设备**到设备，即插即用管理器将发送 IRP 到设备的删除关系，如果有的话。 PnP 管理器还将取消删除 IRP 发送到设备的子级。

PnP 管理器会调用任何**EventCategoryTargetDeviceChange**后的通知回调**IRP\_MN\_取消\_删除\_设备**请求完成。 通过调用在设备上注册此类回调[ **IoRegisterPlugPlayNotification**](https://msdn.microsoft.com/library/windows/hardware/ff549526)。 PnP 管理器注册任何用户模式组件还要求对此类通知上，通过调用**RegisterDeviceNotification**。

**IRP\_MN\_取消\_删除\_设备**依次按设备父总线驱动程序和设备堆栈中每个更高版本的驱动程序必须首先处理请求。 驱动程序句柄删除 Irp 中的其[ *DispatchPnP* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程。

驱动程序处理**IRP\_MN\_取消\_删除\_设备**如下所示中的过程包含请求其*DispatchPnP*例程：

1.  在函数或筛选器驱动程序中，推迟重新启动设备，直到低级驱动程序已完成其重启操作。

    函数或筛选器驱动程序设置[ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354)例程，传递**IRP\_MN\_取消\_删除\_设备**设备堆栈，并推迟重新启动操作，直到 IRP 用完所有较低的驱动程序。 (请参阅[低级驱动程序完成之前推迟 PnP IRP 处理](postponing-pnp-irp-processing-until-lower-drivers-finish.md)。)

2.  较低的驱动程序完成后，将设备恢复为以前的即插即用状态。

    驱动程序将设备恢复为之前接收的状态**IRP\_MN\_查询\_删除\_设备**请求。 通常情况下，驱动程序将设备恢复为已启动状态。 具体操作取决于设备和驱动程序。

    如果先前已对唤醒设备，设备电源策略所有者 （通常是功能驱动程序） 应发送[ **IRP\_MN\_等待\_唤醒**](https://msdn.microsoft.com/library/windows/hardware/ff551766)若要重新启用唤醒的请求。 请参阅[电源管理](implementing-power-management.md)有关详细信息。

3.  设置**Irp-&gt;IoStatus.Status**于状态\_成功并完成与 IRP [ **IoCompleteRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548343)。

    与任何 PnP IRP，总线驱动程序完成 IRP。

    函数或筛选器驱动程序还将完成 IRP，在这种情况下由于驱动程序的*IoCompletion*例程中断完成处理通过返回状态\_详细\_处理\_必填。

    驱动程序必须成功完成此 IRP。 如果任何驱动程序失败时此 IRP，设备是处于不一致的状态。

当设备启动并处于活动状态时，驱动程序可能会收到虚假的取消删除请求。 此问题，例如，如果该驱动程序 （或更高版本设备堆栈中的驱动程序） 故障**IRP\_MN\_查询\_删除\_设备**请求。 设备已启动并处于活动状态时，驱动程序只需成功在设备的虚假的取消删除请求。

 

 




