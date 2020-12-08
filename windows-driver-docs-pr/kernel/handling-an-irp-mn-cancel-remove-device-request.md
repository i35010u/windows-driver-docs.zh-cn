---
title: 处理 IRP_MN_CANCEL_REMOVE_DEVICE 请求
description: 处理 IRP_MN_CANCEL_REMOVE_DEVICE 请求
keywords:
- IRP_MN_CANCEL_REMOVE_DEVICE
- 虚假取消-删除请求 WDK PnP
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: e9303b2dc97060f5f8220cb59e5ee3efabc6f190
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838025"
---
# <a name="handling-an-irp_mn_cancel_remove_device-request"></a>处理 IRP \_ MN \_ 取消 \_ 删除 \_ 设备请求





为了响应 [**irp \_ MN \_ CANCEL \_ remove \_ device**](./irp-mn-cancel-remove-device.md) 请求，设备的驱动程序必须将设备返回到接收 **IRP \_ MN \_ 查询 \_ 删除 \_ 设备** 请求之前的状态。 通常，驱动程序会将设备恢复到 "已启动" 状态。

除了将 **irp \_ MN \_ CANCEL \_ REMOVE \_ 设备** 发送到设备之外，PNP 管理器还会将 irp 发送到设备的删除关系（如果有）。 PnP 管理器还会将取消-删除 IRP 发送到设备的子项。

当 **IRP \_ MN " \_ 取消 \_ 删除 \_ 设备**" 请求完成后，PnP 管理器会调用任何 **EventCategoryTargetDeviceChange** 通知回调。 此类回调是通过调用 [**IoRegisterPlugPlayNotification**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterplugplaynotification)在设备上注册的。 PnP 管理器还通过调用 **RegisterDeviceNotification** 调用为此类通知注册的任何用户模式组件。

必须首先由设备的父总线驱动程序和设备堆栈中的每个更高的驱动程序处理 **IRP \_ MN \_ CANCEL \_ REMOVE \_ DEVICE** 请求。 驱动程序会在其 [*DispatchPnP*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) 例程中处理删除 irp。

驱动程序使用以下过程处理 **IRP \_ MN \_ CANCEL \_ REMOVE \_ DEVICE** 请求： *DispatchPnP* 例程：

1.  在函数或筛选器驱动程序中，推迟重新启动设备，直到驱动程序完成其重新启动操作。

    函数或筛选器驱动程序设置 [*IoCompletion*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine) 例程，将 **irp \_ MN " \_ 取消 \_ 删除 \_ 设备** " 关闭设备堆栈，并推迟其重启操作，直到所有较低版本的驱动程序都已完成 IRP。  (请参阅 [推迟 PNP IRP 处理，直到驱动程序的驱动程序完成](postponing-pnp-irp-processing-until-lower-drivers-finish.md)。 ) 

2.  在较低的驱动程序完成后，将设备恢复为其以前的 PnP 状态。

    驱动程序将设备恢复为接收 **IRP \_ MN \_ 查询 \_ 删除 \_ 设备** 请求之前的状态。 通常，驱动程序会将设备恢复到 "已启动" 状态。 具体操作取决于设备和驱动程序。

    如果先前为设备启用了唤醒，则设备电源策略所有者通常 (功能驱动程序) 应发送 [**IRP \_ MN \_ 等待 \_ 唤醒**](./irp-mn-wait-wake.md) 请求以重新启用唤醒。 有关详细信息，请参阅 [电源管理](./introduction-to-power-management.md) 。

3.  将 **irp- &gt; IoStatus** 设置为状态 \_ 成功，并通过 [**IoCompleteRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)完成 Irp。

    与任何 PnP IRP 一样，总线驱动程序完成 IRP。

    函数或筛选器驱动程序还完成 IRP，在这种情况下，原因是驱动程序的 *IoCompletion* 例程通过返回状态 " \_ 需要更多的处理" 来中断完成处理 \_ \_ 。

    驱动程序必须成功此 IRP。 如果任何驱动程序未通过此 IRP，则设备处于不一致状态。

设备启动并处于活动状态时，驱动程序可能会收到虚假的取消删除请求。 例如，如果驱动程序 (或设备堆栈中较高版本的驱动程序，则可能会发生这种情况) **IRP \_ MN \_ 查询 \_ 删除 \_ 设备** 请求。 设备启动并处于活动状态时，驱动程序只是对设备成功执行虚假的取消删除请求。

 

