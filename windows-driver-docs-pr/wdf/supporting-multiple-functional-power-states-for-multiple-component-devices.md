---
title: 多个组件设备、 一个或多个功能的电源状态
description: 支持多组件设备呈现单个或多个功能性电源状态
ms.assetid: D601A0F6-A035-4161-879A-D495518E7EC6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4f561c851486b2148b687f119383b7c73a44c648
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368077"
---
# <a name="supporting-multiple-component-devices-with-single-or-multiple-functional-power-states"></a>支持多组件设备呈现单个或多个功能性电源状态


\[仅适用于 KMDF\]

多个组件设备的 KMDF 驱动程序可以定义每个组件的一个或多个功能的电源的状态。

在这种情况下，该驱动程序直接与电源管理框架 (PoFx) 注册。 若要指定，WDF 不应注册与 PoFx，驱动程序调用[ **WdfDeviceAssignS0IdleSettings** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceassigns0idlesettings)与**IdleTimeoutType**隶属[**WDF\_设备\_POWER\_策略\_空闲\_设置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/ns-wdfdevice-_wdf_device_power_policy_idle_settings)结构设置为**DriverManagedIdleTimeout**. 通常情况下，该驱动程序调用此方法从其[ *EvtDriverDeviceAdd* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)回调函数。

接下来，驱动程序必须向 PoFx 注册。 若要执行此操作，驱动程序调用[ **PoFxRegisterDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pofxregisterdevice) ，然后[ **PoFxStartDevicePowerManagement**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pofxstartdevicepowermanagement)。 您的驱动程序必须注册 PoFx 只有一次设备首次启动时。 这是通过调用这些例程从驱动程序提供一个方法可以解决[ *EvtDeviceSelfManagedIoInit* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_init)函数。 *EvtDeviceSelfManagedIoInit*调用仅在首次启动设备。

该驱动程序时删除该设备，必须调用[ **PoFxUnregisterDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pofxunregisterdevice)注销 PoFx 的设备。 若要取消注册仅一次，我们建议的驱动程序调用从驱动程序提供此例程[ *EvtDeviceSelfManagedIoFlush* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_flush)函数。 *EvtDeviceSelfManagedIoFlush*正在删除设备时才调用。 通过在注销*EvtDeviceSelfManagedIoFlush*、 驱动程序在睡眠期间保留 power 注册和重新平衡转换，并且无需维护 power 引用保持挂起的 I/O 请求期间这些进行的转换。

当驱动程序调用[ *PoFxRegisterDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_post_po_fx_register_device)，接收它可用于直接交互 PoFx，如以下主题中所述的电源注册句柄 (POHANDLE):

-   [协调与组件电源状态的 I/O 请求](coordinating-i-o-requests-with-component-power-state.md)
-   [报告设备开机时系统将恢复为 S0](reporting-device-powered-on.md)
-   [支持在多个组件的设备上的空闲状态的电源关闭](supporting-idle-power-down-on-multiple-component-devices.md)

此外，驱动程序可以调用[电源 framework 例程](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)直接以发送电源控制请求并指定延迟，驻留和唤醒要求。

有关 PoFx 详细信息，请参阅[电源管理框架概述](https://docs.microsoft.com/windows-hardware/drivers/kernel/overview-of-the-power-management-framework)。

 

 





