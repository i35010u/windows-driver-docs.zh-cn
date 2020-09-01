---
title: 必需的 Dispatch 例程
description: 必需的 Dispatch 例程
ms.assetid: 9b760ac7-7f31-47ad-bf84-7d79c6b24ebd
keywords:
- 调度例程 WDK 内核，必需
- 必需的调度例程 WDK 内核
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.openlocfilehash: d56abd611db8f05bf19961dd0d315c9747926582
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89189273"
---
# <a name="required-dispatch-routines"></a>必需的 Dispatch 例程

大多数驱动程序必须处理以下 *调度* 例程：

-   [*DispatchPnP*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)

    [**IRP \_MJ \_ pnp**](./irp-mj-pnp.md) 指示涉及 PNP 设备识别、硬件配置或资源分配的请求。 此类请求通常会从 PnP 管理器发送到设备驱动程序，或从紧密耦合的高级驱动程序发送到设备驱动程序。

-   [*DispatchPower*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)

    [**IRP \_MJ \_ power**](./irp-mj-power.md) 指示与设备或系统的电源状态有关的请求。 此类请求通过电源管理器或紧密耦合的更高级别驱动程序发送到设备驱动程序。

-   [*DispatchCreate*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)

    [**IRP \_MJ \_ CREATE**](./irp-mj-create.md) 表示用户模式受保护的子系统（可能代表应用程序或特定于子系统的驱动程序）已请求与目标设备对象相关联的文件对象的句柄，或者较高级别的驱动程序将其设备对象连接或附加到目标设备对象。

-   [*DispatchClose*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)

    [**IRP \_MJ \_ CLOSE**](./irp-mj-close.md) 指示已关闭并释放与目标设备对象相关联的文件对象的最后一个句柄。 所有 i/o 请求均已完成或已取消，因此没有对文件对象指针的未处理引用。

-   [*DispatchRead*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)

    [**IRP \_"MJ \_ 读取**](./irp-mj-read.md) " 指示将数据从基础物理设备传输到系统的 i/o 请求。

-   [*DispatchWrite*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)

    [**IRP \_"MJ \_ 写入**](./irp-mj-write.md) " 指示将数据从系统传输到基础物理设备的 i/o 请求。

-   [*DispatchDeviceControl*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)

    [**IRP \_"MJ \_ 设备 \_ 控制**](./irp-mj-device-control.md) " 指示一个请求，该请求包含特定于设备类型的 i/o 控制代码，该代码指定特定于设备类型的操作。 高层驱动程序将这些 Irp 传递到其基础设备驱动程序，这通常通过访问设备来处理请求。

-   [*DispatchInternalDeviceControl*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)

    [**IRP \_"MJ \_ 内部 \_ 设备 \_ 控制**](./irp-mj-internal-device-control.md) " 指示发送到设备驱动程序的请求，在大多数情况下，从紧耦合的高级驱动程序开始，通常使用私下定义的、特定于驱动程序的特定于设备类型的 i/o 控制代码，或特定于设备的 i/o 控制代码，请求特定于设备或设备的操作。

    只需要某些类型的驱动程序来处理系统定义的内部设备 i/o 控制请求，包括特定 SCSI 驱动程序、键盘或鼠标设备驱动程序以及与系统提供的驱动程序互操作的并行驱动程序。

-   [*DispatchSystemControl*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)

    [**IRP \_"MJ \_ 系统 \_ 控制**](./irp-mj-system-control.md) " 用于指定对驱动程序的 WMI 请求。 有关 WMI 的详细信息，请参阅 [Windows Management Instrumentation](implementing-wmi.md)。

驱动程序必须提供的调度例程会因基础物理设备的类型和功能而异。 有关 IRP 驱动程序必须处理的有关 IRP 主要功能代码的特定于设备类型的信息，请参阅 Windows 驱动程序工具包 (WDK) 中的设备类型特定文档。

 

