---
title: 启用和禁用设备接口实例
description: 启用和禁用设备接口实例
ms.assetid: 4e3341c2-ba95-458e-8d92-a35545a773e0
keywords:
- 接口类 WDK 设备安装
- 禁用设备接口实例
- IoSetDeviceInterfaceState
- 设备接口的类 WDK 设备安装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 60909ce1384cd97cec34c793634d2b0c6f43be1a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374991"
---
# <a name="enabling-and-disabling-a-device-interface-instance"></a>启用和禁用设备接口实例





已成功启动后该设备，注册接口的驱动程序调用[ **IoSetDeviceInterfaceState** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetdeviceinterfacestate)启用接口实例。 驱动程序通过返回的符号链接名称[ **IoRegisterDeviceInterface** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioregisterdeviceinterface)与布尔值一起**TRUE**启用接口实例。

如果该驱动程序可以成功启动其设备，则应调用此例程时处理 Plug and Play (PnP) 管理器的[**执行了 IRP_MN_START_DEVICE** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)请求。

执行了 IRP_MN_START_DEVICE 请求完成后，即插即用管理器向请求它们的所有内核模式或用户模式组件发出设备接口到达通知。 有关详细信息，请参阅[注册的设备接口更改通知](https://docs.microsoft.com/windows-hardware/drivers/kernel/registering-for-device-interface-change-notification)。

若要禁用设备接口实例，驱动程序调用[ **IoSetDeviceInterfaceState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetdeviceinterfacestate)，并传递*SymbolicLinkName*返回的[ **IoRegisterDeviceInterface** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioregisterdeviceinterface)并**FALSE**的值作为*启用*。

当它处理时，驱动程序应禁用设备的接口[ **IRP_MN_SURPRISE_REMOVAL** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-surprise-removal)或[ **IRP_MN_REMOVE_DEVICE** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device)对设备的请求。 如果驱动程序不会禁用设备的接口，当处理这些删除 Irp 时，它必须随后尝试这样做是因为 PnP 管理器将禁用接口时它会删除设备。

停止设备时，驱动程序不应禁用接口 ([**IRP_MN_STOP_DEVICE**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-stop-device)); 相反，它应将保留任何启用的设备接口和队列 I/O 请求，直到其收到另一个[**执行了 IRP_MN_START_DEVICE** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)请求。 同样，驱动程序不应禁用其接口，当设备处于睡眠状态。 它应排队 I/O 请求，直到设备被唤醒。 有关详细信息，请参阅[支持设备的已唤醒功能](https://docs.microsoft.com/windows-hardware/drivers/kernel/supporting-devices-that-have-wake-up-capabilities)。

 

 





