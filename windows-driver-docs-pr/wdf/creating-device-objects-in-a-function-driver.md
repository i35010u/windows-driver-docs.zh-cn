---
title: 在功能驱动程序中创建设备对象
description: 在功能驱动程序中创建设备对象
ms.assetid: 3b988f6d-c50e-412d-85cb-031746535ff4
keywords:
- 即插即用 WDK KMDF，功能的驱动程序
- 插 WDK KMDF，功能的驱动程序
- 电源管理 WDK KMDF，功能的驱动程序
- 函数的 WDK KMDF 驱动程序
- WDK KMDF 的功能的设备对象
- FDOs WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 54fe53b4b7978960eceb15c5071651a8b92f0821
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382382"
---
# <a name="creating-device-objects-in-a-function-driver"></a>在功能驱动程序中创建设备对象


每个[功能驱动程序](https://docs.microsoft.com/windows-hardware/drivers/kernel/function-drivers)为每个系统不存在其受支持的设备创建 framework 设备对象。 因为这些设备对象创建的功能的驱动程序，它们被称为功能的设备对象 (FDOs)。 每个 FDO 是设备的功能驱动程序的表示形式。

功能驱动程序必须创建一个框架设备对象框架将调用驱动程序的每次[ *EvtDriverDeviceAdd* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)回调函数。 框架调用此回调函数来通知其支持的设备的系统存在的驱动程序。

在驱动程序[ *EvtDriverDeviceAdd* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)回调函数接收指向[ **WDFDEVICE\_INIT** ](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfdevice_init)结构。 该驱动程序可以调用一系列[framework 设备对象初始化方法](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/#device-init-methods)，这将信息存储在 WDFDEVICE\_INIT 结构。 此外，可以调用功能的驱动程序[framework FDO 初始化方法](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/#fdo-init-methods)。

通常在功能驱动程序中创建的框架设备对象包括以下步骤：

-   注册即插即用、 电源和电源策略回调函数。

    大多数函数驱动程序调用[ **WdfDeviceInitSetPnpPowerEventCallbacks** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpnppowereventcallbacks)注册 PnP 和电源的回调函数。 有关这些回调函数的详细信息，请参阅[支持即插即用和功能的驱动程序中的电源管理](supporting-pnp-and-power-management-in-function-drivers.md)。

    如果设备支持低能耗空闲状态或具有唤醒功能，功能驱动程序通常还会调用[ **WdfDeviceInitSetPowerPolicyEventCallbacks** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpowerpolicyeventcallbacks)注册电源策略回调函数。 有关这些回调函数的详细信息，请参阅[电源策略所有权](power-policy-ownership.md)。

-   正在注册函数特定于驱动程序的回调函数。

    某些函数的驱动程序调用[ **WdfFdoInitSetEventCallbacks**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdffdo/nf-wdffdo-wdffdoinitseteventcallbacks)，则它们必须参与指定设备需要的系统硬件资源。 有关硬件资源的详细信息，请参阅[基于框架的驱动程序的硬件资源](hardware-resources-for-kmdf-drivers.md)。

-   正在注册文件事件回调函数。

    如果您的驱动程序必须响应应用程序打开或关闭设备上的文件时，该驱动程序必须调用[ **WdfDeviceInitSetFileObjectConfig** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitsetfileobjectconfig)注册框架文件对象的回调函数. 有关详细信息，请参阅[使用框架文件对象](framework-file-objects.md)。

-   设置 I/O 请求属性。

    如果您的驱动程序将接收来自 framework 队列对象的 I/O 请求，该驱动程序可以调用[ **WdfDeviceInitSetRequestAttributes** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitsetrequestattributes)设置框架会将分配给设备的上下文内存请求对象。 有关详细信息，请参阅[使用请求的对象上下文](using-request-object-context.md)。

-   设置设备特征。

    通常情况下，功能驱动程序调用以下方法来指定设备的特征的一些：

    -   [**WdfDeviceInitSetDeviceType**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitsetdevicetype)，以确定硬件的驱动程序支持的类型。
    -   [**WdfDeviceInitSetIoType**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitsetiotype)，以便标识了方法来访问数据缓冲区，如果该驱动程序处理来自应用程序的 I/O 请求。
    -   [**WdfDeviceInitSetCharacteristics**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitsetcharacteristics)，将设置设备的特征，例如设备是否是只读的或支持可移动介质。
    -   [**WdfDeviceInitSetExclusive**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitsetexclusive)，如果设备通过一次一个应用程序需要独占访问权限。
    -   [**WdfDeviceInitSetPowerInrush**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpowerinrush)，如果设备需要当前涌入时从低功耗状态转换为其状态的工作 (D0)。
    -   [**WdfDeviceInitSetPowerPageable** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpowerpageable)或[ **WdfDeviceInitSetPowerNotPageable**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpowernotpageable)，以指示是否在系统时，驱动程序必须访问可分页数据处于睡眠状态的状态和工作 (S0) 状态之间转换。
    -   [**WdfDeviceInitAssignName**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitassignname)、 要将一个名称分配到的设备对象。
    -   [**WdfDeviceInitAssignSDDLString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitassignsddlstring)、 要分配给设备对象的安全描述符。
    -   [**WdfDeviceInitSetDeviceClass**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitsetdeviceclass)，以便标识设备的安装程序类。
-   获取设备属性。

    有时函数驱动程序必须获取设备的总线驱动程序或其他较低级别的驱动程序，已设置的设备属性信息。 该驱动程序可以调用[ **WdfFdoInitQueryProperty** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdffdo/nf-wdffdo-wdffdoinitqueryproperty)或[ **WdfFdoInitAllocAndQueryProperty** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdffdo/nf-wdffdo-wdffdoinitallocandqueryproperty)获取此信息。 面向 Windows 8.1 及更高版本的新驱动程序可以调用[ **WdfFdoInitQueryPropertyEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdffdo/nf-wdffdo-wdffdoinitquerypropertyex)并[ **WdfFdoInitAllocAndQueryPropertyEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdffdo/nf-wdffdo-wdffdoinitallocandquerypropertyex).

-   访问设备的注册表项。

    某些功能的驱动程序必须获取有关设备或另一个驱动程序、 用户或安装包已放在注册表中的驱动程序的信息。 该驱动程序可以调用[ **WdfFdoInitOpenRegistryKey** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdffdo/nf-wdffdo-wdffdoinitopenregistrykey)打开设备或驱动程序的注册表项。 有关详细信息，请参阅[使用的注册表中基于框架的驱动程序](https://docs.microsoft.com/windows-hardware/drivers/wdf/using-the-registry-in-wdf-drivers)。

-   创建默认子列表配置，以用于动态枚举。

    如果你正在编写功能驱动程序对于总线，并且如果您的驱动程序将执行的子设备连接到该总线的动态枚举，该驱动程序必须调用[ **WdfFdoInitSetDefaultChildListConfig** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdffdo/nf-wdffdo-wdffdoinitsetdefaultchildlistconfig). 有关详细信息，请参阅[枚举的总线上设备](enumerating-the-devices-on-a-bus.md)。

-   创建设备对象。

    创建设备对象的最后一步是调用[ **WdfDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicecreate)。

 

 





