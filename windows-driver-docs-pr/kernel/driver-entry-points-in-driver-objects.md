---
title: 驱动程序对象中的驱动程序入口点
description: 驱动程序对象中的驱动程序入口点
ms.assetid: f004c2b3-8435-4c25-82e9-aff3911dc316
keywords:
- 驱动对象 WDK 内核
- 标准驱动程序例程 WDK 内核，驱动程序对象
- 驱动程序例程 WDK 内核，驱动程序对象
- 例程的 WDK 内核，驱动程序对象
- 对象 WDK 驱动程序对象
- 入口点 WDK 内核
- 驱动程序入口点 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 65563d33b38e9c9a47bc536c90811f13bca81f86
ms.sourcegitcommit: 4f08f5686c0bbc27d58930b993cbab1a98e3afb0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/03/2020
ms.locfileid: "89443923"
---
# <a name="driver-entry-points-in-driver-objects"></a>驱动程序对象中的驱动程序入口点





内核模式驱动程序必须在其驱动程序对象中指定以下入口点：

-   至少一个调度例程的入口点，以便获取 Irp 请求 PnP、电源和 i/o 操作。

-   [*AddDevice*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)例程的入口点，位于**DriverObject- &gt; DriverExtension- &gt; AddDevice**。

-   其 [*StartIo*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio) 例程的入口点（如果它管理自己的 irp 队列）。

-   如果可以动态加载和/或动态替换驱动程序，则 [*卸载*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload) 入口点以释放驱动程序已分配的任何系统资源，如系统对象或内存。 在系统运行时不能替换 (驱动程序，如键盘驱动程序，不需要提供 *卸载* 例程。 ) 

这些要求不适用于某些微型端口驱动程序，其中对应的类或端口驱动程序定义驱动程序对象中的入口点。 有关详细信息，请参阅特定于设备类型的文档。

I/o 管理器在相应的驱动程序对象中维护有关驱动程序创建的设备对象的信息。

加载驱动程序时，将使用指向驱动程序对象的指针调用其 [**DriverEntry**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize) 例程。 如果调用了驱动程序的 **DriverEntry** 例程，它将设置 *调度*、 *StartIo* (如果任何) ，并在驱动程序对象中直接 (如有任何) 入口点，则 *卸载* ，如下所示：

```cpp
DriverObject->MajorFunction[IRP_MJ_xxx] = DDDispatchXxx; 
              :    : 
DriverObject->MajorFunction[IRP_MJ_yyy] = DDDispatchYyy; 
              :    : 
DriverObject->DriverStartIo = DDStartIo; 
DriverObject->DriverUnload = DDUnload; 
              :    : 
```

**DriverEntry**例程还在其 driver 对象的**DriverExtension**中设置其*AddDevice*例程的入口点，如下所示：

```cpp
DriverObject->DriverExtension->AddDevice = DDAddDevice; 
```

**DriverEntry**或可选的重新[*初始化*](/windows-hardware/drivers/ddi/ntddk/nc-ntddk-driver_reinitialize)例程还可以使用 driver 对象中的字段，而不是在[驱动程序对象简介](introduction-to-driver-objects.md)中显示，以便从和/或设置 configuration manager 的注册表数据库中的信息。 有关详细信息，请参阅 [驱动程序的注册表项](../install/overview-of-registry-trees-and-keys.md)。

I/o 管理器不会导出支持例程来处理驱动程序对象，这些对象是 [**驱动程序 \_ 对象**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_driver_object) 结构。 I/o 管理器使用驱动程序对象跟踪当前加载的驱动程序。 驱动程序对象的某些成员仅由 i/o 管理器使用。 其他成员也由驱动程序编写器使用;例如，您必须知道某些成员名称，才能定义 *AddDevice*、 *调度*、 *StartIo*和 *卸载* 入口点。 您既不应尝试使用 **驱动程序 \_ 对象** 结构中未记录的成员，也不应针对本文档中命名的任何驱动程序对象成员的位置进行假设。 否则，不能将驱动程序从一个 Windows 平台移植到另一个平台。

 

