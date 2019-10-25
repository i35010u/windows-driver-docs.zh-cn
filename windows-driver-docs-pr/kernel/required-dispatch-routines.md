---
title: 必需的 Dispatch 例程
description: 必需的 Dispatch 例程
ms.assetid: 9b760ac7-7f31-47ad-bf84-7d79c6b24ebd
keywords:
- 调度例程 WDK 内核，必需
- 必需的调度例程 WDK 内核
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.openlocfilehash: eb42ff5bb4a781c129f61f8ee85b1ed72e319215
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836470"
---
# <a name="required-dispatch-routines"></a>必需的 Dispatch 例程

大多数驱动程序必须处理以下*调度*例程：

-   [*DispatchPnP*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)

    [**IRP\_MJ\_pnp**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-pnp)表示涉及 PNP 设备识别、硬件配置或资源分配的请求。 此类请求通常会从 PnP 管理器发送到设备驱动程序，或从紧密耦合的高级驱动程序发送到设备驱动程序。

-   [*DispatchPower*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)

    [**IRP\_MJ\_电源**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-power)表示与设备或系统的电源状态有关的请求。 此类请求通过电源管理器或紧密耦合的更高级别驱动程序发送到设备驱动程序。

-   [*DispatchCreate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)

    [**IRP\_MJ\_CREATE**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-create)指示用户模式受保护的子系统（可能代表应用程序或特定于子系统的驱动程序）已请求与目标设备对象相关联的文件对象的句柄，或高层驱动程序将其设备对象连接或附加到目标设备对象。

-   [*DispatchClose*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)

    [**IRP\_MJ\_CLOSE**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-close)指示已关闭并释放与目标设备对象相关联的文件对象的最后一个句柄。 所有 i/o 请求均已完成或已取消，因此没有对文件对象指针的未处理引用。

-   [*DispatchRead*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)

    [**IRP\_MJ\_读取**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-read)指示将数据从基础物理设备传输到系统的 i/o 请求。

-   [*DispatchWrite*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)

    [**IRP\_MJ\_写入**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-write)指示将数据从系统传输到基础物理设备的 i/o 请求。

-   [*DispatchDeviceControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)

    [**IRP\_MJ\_设备\_控件**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)指示一个请求，该请求包含特定于设备类型的 i/o 控制代码，该代码指定特定于设备类型的操作。 高层驱动程序将这些 Irp 传递到其基础设备驱动程序，这通常通过访问设备来处理请求。

-   [*DispatchInternalDeviceControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)

    [**IRP\_MJ\_内部\_设备\_控制**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)指示发送到设备驱动程序的请求，在大多数情况下，从紧耦合的更高级别的驱动程序，通常使用私下定义的特定于驱动程序的和特定于设备类型或特定于设备的 i/o 控制代码，请求特定于设备的操作或特定于设备的操作。

    只需要某些类型的驱动程序来处理系统定义的内部设备 i/o 控制请求，包括特定 SCSI 驱动程序、键盘或鼠标设备驱动程序以及与系统提供的驱动程序互操作的并行驱动程序。

-   [*DispatchSystemControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)

    [**IRP\_MJ\_系统\_控件**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-system-control)用于指定对驱动程序的 WMI 请求。 有关 WMI 的详细信息，请参阅[Windows Management Instrumentation](implementing-wmi.md)。

驱动程序必须提供的调度例程会因基础物理设备的类型和功能而异。 有关 IRP 驱动程序必须处理的有关 IRP 主要功能代码的特定于设备类型的信息，请参阅 Windows 驱动程序工具包（WDK）中的设备类型特定文档。

 

 




