---
title: 框架中的状态计算机
description: 框架中的状态计算机
ms.assetid: 5ef307c6-0310-4a83-a63f-3a6d96782013
keywords:
- 即插即用 WDK KMDF，状态机
- 插 WDK KMDF，状态机
- 电源管理 WDK KMDF，状态机
- 状态机 WDK KMDF
- 指出 WDK KMDF
- 即插即用的状态机 WDK KMDF
- 电源状态 WDK KMDF
- 当前状态计算机状态 WDK KMDF
- WDK KMDF，状态机的状态信息
- 电源策略 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ca35d5f5137392ec3937ebef6ce251e21ea68d75
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376177"
---
# <a name="state-machines-in-the-framework"></a>框架中的状态计算机


若要跟踪的每个设备的状态，框架将使用即插即用的状态机、 电源状态机和电源策略状态机。 框架将创建每个设备都插入到系统每个状态机的实例。

>[!NOTE]
>此功能是仅供 Microsoft 内部使用。

对于确实需要了解此信息的驱动程序，framework 提供了两个集的接口：

-   一组驱动程序所提供事件回调函数。

    该驱动程序可以请求 framework 调用一个以下回调的函数的一个状态机将进入或退出某一特定状态时：

    -   [*EvtDevicePnpStateChange*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_pnp_state_change_notification)，该驱动程序将通过调用其注册[ **WdfDeviceInitRegisterPnpStateChangeCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitregisterpnpstatechangecallback)。
    -   [*EvtDevicePowerStateChange*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_power_state_change_notification)，该驱动程序将通过调用其注册[ **WdfDeviceInitRegisterPowerStateChangeCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitregisterpowerstatechangecallback)。
    -   [*EvtDevicePowerPolicyStateChange*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_power_policy_state_change_notification)，该驱动程序将通过调用其注册[ **WdfDeviceInitRegisterPowerPolicyStateChangeCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitregisterpowerpolicystatechangecallback)。
-   一组返回的状态机的当前状态的方法。

    该驱动程序可以调用以下方法之一来确定某个特定设备的状态机的当前状态：

    -   [**WdfDeviceGetDevicePnpState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicegetdevicepnpstate)
    -   [**WdfDeviceGetDevicePowerState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicegetdevicepowerstate)
    -   [**WdfDeviceGetDevicePowerPolicyState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicegetdevicepowerpolicystate)

 

 





