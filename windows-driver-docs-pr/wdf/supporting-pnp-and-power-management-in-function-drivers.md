---
title: 支持在功能驱动程序中进行 PnP 和电源管理
description: 支持在功能驱动程序中进行 PnP 和电源管理
ms.assetid: 487d4a69-a8a8-406c-8572-688388deabe3
keywords:
- PnP WDK KMDF、function 驱动程序
- 即插即用 WDK KMDF，函数驱动程序
- 电源管理 WDK KMDF，函数驱动程序
- 函数驱动程序 WDK KMDF
- 电源策略 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a0305004824b45f11da641ab47b5a6a99059b6f6
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89190781"
---
# <a name="supporting-pnp-and-power-management-in-function-drivers"></a>支持在功能驱动程序中进行 PnP 和电源管理


*函数驱动程序* 控制设备的操作，因此它们访问设备硬件。 这些驱动程序必须支持 PnP 和电源管理操作，并且通常在 [创建设备对象](creating-a-framework-device-object.md)时注册多个事件回调函数。

通常，函数驱动程序的 [*EvtDriverDeviceAdd*](/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add) 事件回调函数调用 [**WdfDeviceInitSetPnpPowerEventCallbacks**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpnppowereventcallbacks) 来注册以下回调函数：

-   [*EvtDevicePrepareHardware*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)，它将设备的系统分配的资源传递给驱动程序。 驱动程序可以执行操作，例如将设备的总线相关内存映射到处理器的虚拟地址空间，以便驱动程序可以访问硬件。

-   [*EvtDeviceD0Entry*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry)，它执行每次驱动程序设备进入工作 (D0) 状态时所需的操作，如加载固件。

-   [*EvtDeviceD0Exit*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit)，它执行每次驱动程序的设备处于工作状态 (D0) 状态并且进入低功耗状态时所需的操作。

-   [*EvtDeviceReleaseHardware*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_release_hardware)，它释放 [*EvtDevicePrepareHardware*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware) 分配的任何系统资源。

与所有框架定义的回调函数一样，以上列表中的回调函数是可选的。 仅当你的驱动程序需要时才需要提供它们。

函数驱动程序可以调用 [**WdfDeviceSetPnpCapabilities**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicesetpnpcapabilities) 和 [**WdfDeviceSetPowerCapabilities**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicesetpowercapabilities) 来向操作系统报告设备的 PnP 和电源管理功能。

通常情况下，将对大多数 i/o 请求使用框架的 *电源托管 i/o 队列* 。 如果 i/o 队列是电源管理的，则框架仅在其设备处于工作状态 (D0) 状态时才将请求传递给驱动程序。 有关电源管理 i/o 队列的详细信息，请参阅 [电源管理以了解 I/o 队列](power-management-for-i-o-queues.md)。

通常，设备的函数驱动程序是驱动程序堆栈的 *电源策略所有者* 。 电源策略所有者确定设备的相应 [设备电源状态](../kernel/device-power-states.md) ，并在设备的电源状态发生变化时将请求发送到设备的驱动程序堆栈。 对于基于框架的驱动程序，框架将处理此责任，因此你不必在驱动程序中提供代码来请求设备电源状态的更改。

电源策略所有者有另外两个责任：它控制设备在处于空闲状态时进入低功耗状态，并且系统保持其 [工作 (S0) 状态](../kernel/system-working-state-s0.md)，并控制设备在检测到低功耗状态的外部事件时生成唤醒信号的能力。 如果设备具有空闲或唤醒功能，则函数驱动程序可以提供额外的回调函数。 有关电源策略所有者职责的详细信息，请参阅 [电源策略所有权](power-policy-ownership.md)。

 

