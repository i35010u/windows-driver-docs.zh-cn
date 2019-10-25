---
title: 多组件设备，一种或多种功能电源状态
description: 支持多组件设备呈现单个或多个功能性电源状态
ms.assetid: D601A0F6-A035-4161-879A-D495518E7EC6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 41094f0608b3bdc87b25cbca6158680517ad1c26
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831740"
---
# <a name="supporting-multiple-component-devices-with-single-or-multiple-functional-power-states"></a>支持多组件设备呈现单个或多个功能性电源状态


\[仅适用于 KMDF\]

多组件设备的 KMDF 驱动程序可以定义每个组件的一个或多个功能电源状态。

在这种情况下，驱动程序会直接注册电源管理框架（PoFx）。 若要指定 WDF 不应向 PoFx 注册，驱动程序将调用[**WdfDeviceAssignS0IdleSettings**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceassigns0idlesettings) ，并将 IdleTimeoutType 成员与 WDF\_设备的成员一起调用[ **\_POWER\_策略\_空闲\_设置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/ns-wdfdevice-_wdf_device_power_policy_idle_settings)结构设置为**DriverManagedIdleTimeout**。 通常，驱动程序从其[*EvtDriverDeviceAdd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)回调函数调用此方法。

接下来，驱动程序必须注册到 PoFx。 为此，驱动程序将调用[**PoFxRegisterDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxregisterdevice) ，然后调用[**PoFxStartDevicePowerManagement**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxstartdevicepowermanagement)。 设备首次启动时，驱动程序必须仅向 PoFx 注册一次。 实现此目的的一种方法是从驱动程序提供的[*EvtDeviceSelfManagedIoInit*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_init)函数调用这些例程。 仅在设备首次启动时调用*EvtDeviceSelfManagedIoInit* 。

删除设备后，驱动程序必须调用[**PoFxUnregisterDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxunregisterdevice)以从 PoFx 取消注册设备。 若要仅注销一次，建议从驱动程序提供的[*EvtDeviceSelfManagedIoFlush*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_flush)函数调用此例程。 仅当删除设备时，才会调用*EvtDeviceSelfManagedIoFlush* 。 通过在*EvtDeviceSelfManagedIoFlush*中注销，驱动程序会在睡眠和重新平衡转换期间保留电源注册，并且无需维护在这些转换过程中保持挂起状态的 i/o 请求的 power 引用。

当驱动程序调用[*PoFxRegisterDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_post_po_fx_register_device)时，它会收到一个可用于与 PoFx 直接交互的 power registration 控点（POHANDLE），如以下主题中所述：

-   [协调组件电源状态的 i/o 请求](coordinating-i-o-requests-with-component-power-state.md)
-   [系统返回到 S0 时打开的报告设备](reporting-device-powered-on.md)
-   [支持多组件设备的空闲关机](supporting-idle-power-down-on-multiple-component-devices.md)

此外，驱动程序还可以直接调用[power framework 例程](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)来发送电源控制请求并指定延迟、常驻和唤醒要求。

有关 PoFx 的详细信息，请参阅[电源管理框架概述](https://docs.microsoft.com/windows-hardware/drivers/kernel/overview-of-the-power-management-framework)。

 

 





