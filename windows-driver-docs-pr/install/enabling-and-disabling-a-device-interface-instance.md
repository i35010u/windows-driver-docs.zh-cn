---
title: 启用和禁用设备接口实例
description: 启用和禁用设备接口实例
ms.assetid: 4e3341c2-ba95-458e-8d92-a35545a773e0
keywords:
- 接口类 WDK 设备安装
- 禁用设备接口实例
- IoSetDeviceInterfaceState
- 设备接口类 WDK 设备安装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 098ee2e4eb58e90eff81f567acc1fcce30003b6b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840638"
---
# <a name="enabling-and-disabling-a-device-interface-instance"></a>启用和禁用设备接口实例





成功启动设备后，注册接口的驱动程序将调用[**IoSetDeviceInterfaceState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetdeviceinterfacestate)来启用接口实例。 驱动程序将[**IoRegisterDeviceInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterdeviceinterface)返回的符号链接名称与布尔值**TRUE**一起传递，以启用接口实例。

如果驱动程序可以成功启动其设备，则应在处理即插即用（PnP）管理器的[**IRP_MN_START_DEVICE**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)请求时调用此例程。

IRP_MN_START_DEVICE 请求完成后，PnP 管理器会向任何请求它们的内核模式或用户模式组件颁发设备接口到达通知。 有关详细信息，请参阅[注册设备接口更改通知](https://docs.microsoft.com/windows-hardware/drivers/kernel/registering-for-device-interface-change-notification)。

若要禁用设备接口实例，驱动程序将调用[**IoSetDeviceInterfaceState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetdeviceinterfacestate)，并将[**IoRegisterDeviceInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterdeviceinterface)返回的*SymbolicLinkName*和**FALSE**作为*Enable*的值传递。

驱动程序在处理设备的[**IRP_MN_SURPRISE_REMOVAL**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-surprise-removal)或[**IRP_MN_REMOVE_DEVICE**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device)请求时，应禁用设备的接口。 如果驱动程序在处理这些删除 Irp 时未禁用设备接口，则它不能再尝试执行此操作，因为 PnP 管理器会在删除设备时禁用接口。

设备停止时，驱动程序不应禁用接口（[**IRP_MN_STOP_DEVICE**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-stop-device)）;相反，它应将任何设备接口启用并排队 i/o 请求，直到它收到另一个[**IRP_MN_START_DEVICE**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)请求。 同样，在设备进入睡眠状态时，驱动程序不应禁用其接口。 它应将 i/o 请求排队，直到设备唤醒。 有关详细信息，请参阅[支持具有唤醒功能的设备](https://docs.microsoft.com/windows-hardware/drivers/kernel/supporting-devices-that-have-wake-up-capabilities)。

 

 





