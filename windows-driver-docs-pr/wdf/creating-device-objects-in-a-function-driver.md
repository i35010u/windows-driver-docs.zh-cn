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
ms.openlocfilehash: 821f0af74fe62250a0b1ac2bab94b102ad827ae1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544524"
---
# <a name="creating-device-objects-in-a-function-driver"></a>在功能驱动程序中创建设备对象


每个[功能驱动程序](https://msdn.microsoft.com/library/windows/hardware/ff546516)为每个系统不存在其受支持的设备创建 framework 设备对象。 因为这些设备对象创建的功能的驱动程序，它们被称为功能的设备对象 (FDOs)。 每个 FDO 是设备的功能驱动程序的表示形式。

功能驱动程序必须创建一个框架设备对象框架将调用驱动程序的每次[ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)回调函数。 框架调用此回调函数来通知其支持的设备的系统存在的驱动程序。

在驱动程序[ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)回调函数接收指向[ **WDFDEVICE\_INIT** ](https://msdn.microsoft.com/library/windows/hardware/ff546951)结构。 该驱动程序可以调用一系列[framework 设备对象初始化方法](https://msdn.microsoft.com/library/windows/hardware/dn265631#device-init-methods)，这将信息存储在 WDFDEVICE\_INIT 结构。 此外，可以调用功能的驱动程序[framework FDO 初始化方法](https://msdn.microsoft.com/library/windows/hardware/dn265631#fdo-init-methods)。

通常在功能驱动程序中创建的框架设备对象包括以下步骤：

-   注册即插即用、 电源和电源策略回调函数。

    大多数函数驱动程序调用[ **WdfDeviceInitSetPnpPowerEventCallbacks** ](https://msdn.microsoft.com/library/windows/hardware/ff546135)注册 PnP 和电源的回调函数。 有关这些回调函数的详细信息，请参阅[支持即插即用和功能的驱动程序中的电源管理](supporting-pnp-and-power-management-in-function-drivers.md)。

    如果设备支持低能耗空闲状态或具有唤醒功能，功能驱动程序通常还会调用[ **WdfDeviceInitSetPowerPolicyEventCallbacks** ](https://msdn.microsoft.com/library/windows/hardware/ff546774)注册电源策略回调函数。 有关这些回调函数的详细信息，请参阅[电源策略所有权](power-policy-ownership.md)。

-   正在注册函数特定于驱动程序的回调函数。

    某些函数的驱动程序调用[ **WdfFdoInitSetEventCallbacks**](https://msdn.microsoft.com/library/windows/hardware/ff547268)，则它们必须参与指定设备需要的系统硬件资源。 有关硬件资源的详细信息，请参阅[基于框架的驱动程序的硬件资源](hardware-resources-for-kmdf-drivers.md)。

-   正在注册文件事件回调函数。

    如果您的驱动程序必须响应应用程序打开或关闭设备上的文件时，该驱动程序必须调用[ **WdfDeviceInitSetFileObjectConfig** ](https://msdn.microsoft.com/library/windows/hardware/ff546107)注册框架文件对象的回调函数. 有关详细信息，请参阅[使用框架文件对象](framework-file-objects.md)。

-   设置 I/O 请求属性。

    如果您的驱动程序将接收来自 framework 队列对象的 I/O 请求，该驱动程序可以调用[ **WdfDeviceInitSetRequestAttributes** ](https://msdn.microsoft.com/library/windows/hardware/ff546786)设置框架会将分配给设备的上下文内存请求对象。 有关详细信息，请参阅[使用请求的对象上下文](using-request-object-context.md)。

-   设置设备特征。

    通常情况下，功能驱动程序调用以下方法来指定设备的特征的一些：

    -   [**WdfDeviceInitSetDeviceType**](https://msdn.microsoft.com/library/windows/hardware/ff546090)，以确定硬件的驱动程序支持的类型。
    -   [**WdfDeviceInitSetIoType**](https://msdn.microsoft.com/library/windows/hardware/ff546128)，以便标识了方法来访问数据缓冲区，如果该驱动程序处理来自应用程序的 I/O 请求。
    -   [**WdfDeviceInitSetCharacteristics**](https://msdn.microsoft.com/library/windows/hardware/ff546074)，将设置设备的特征，例如设备是否是只读的或支持可移动介质。
    -   [**WdfDeviceInitSetExclusive**](https://msdn.microsoft.com/library/windows/hardware/ff546097)，如果设备通过一次一个应用程序需要独占访问权限。
    -   [**WdfDeviceInitSetPowerInrush**](https://msdn.microsoft.com/library/windows/hardware/ff546142)，如果设备需要当前涌入时从低功耗状态转换为其状态的工作 (D0)。
    -   [**WdfDeviceInitSetPowerPageable** ](https://msdn.microsoft.com/library/windows/hardware/ff546766)或[ **WdfDeviceInitSetPowerNotPageable**](https://msdn.microsoft.com/library/windows/hardware/ff546147)，以指示是否在系统时，驱动程序必须访问可分页数据处于睡眠状态的状态和工作 (S0) 状态之间转换。
    -   [**WdfDeviceInitAssignName**](https://msdn.microsoft.com/library/windows/hardware/ff546029)、 要将一个名称分配到的设备对象。
    -   [**WdfDeviceInitAssignSDDLString**](https://msdn.microsoft.com/library/windows/hardware/ff546035)、 要分配给设备对象的安全描述符。
    -   [**WdfDeviceInitSetDeviceClass**](https://msdn.microsoft.com/library/windows/hardware/ff546084)，以便标识设备的安装程序类。
-   获取设备属性。

    有时函数驱动程序必须获取设备的总线驱动程序或其他较低级别的驱动程序，已设置的设备属性信息。 该驱动程序可以调用[ **WdfFdoInitQueryProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff547254)或[ **WdfFdoInitAllocAndQueryProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff547239)获取此信息。 面向 Windows 8.1 及更高版本的新驱动程序可以调用[ **WdfFdoInitQueryPropertyEx** ](https://msdn.microsoft.com/library/windows/hardware/dn265613)并[ **WdfFdoInitAllocAndQueryPropertyEx** ](https://msdn.microsoft.com/library/windows/hardware/dn265612).

-   访问设备的注册表项。

    某些功能的驱动程序必须获取有关设备或另一个驱动程序、 用户或安装包已放在注册表中的驱动程序的信息。 该驱动程序可以调用[ **WdfFdoInitOpenRegistryKey** ](https://msdn.microsoft.com/library/windows/hardware/ff547249)打开设备或驱动程序的注册表项。 有关详细信息，请参阅[使用的注册表中基于框架的驱动程序](https://msdn.microsoft.com/library/windows/hardware/ff545562)。

-   创建默认子列表配置，以用于动态枚举。

    如果你正在编写功能驱动程序对于总线，并且如果您的驱动程序将执行的子设备连接到该总线的动态枚举，该驱动程序必须调用[ **WdfFdoInitSetDefaultChildListConfig** ](https://msdn.microsoft.com/library/windows/hardware/ff547258). 有关详细信息，请参阅[枚举的总线上设备](enumerating-the-devices-on-a-bus.md)。

-   创建设备对象。

    创建设备对象的最后一步是调用[ **WdfDeviceCreate**](https://msdn.microsoft.com/library/windows/hardware/ff545926)。

 

 





