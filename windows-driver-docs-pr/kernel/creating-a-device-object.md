---
title: 创建设备对象
description: 创建设备对象
ms.assetid: 3eda8eb2-8a83-4753-a099-2531bfb9aeeb
keywords:
- 设备对象 WDK 内核，创建
- 非 WDM 驱动程序设备对象 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 42923eb5e4ee1e112ed3d6957c53a4bba50565c2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377181"
---
# <a name="creating-a-device-object"></a>创建设备对象





整体化驱动程序必须创建为其处理 I/O 请求的每个物理、 逻辑，或虚拟设备的设备对象。 不会创建设备的设备对象的驱动程序不会接收任何 Irp 的设备。

在某些技术领域，不需要创建其自己的设备对象与类驱动程序或端口驱动程序相关联的微型驱动程序。 相反，类或端口驱动程序创建的设备对象，并接收所有 Irp 的设备。 然后，类或端口驱动程序使用特定于驱动程序的方法将传递给微型驱动程序的 I/O 请求。 请参阅你的特定技术领域，以确定是否 Microsoft 提供了创建代表您的驱动程序的设备对象的类或端口驱动程序的文档。

驱动程序调用[ **IoCreateDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocreatedevice)或[ **IoCreateDeviceSecure** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdmsec/nf-wdmsec-wdmlibiocreatedevicesecure)创建它们的设备对象。 若要使用的例程的详细信息，请参阅以下各节。

[创建设备对象用于 WDM 函数和筛选器驱动程序](#creating-device-objects-for-wdm-function-and-filter-drivers)

[创建设备对象用于 WDM 总线驱动程序](#creating-device-objects-for-wdm-bus-drivers)

[为非 WDM 驱动程序创建设备对象](#creating-device-objects-for-non-wdm-drivers)

当驱动程序创建一个设备对象时，它会提供以下信息**IoCreateDevice**或**IoCreateDeviceSecure**:

-   设备的大小*设备扩展*。 设备扩展是一个系统分配存储区域，该驱动程序可以使用特定于设备的存储。 有关详细信息，请参阅[设备扩展](device-extensions.md)。

-   系统定义的常量，指示**DeviceType**设备对象表示的对象。 有关详细信息，请参阅[指定设备类型](specifying-device-types.md)。

-   一个或多个或运算，指示设备的设备特征的系统定义的常量。 有关详细信息，请参阅[指定设备特征](specifying-device-characteristics.md)。

-   一个名为的布尔值*独占*，，指定是否有点中的设备对象**标志**是否应设置\_独占的、 指示驱动程序服务的独占的设备，如视频、 串行、 并行或声音设备。 WDM 驱动程序必须设置*独占*到**FALSE**。 有关详细信息，请参阅[指定对设备对象的独占访问](specifying-exclusive-access-to-device-objects.md)。

-   指向该驱动程序的驱动程序对象的指针。 WDM 函数或筛选器驱动程序作为参数接收指向其驱动程序对象的其[ *AddDevice* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_add_device)例程。 所有驱动程序接收一个指向其驱动程序对象中其[ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)例程。 系统使用此指针将驱动程序使用其设备对象相关联。

-   指向以 null 结尾的 Unicode 字符串的可选指针 (*DeviceName*) 命名的设备。 WDM 驱动程序，以外总线驱动程序，请不要提供设备名称;因此，这样做会绕过 PnP 管理器的安全功能。 有关详细信息，请参阅[名为设备对象](named-device-objects.md)。

如果在调用[ **IoCreateDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocreatedevice)或[ **IoCreateDeviceSecure** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdmsec/nf-wdmsec-wdmlibiocreatedevicesecure)成功，I/O 管理器提供了存储设备对象本身和所有其他数据结构与设备对象相关联，其中包括设备扩展，它可以用零初始化。

### <a name="creating-device-objects-for-wdm-function-and-filter-drivers"></a>创建设备对象用于 WDM 函数和筛选器驱动程序

WDM 驱动程序，以外总线驱动程序调用**IoCreateDevice**创建它们的设备对象。 大多数 WDM 驱动程序中创建它们的设备对象及其*AddDevice*例程。 某些驱动程序，例如磁盘驱动程序必须响应来驱动布局 Ioctl，调用**IoCreateDevice**从调度例程。

Windows Driver Kit (WDK) 文档中的设备特定于类型的章节说明，否则，除非您的驱动程序应创建在其设备对象及其*AddDevice*例程。 有关详细信息，请参阅[编写 AddDevice 例程](writing-an-adddevice-routine.md)。

### <a name="creating-device-objects-for-wdm-bus-drivers"></a>创建设备对象用于 WDM 总线驱动程序

它在枚举响应中的新设备时，WDM 总线驱动程序创建一个 PDO [ **IRP\_MN\_查询\_设备\_关系**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-device-relations)请求，如果关系类型是**BusRelations**。

下列规则确定是否总线驱动程序会调用**IoCreateDevice**或**IoCreateDeviceSecure**创建设备对象：

-   如果可以在使用设备*raw 模式*，然后必须调用**IoCreateDeviceSecure**。

-   如果设备不是 raw 模式支持，然后总线驱动程序可以使用任一**IoCreateDevice**或**IoCreateDeviceSecure**。 **IoCreateDevice**总线上设备的默认系统安全性已足够; 时，可以使用**IoCreateDeviceSecure**可用于指定更严格的安全描述符。 有关详细信息，请参阅[控制的设备访问](controlling-device-access.md)。

### <a name="creating-device-objects-for-non-wdm-drivers"></a>为非 WDM 驱动程序创建设备对象

非 WDM 驱动程序将使用**IoCreateDevice**若要创建未命名的设备对象，并**IoCreateDeviceSecure**创建名为设备对象。 请注意非 WDM 驱动程序的未命名的设备对象不能从用户模式下，访问，因此驱动程序通常必须创建至少一个已命名的对象。

 

 




