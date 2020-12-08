---
title: 何时检查驱动程序的 I/O 堆栈位置
description: 何时检查驱动程序的 I/O 堆栈位置
keywords:
- 调度例程 WDK 内核，i/o 堆栈位置
- I/o 堆栈位置 WDK 调度例程
- 驱动程序 i/o 堆栈位置 WDK 调度例程
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: bc39de14948a3ee539507ab00917903ffe668394
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803537"
---
# <a name="when-to-check-the-drivers-io-stack-location"></a>何时检查驱动程序的 I/O 堆栈位置





对于每个传入 IRP，驱动程序的 [i/o 堆栈位置](i-o-stack-locations.md) 中都设置了一个主要 i/o 函数代码。

驱动程序的调度例程必须检查 IRP 的驱动程序 i/o 堆栈位置，以确定是否存在以下任何情况时要执行的操作：

-   调度例程处理多个主要 i/o 函数代码。

-   调度例程必须为某些主要函数代码处理一组次要函数代码。 具有次要函数代码的 Irp 包括 [**irp \_ mj \_ PNP**](./irp-mj-pnp.md) 和 [**IRP \_ mj \_ 功能**](./irp-mj-power.md)，以及 SCSI 端口驱动程序和文件系统驱动程序必须处理的某些 irp。

-   设备驱动程序或紧密耦合的更高级别驱动程序的调度例程处理 [**IRP \_ mj \_ 设备 \_ 控制**](./irp-mj-device-control.md) 或 [**irp \_ mj \_ 内部 \_ 设备 \_ 控制**](./irp-mj-internal-device-control.md) 请求，这些请求具有一组关联的 i/o 控制代码。

若要获取指向驱动程序的 i/o 堆栈位置的指针，其调度例程将调用 [**IoGetCurrentIrpStackLocation**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)。

高层驱动程序的调度例程始终调用 **IoGetCurrentIrpStackLocation** 并调用 [**IoGetNextIrpStackLocation**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetnextirpstacklocation) ，以获取一个指针，该指针指向为下一个较低版本驱动程序设置的 irp 的 i/o 堆栈位置，并将 [irp 向下传递到驱动程序堆栈](passing-irps-down-the-driver-stack.md)中。

设备驱动程序的 [*DispatchDeviceControl*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)例程或 [*DispatchInternalDeviceControl*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)例程（也可能是它的紧密耦合类驱动程序)  (）必须确定在驱动程序的 i/o 堆栈位置中为每个请求设置了哪些 i/o **控制代码。** I/o 控制代码包含在驱动程序的 i/o 堆栈位置中。

在大多数情况下，较高级别的驱动程序的 *DispatchDeviceControl* 或 *DispatchInternalDeviceControl* 例程仅将 **Irp \_ mj \_ 设备 \_ 控制** 或 **irp \_ mj \_ 内部 \_ 设备 \_ 控制** 请求传递到下一个较低版本的驱动程序，并在 irp 中设置其堆栈位置。 但是，SCSI 类驱动程序必须检查某些 [Scsi 端口 i/o 控制代码](/windows-hardware/drivers/ddi/index) ，以便它们能够在传递这些请求之前正确设置 scsi 端口驱动程序的 i/o 堆栈位置。

 

