---
title: 必需的 Dispatch 例程
description: 必需的 Dispatch 例程
ms.assetid: 9b760ac7-7f31-47ad-bf84-7d79c6b24ebd
keywords:
- 所需的调度例程 WDK 内核
- 所需的调度例程 WDK 内核
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.openlocfilehash: e3dc9f6943eeb0cc4369009413e289abdaa86ed3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575876"
---
# <a name="required-dispatch-routines"></a>必需的 Dispatch 例程

大多数驱动程序必须处理以下*调度*例程：

-   [*DispatchPnP*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)

    [**IRP\_MJ\_PNP** ](https://msdn.microsoft.com/library/windows/hardware/ff550772)指示涉及即插即用设备识别、 硬件配置或资源分配的请求。 此类请求通常发送到设备驱动程序从 PnP 管理器或紧密耦合的更高级别的驱动程序。

-   [*DispatchPower*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)

    [**IRP\_MJ\_电源**](https://msdn.microsoft.com/library/windows/hardware/ff550784)指示请求属于的设备或系统电源状态。 电源管理器或紧密耦合的更高级别的驱动程序的情况下，此类请求发送到设备驱动程序。

-   [*DispatchCreate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)

    [**IRP\_MJ\_创建**](https://msdn.microsoft.com/library/windows/hardware/ff550729)任一这表示用户模式下受保护的子系统，可能是代表应用程序或子系统特定于驱动程序已请求句柄与关联的文件对象目标设备对象，或更高级别的驱动程序是连接或将其设备对象附加到目标设备对象。

-   [*DispatchClose*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)

    [**IRP\_MJ\_关闭**](https://msdn.microsoft.com/library/windows/hardware/ff550720)指示的文件对象的最后一个句柄相关联的目标设备对象已关闭和释放。 已完成或取消，因此没有任何未完成的文件对象指针引用的所有 I/O 请求。

-   [*DispatchRead*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)

    [**IRP\_MJ\_读取**](https://msdn.microsoft.com/library/windows/hardware/ff550794)指示将数据从基础物理设备传输到系统的 I/O 请求。

-   [*DispatchWrite*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)

    [**IRP\_MJ\_编写**](https://msdn.microsoft.com/library/windows/hardware/ff550819)指示将从系统的数据传输到基础物理设备的 I/O 请求。

-   [*DispatchDeviceControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)

    [**IRP\_MJ\_设备\_控件**](https://msdn.microsoft.com/library/windows/hardware/ff550744)指示包含指定的设备特定于类型的操作的系统定义的特定于设备的类型的 I/O 控制代码的请求。 更高级别的驱动程序通过这些 Irp 到其基础设备驱动程序，它通常通过访问设备处理该请求。

-   [*DispatchInternalDeviceControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)

    [**IRP\_MJ\_内部\_设备\_控制**](https://msdn.microsoft.com/library/windows/hardware/ff550766)指示请求发送到设备驱动程序，在大多数情况下从紧密耦合的更高级别的驱动程序，并且通常与私下定义、 特定于驱动程序和特定于设备类型或特定于设备的 I/O 控制代码请求特定于设备类型或特定于设备的操作。

    仅某些种类的驱动程序都需要处理系统定义的内部设备 I/O 控制请求，包括某些 SCSI 驱动程序、 键盘或鼠标设备驱动程序和并行的驱动程序进行互操作与系统提供的驱动程序。

-   [*DispatchSystemControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)

    [**IRP\_MJ\_系统\_控件**](https://msdn.microsoft.com/library/windows/hardware/ff550813)用来指定驱动程序的 WMI 请求。 有关 WMI 的详细信息，请参阅[Windows Management Instrumentation](implementing-wmi.md)。

必须提供一个驱动程序的调度例程而异的类型和功能的基础物理设备。 有关驱动程序必须处理的 IRP 主要函数代码的特定于设备的类型的信息，请参阅 Windows Driver Kit (WDK) 中的设备类型特定文档。

 

 




