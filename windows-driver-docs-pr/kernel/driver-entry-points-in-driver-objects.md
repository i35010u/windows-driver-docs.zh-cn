---
title: 驱动程序对象中的驱动程序入口点
description: 驱动程序对象中的驱动程序入口点
ms.assetid: f004c2b3-8435-4c25-82e9-aff3911dc316
keywords:
- 驱动程序 WDK 内核对象
- 标准驱动程序例程 WDK 内核，驱动程序对象
- 驱动程序例程 WDK 内核，驱动程序对象
- 例程 WDK 内核，驱动程序对象
- 对象 WDK 驱动程序对象
- 入口点 WDK 内核
- 驱动程序入口点 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 60018065b47eef6ca229163bcf2c7952efab44b6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384959"
---
# <a name="driver-entry-points-in-driver-objects"></a>驱动程序对象中的驱动程序入口点





内核模式驱动程序必须在其驱动程序对象中指定以下入口点：

-   至少一个调度例程的入口点，以获取请求的 Irp，即插即用、 电源和 I/O 操作。

-   入口点及其[ *AddDevice* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_add_device)例程，在**DriverObject-&gt; DriverExtension-&gt; AddDevice**。

-   入口点及其[ *StartIo* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_startio)例程中，如果它管理其自身的 Irp 的队列。

-   如果该驱动程序可以进行加载和/或动态，替换[ *Unload* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_unload)入口点，以便释放任何系统资源，如系统对象或驱动程序已分配的内存。 (运行系统时，例如键盘驱动程序，不能替换的驱动程序不需要提供*Unload*例程。)

这些要求不适用于某些微型端口驱动程序，并为其相应的类或端口驱动程序的入口点在中定义的驱动程序对象。 请参阅详细信息的特定于设备的类型的文档。

I/O manager 会维护有关相应的驱动程序对象中的驱动程序创建的设备对象的信息。

加载驱动程序时，其[ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)例程调用时所使用的驱动程序对象的指针。 当驱动程序的**DriverEntry**调用例程，它会设置*调度*， *StartIo* （如果有），和*卸载*（如果有） 的入口点直接在驱动程序对象，如下所示：

```cpp
DriverObject->MajorFunction[IRP_MJ_xxx] = DDDispatchXxx; 
              :    : 
DriverObject->MajorFunction[IRP_MJ_yyy] = DDDispatchYyy; 
              :    : 
DriverObject->DriverStartIo = DDStartIo; 
DriverObject->DriverUnload = DDUnload; 
              :    : 
```

**DriverEntry**例程还会设置的入口点及其*AddDevice*例程，在**DriverExtension**其驱动程序对象，如下所示：

```cpp
DriverObject->DriverExtension->AddDevice = DDAddDevice; 
```

一个**DriverEntry**或可选[*重新初始化*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nc-ntddk-driver_reinitialize)例程还可以使用的驱动程序对象中的字段 (不会显示[驱动程序对象图](introduction-to-driver-objects.md#driver-object-illustration))若要获取信息和/或配置管理器的注册表数据库中设置的信息。 有关详细信息，请参阅[驱动程序的注册表项](https://docs.microsoft.com/windows-hardware/drivers/install/overview-of-registry-trees-and-keys)。

I/O 管理器将导出任何支持例程来处理驱动程序对象，后者是[**驱动程序\_对象**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_driver_object)结构。 I/O 管理器使用的驱动程序对象用于跟踪的当前加载的驱动程序。 驱动程序对象的某些成员仅使用 I/O 管理器。 其他成员也由驱动程序编写人员;例如，您必须知道某些成员名称，可定义*AddDevice*，*调度*， *StartIo*，以及*卸载*入口点。 既不应尝试使用未记录中的成员**驱动程序\_对象**结构，也不有关本文档中名为任何驱动程序对象成员的位置做出假设。 否则，无法保持到另一个驱动程序从一个 Windows 平台的可移植性。

 

 




