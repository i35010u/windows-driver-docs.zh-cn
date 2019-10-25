---
title: 创建设备对象
description: 创建设备对象
ms.assetid: 3eda8eb2-8a83-4753-a099-2531bfb9aeeb
keywords:
- 设备对象 WDK 内核，创建
- 非 WDM 驱动程序设备对象 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1fe99c5247d6eae64ad2e3517f7a0622df6de977
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837018"
---
# <a name="creating-a-device-object"></a>创建设备对象





整体驱动程序必须为其处理 i/o 请求的每个物理、逻辑或虚拟设备创建一个设备对象。 不为设备创建设备对象的驱动程序不会接收设备的任何 Irp。

在某些技术领域，与类驱动程序或端口驱动程序相关联的微型驱动程序不必创建自己的设备对象。 相反，类或端口驱动程序会创建设备对象，并接收设备的所有 Irp。 然后，类或端口驱动程序使用驱动程序特定的方法将 i/o 请求传递给微型驱动程序。 请参阅特定技术领域的文档，以确定 Microsoft 是否提供代表你的驱动程序创建设备对象的类或端口驱动程序。

驱动程序调用[**IoCreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatedevice)或[**IoCreateDeviceSecure**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdmsec/nf-wdmsec-wdmlibiocreatedevicesecure)来创建其设备对象。 有关使用哪个例程的详细信息，请参阅以下各节。

[为 WDM 函数和筛选器驱动程序创建设备对象](#creating-device-objects-for-wdm-function-and-filter-drivers)

[为 WDM 总线驱动程序创建设备对象](#creating-device-objects-for-wdm-bus-drivers)

[为非 WDM 驱动程序创建设备对象](#creating-device-objects-for-non-wdm-drivers)

当驱动程序创建设备对象时，它会向**IoCreateDevice**或**IoCreateDeviceSecure**提供以下信息：

-   设备的*设备扩展*的大小。 设备扩展是系统分配的存储区域，驱动程序可将其用于特定于设备的存储。 有关详细信息，请参阅[设备扩展](device-extensions.md)。

-   系统定义的常量，指示由设备对象表示的**DeviceType** 。 有关详细信息，请参阅[指定设备类型](specifying-device-types.md)。

-   一个或多个运算的系统定义常量，用于指示设备的设备特性。 有关详细信息，请参阅[指定设备特征](specifying-device-characteristics.md)。

-   一个名为 " *Exclusive*" 的布尔值，指定是否应将设备对象**标志**中的位设置为 "DO\_exclusive"，指示驱动程序服务专用设备，如视频、串行、并行或声音设备。 WDM 驱动程序必须*将其设置*为**FALSE**。 有关详细信息，请参阅[指定对设备对象的独占访问权限](specifying-exclusive-access-to-device-objects.md)。

-   指向驱动程序的驱动程序对象的指针。 WDM 函数或筛选器驱动程序接收指向其驱动程序对象的指针作为其[*AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)例程的参数。 所有驱动程序都在其[**DriverEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)例程中收到指向其驱动程序对象的指针。 系统使用此指针将驱动程序与其设备对象相关联。

-   指向以 null 结尾的 Unicode 字符串（*DeviceName*）命名设备的可选指针。 除了总线驱动程序以外，WDM 驱动程序不提供设备名称;这样做会绕过 PnP 管理器的安全功能。 有关详细信息，请参阅[命名设备对象](named-device-objects.md)。

如果对[**IoCreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatedevice)或[**IoCreateDeviceSecure**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdmsec/nf-wdmsec-wdmlibiocreatedevicesecure)的调用成功，i/o 管理器将为设备对象本身以及与设备对象关联的所有其他数据结构（包括设备扩展）提供存储，初始化为零。

### <a name="creating-device-objects-for-wdm-function-and-filter-drivers"></a>为 WDM 函数和筛选器驱动程序创建设备对象

除总线驱动程序外，WDM 驱动程序可调用**IoCreateDevice**来创建其设备对象。 大多数 WDM 驱动程序都在其*AddDevice*例程中创建其设备对象。 某些驱动程序，如必须响应驱动器布局 IOCTLs 的磁盘驱动程序，请从调度例程调用**IoCreateDevice** 。

除非 Windows 驱动程序工具包（WDK）文档状态的设备特定于设备类型的部分，否则，驱动程序应在其*AddDevice*例程中创建其设备对象。 有关详细信息，请参阅[编写 AddDevice 例程](writing-an-adddevice-routine.md)。

### <a name="creating-device-objects-for-wdm-bus-drivers"></a>为 WDM 总线驱动程序创建设备对象

当关系类型为**BusRelations**时，WDM 总线驱动程序将创建一个 PDO，以响应[**IRP\_MN\_查询\_设备\_关系**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-device-relations)请求。

以下规则确定总线驱动程序是否调用**IoCreateDevice**或**IoCreateDeviceSecure**来创建设备对象：

-   如果设备可用于*raw 模式*，则必须调用**IoCreateDeviceSecure**。

-   如果设备不支持 raw 模式，则总线驱动程序可以使用**IoCreateDevice**或**IoCreateDeviceSecure**。 当总线上设备的默认系统安全充足时，可以使用**IoCreateDevice** ;**IoCreateDeviceSecure**可用于指定更严格的安全描述符。 有关详细信息，请参阅[控制设备访问](controlling-device-access.md)。

### <a name="creating-device-objects-for-non-wdm-drivers"></a>为非 WDM 驱动程序创建设备对象

非 WDM 驱动程序使用**IoCreateDevice**来创建未命名的设备对象，并使用**IoCreateDeviceSecure**创建命名设备对象。 请注意，非 WDM 驱动程序的未命名设备对象无法从用户模式进行访问，因此，驱动程序通常必须创建至少一个命名的对象。

 

 




