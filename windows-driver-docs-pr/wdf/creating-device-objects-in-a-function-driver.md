---
title: 在功能驱动程序中创建设备对象
description: 在功能驱动程序中创建设备对象
keywords:
- PnP WDK KMDF、function 驱动程序
- 即插即用 WDK KMDF，函数驱动程序
- 电源管理 WDK KMDF，函数驱动程序
- 函数驱动程序 WDK KMDF
- 功能设备对象 WDK KMDF
- FDOs WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b55c346456008d7348fce0235a915aa04994c3b2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837045"
---
# <a name="creating-device-objects-in-a-function-driver"></a>在功能驱动程序中创建设备对象


每个 [函数驱动程序](../kernel/function-drivers.md) 为系统上存在的每个受支持的设备创建框架设备对象。 由于这些设备对象由函数驱动程序创建，因此它们被称为功能设备对象 (FDOs) 。 每个 FDO 都是一个设备驱动程序的表示形式。

函数驱动程序必须在框架每次调用驱动程序的 [*EvtDriverDeviceAdd*](/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add) 回调函数时创建框架设备对象。 框架调用此回调函数以通知驱动程序系统上存在其某个受支持的设备。

驱动程序的 [*EvtDriverDeviceAdd*](/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add) 回调函数接收指向 [**WDFDEVICE \_ INIT**](./wdfdevice_init.md) 结构的指针。 驱动程序可以调用一组 [框架设备对象初始化方法](/windows-hardware/drivers/ddi/wdfdevice/#device-init-methods)，这些方法在 WDFDEVICE INIT 结构中存储信息 \_ 。 此外，函数驱动程序还可以调用 [FRAMEWORK FDO 初始化方法](/windows-hardware/drivers/ddi/wdfdevice/#fdo-init-methods)。

在函数驱动程序中创建框架设备对象通常包括以下步骤：

-   注册 PnP、电源和电源策略回调函数。

    大多数函数驱动程序调用 [**WdfDeviceInitSetPnpPowerEventCallbacks**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpnppowereventcallbacks) 来注册 PnP 和 power 回调函数。 有关这些回调函数的详细信息，请参阅 [支持函数驱动程序中的 PnP 和电源管理](supporting-pnp-and-power-management-in-function-drivers.md)。

    如果设备支持低功耗空闲或具有唤醒功能，则函数驱动程序通常还会调用 [**WdfDeviceInitSetPowerPolicyEventCallbacks**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpowerpolicyeventcallbacks) 来注册电源策略回调函数。 有关这些回调函数的详细信息，请参阅 [电源策略所有权](power-policy-ownership.md)。

-   正在注册函数驱动程序特定的回调函数。

    如果某些函数驱动程序必须参与指定设备所需的系统硬件资源，则会调用 [**WdfFdoInitSetEventCallbacks**](/windows-hardware/drivers/ddi/wdffdo/nf-wdffdo-wdffdoinitseteventcallbacks)。 有关硬件资源的详细信息，请参阅 [Framework-Based 驱动程序的硬件资源](hardware-resources-for-kmdf-drivers.md)。

-   正在注册文件事件回调函数。

    当应用程序在设备上打开或关闭文件时，如果驱动程序必须响应，则驱动程序必须调用 [**WdfDeviceInitSetFileObjectConfig**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetfileobjectconfig) 来注册框架文件对象的回调函数。 有关详细信息，请参阅 [使用框架文件对象](framework-file-objects.md)。

-   设置 i/o 请求属性。

    如果你的驱动程序将接收来自框架队列对象的 i/o 请求，则驱动程序可以调用 [**WdfDeviceInitSetRequestAttributes**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetrequestattributes) 来设置框架将分配给设备的请求对象的上下文内存。 有关详细信息，请参阅 [使用请求对象上下文](using-request-object-context.md)。

-   设置设备特性。

    通常，函数驱动程序会调用以下部分方法来指定设备特征：

    -   [**WdfDeviceInitSetDeviceType**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetdevicetype)，用于标识驱动程序支持的硬件类型。
    -   [**WdfDeviceInitSetIoType**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetiotype)，用于标识访问数据缓冲区的方法，如果驱动程序处理来自应用程序的 i/o 请求，则为。
    -   [**WdfDeviceInitSetCharacteristics**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetcharacteristics)，用于设置设备特征，例如设备是只读的还是支持可移动介质。
    -   [**WdfDeviceInitSetExclusive**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetexclusive)，如果设备一次需要一个应用程序的独占访问权限。
    -   [**WdfDeviceInitSetPowerInrush**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpowerinrush)，如果设备从低功耗状态过渡到其工作 (D0) 状态时需要浪涌电流。
    -   [**WdfDeviceInitSetPowerPageable**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpowerpageable) 或 [**WdfDeviceInitSetPowerNotPageable**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpowernotpageable)，用于指示当系统在睡眠状态与工作 (S0) 状态之间转换时，驱动程序是否必须访问可分页数据。
    -   [**WdfDeviceInitAssignName**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitassignname)，用于为设备对象指定一个名称。
    -   [**WdfDeviceInitAssignSDDLString**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitassignsddlstring)，用于将安全描述符分配给设备对象。
    -   [**WdfDeviceInitSetDeviceClass**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetdeviceclass)，用于标识设备的安装类。
-   正在获取设备属性。

    有时，函数驱动程序必须获取有关设备总线驱动程序或其他低级驱动程序已设置的设备属性的信息。 驱动程序可以调用 [**WdfFdoInitQueryProperty**](/windows-hardware/drivers/ddi/wdffdo/nf-wdffdo-wdffdoinitqueryproperty) 或 [**WdfFdoInitAllocAndQueryProperty**](/windows-hardware/drivers/ddi/wdffdo/nf-wdffdo-wdffdoinitallocandqueryproperty) 来获取此信息。 面向 Windows 8.1 和更高版本的新驱动程序可以调用 [**WdfFdoInitQueryPropertyEx**](/windows-hardware/drivers/ddi/wdffdo/nf-wdffdo-wdffdoinitquerypropertyex) 和 [**WdfFdoInitAllocAndQueryPropertyEx**](/windows-hardware/drivers/ddi/wdffdo/nf-wdffdo-wdffdoinitallocandquerypropertyex)。

-   访问设备的注册表项。

    某些函数驱动程序必须获取有关设备或驱动程序的信息，其他驱动程序、用户或安装包已置于注册表中。 驱动程序可以调用 [**WdfFdoInitOpenRegistryKey**](/windows-hardware/drivers/ddi/wdffdo/nf-wdffdo-wdffdoinitopenregistrykey) 来打开设备或驱动程序的注册表项。 有关详细信息，请参阅 [在 Framework-Based 驱动程序中使用注册表](./introduction-to-registry-keys-for-drivers.md)。

-   创建用于动态枚举的默认子列表配置。

    如果要为总线编写函数驱动程序，并且驱动程序将执行连接到总线的子设备的动态枚举，则驱动程序必须调用 [**WdfFdoInitSetDefaultChildListConfig**](/windows-hardware/drivers/ddi/wdffdo/nf-wdffdo-wdffdoinitsetdefaultchildlistconfig)。 有关详细信息，请参阅 [枚举总线上的设备](enumerating-the-devices-on-a-bus.md)。

-   正在创建设备对象。

    创建设备对象的最后一步是调用 [**WdfDeviceCreate**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)。

 

