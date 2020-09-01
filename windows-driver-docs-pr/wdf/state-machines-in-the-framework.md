---
title: 框架中的状态计算机
description: 框架中的状态计算机
ms.assetid: 5ef307c6-0310-4a83-a63f-3a6d96782013
keywords:
- PnP WDK KMDF，状态机
- 即插即用 WDK KMDF，状态机
- 电源管理 WDK KMDF，状态机
- 状态机 WDK KMDF
- 状态 WDK KMDF
- PnP 状态机 WDK KMDF
- 电源状态 WDK KMDF
- 当前状态机状态 WDK KMDF
- 状态信息 WDK KMDF，状态机
- 电源策略 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 292c88e584a4228366f3b3f4258b503a9b5a85a6
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89190817"
---
# <a name="state-machines-in-the-framework"></a>框架中的状态计算机


为了跟踪每个设备的状态，框架使用 PnP 状态机、电源状态机和电源策略状态机。 框架为插到系统中的每个设备创建每个状态机的实例。

>[!NOTE]
>此功能仅供 Microsoft 内部使用。

对于确实需要知道此信息的驱动程序，该框架提供了两组接口：

-   一组由驱动程序提供的事件回调函数。

    此驱动程序可以在其中一个状态机进入或退出某一状态时，请求框架调用以下回调函数之一：

    -   [*EvtDevicePnpStateChange*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_pnp_state_change_notification)，驱动程序通过调用 [**WdfDeviceInitRegisterPnpStateChangeCallback**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitregisterpnpstatechangecallback)来注册。
    -   [*EvtDevicePowerStateChange*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_power_state_change_notification)，驱动程序通过调用 [**WdfDeviceInitRegisterPowerStateChangeCallback**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitregisterpowerstatechangecallback)来注册。
    -   [*EvtDevicePowerPolicyStateChange*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_power_policy_state_change_notification)，驱动程序通过调用 [**WdfDeviceInitRegisterPowerPolicyStateChangeCallback**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitregisterpowerpolicystatechangecallback)来注册。
-   返回状态机的当前状态的一组方法。

    驱动程序可以调用以下方法之一来确定特定设备的某个状态机的当前状态：

    -   [**WdfDeviceGetDevicePnpState**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicegetdevicepnpstate)
    -   [**WdfDeviceGetDevicePowerState**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicegetdevicepowerstate)
    -   [**WdfDeviceGetDevicePowerPolicyState**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicegetdevicepowerpolicystate)

 

