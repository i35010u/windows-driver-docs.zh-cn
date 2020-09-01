---
title: 在总线驱动程序中创建设备对象
description: 在总线驱动程序中创建设备对象
ms.assetid: 36b4d24c-9f5e-4853-bf70-c94613e01f2b
keywords:
- PnP WDK KMDF，总线驱动程序
- 即插即用 WDK KMDF、总线驱动程序
- 电源管理 WDK KMDF、总线驱动程序
- 总线驱动程序 WDK KMDF
- 物理设备对象 WDK KMDF
- PDOs WDK KMDF
- 总线枚举 WDK KMDF
- 枚举 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8d841ac0185df67fe05a1bae021424cee2f7ca7e
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89191749"
---
# <a name="creating-device-objects-in-a-bus-driver"></a>在总线驱动程序中创建设备对象


每个 [总线驱动程序](../kernel/bus-drivers.md) 都必须在发现子设备连接到父设备时创建框架设备对象。 父设备通常是一种总线，但它也可以是一个多功能设备，每个功能都需要一组单独的驱动程序， (例如支持数字音频和 MIDI) 的声卡。 总线驱动程序创建的设备对象被称为 (PDOs) 的物理设备对象，因为每个对象都表示一段硬件的实际连接 (子)  (父) 。

标识和报告连接到总线的设备的过程称为 " *总线枚举*"。

-   如果总线驱动程序执行 [动态总线枚举](dynamic-enumeration.md)，则其 [*EvtChildListCreateDevice*](/windows-hardware/drivers/ddi/wdfchildlist/nc-wdfchildlist-evt_wdf_child_list_create_device) 回调函数接收 [**WDFDEVICE \_ INIT**](./wdfdevice_init.md) 结构的句柄。

-   如果总线驱动程序执行 [静态总线枚举](static-enumeration.md)，则它必须调用 [**WDFPDOINITALLOCATE**](/windows-hardware/drivers/ddi/wdfpdo/nf-wdfpdo-wdfpdoinitallocate) 以获取 WDFDEVICE INIT 结构的句柄 \_ 。

有关总线枚举的详细信息，请参阅 [枚举总线上的设备](enumerating-the-devices-on-a-bus.md)。

总线驱动程序可以调用一组 [框架设备对象初始化方法](/windows-hardware/drivers/ddi/wdfdevice/#device-init-methods)，这些方法在 [**WDFDEVICE \_ INIT**](./wdfdevice_init.md) 结构中存储信息。 此外，总线驱动程序还可以调用 [框架 PDO 初始化方法](/windows-hardware/drivers/ddi/wdfdevice/#pdo-init-methods)。

为枚举的子设备创建框架设备对象通常包括以下步骤：

-   注册特定于总线驱动程序的回调函数。

    大多数总线驱动程序调用 [**WdfPdoInitSetEventCallbacks**](/windows-hardware/drivers/ddi/wdfpdo/nf-wdfpdo-wdfpdoinitseteventcallbacks)，因为它们必须指定设备需要的系统硬件资源。 有关指定硬件资源的详细信息，请参阅 [基于框架的驱动程序的硬件资源](hardware-resources-for-kmdf-drivers.md)。 如果设备和驱动程序支持弹出，则可以注册其他回调函数。

-   报告 [设备标识字符串](../install/device-identification-strings.md)。

    总线驱动程序必须通过对设备支持的每种类型的字符串调用 [**WdfPdoInitAssignDeviceID**](/windows-hardware/drivers/ddi/wdfpdo/nf-wdfpdo-wdfpdoinitassigndeviceid)、 [**WdfPdoInitAssignInstanceID**](/windows-hardware/drivers/ddi/wdfpdo/nf-wdfpdo-wdfpdoinitassigninstanceid)、 [**WdfPdoInitAddCompatibleID**](/windows-hardware/drivers/ddi/wdfpdo/nf-wdfpdo-wdfpdoinitaddcompatibleid)和 [**WdfPdoInitAddHardwareID**](/windows-hardware/drivers/ddi/wdfpdo/nf-wdfpdo-wdfpdoinitaddhardwareid) 来报告设备的标识字符串。 此外，使用 framework 版本1.9 或更高版本的总线驱动程序可以调用 [**WdfPdoInitAssignContainerID**](/windows-hardware/drivers/ddi/wdfpdo/nf-wdfpdo-wdfpdoinitassigncontainerid)。

-   报告总线驱动程序是否可以在 raw 模式下支持设备。

    如果总线驱动程序支持设备的 raw 模式，则必须调用 [**WdfPdoInitAssignRawDevice**](/windows-hardware/drivers/ddi/wdfpdo/nf-wdfpdo-wdfpdoinitassignrawdevice)。

-   提供描述设备的可显示文本。

    总线驱动程序调用 [**WdfPdoInitAddDeviceText**](/windows-hardware/drivers/ddi/wdfpdo/nf-wdfpdo-wdfpdoinitadddevicetext) 和 [**WdfPdoInitSetDefaultLocale**](/windows-hardware/drivers/ddi/wdfpdo/nf-wdfpdo-wdfpdoinitsetdefaultlocale) ，以多种语言提供向用户描述设备的文本。

-   正在创建设备对象。

    创建设备对象的最后一步是调用 [**WdfDeviceCreate**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)。

如果驱动程序在初始化 \_ 从 [**WdfPdoInitAllocate**](/windows-hardware/drivers/ddi/wdfpdo/nf-wdfpdo-wdfpdoinitallocate)获取的 WDFDEVICE INIT 结构时遇到错误，则驱动程序必须调用 [**WdfDeviceInitFree**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitfree) 而不是 [**WdfDeviceCreate**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)。

在总线驱动程序创建设备对象后，它通常会调用 [**WdfDeviceSetPnpCapabilities**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicesetpnpcapabilities) 和 [**WdfDeviceSetPowerCapabilities**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicesetpowercapabilities) 来报告设备的即插即用和电源功能。

每个总线驱动程序也是总线适配器的函数驱动程序。 因此，驱动程序还必须提供 [*EvtDriverDeviceAdd*](/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add) 回调函数。 此回调函数为系统上的每个总线适配器 (FDO) 创建一个功能设备对象。 有关创建 FDOs 的详细信息，请参阅 [在函数驱动程序中创建设备对象](creating-device-objects-in-a-function-driver.md)。

 

