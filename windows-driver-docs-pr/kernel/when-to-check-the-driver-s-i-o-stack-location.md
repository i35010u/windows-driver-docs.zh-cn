---
title: 何时检查驱动程序的 I/O 堆栈位置
description: 何时检查驱动程序的 I/O 堆栈位置
ms.assetid: ca084221-7b07-4db0-a987-9dd8a66d169c
keywords:
- 调度例程 WDK 内核，i/o 堆栈位置
- I/o 堆栈位置 WDK 调度例程
- 驱动程序 i/o 堆栈位置 WDK 调度例程
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 123c684563f9ffc4dc55071110c3d15515a9614e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835746"
---
# <a name="when-to-check-the-drivers-io-stack-location"></a>何时检查驱动程序的 I/O 堆栈位置





对于每个传入 IRP，驱动程序的[i/o 堆栈位置](i-o-stack-locations.md)中都设置了一个主要 i/o 函数代码。

驱动程序的调度例程必须检查 IRP 的驱动程序 i/o 堆栈位置，以确定是否存在以下任何情况时要执行的操作：

-   调度例程处理多个主要 i/o 函数代码。

-   调度例程必须为某些主要函数代码处理一组次要函数代码。 具有次要函数代码的 Irp 包括[**irp\_mj\_PNP**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-pnp)和[**irp\_mj\_电源**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-power)，以及 SCSI 端口驱动程序和文件系统驱动程序必须处理的某些 irp。

-   设备驱动程序或紧密耦合的更高级别驱动程序的调度例程处理[**IRP\_mj\_设备\_控制**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)或[**IRP\_MJ\_内部\_设备\_控制**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)请求，它具有一组关联的 i/o 控制代码。

若要获取指向驱动程序的 i/o 堆栈位置的指针，其调度例程将调用[**IoGetCurrentIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)。

较高级别的驱动程序的调度例程始终调用**IoGetCurrentIrpStackLocation**并调用[**IoGetNextIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetnextirpstacklocation) ，以获取一个指针，该指针指向为下一个较低的驱动程序设置的 irp 的下一个较低版本的 i/o 堆栈位置，当[向下传递 irp 时，驱动程序堆栈](passing-irps-down-the-driver-stack.md)。

设备驱动程序或其紧耦合类驱动程序的[*DispatchDeviceControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)例程或[*DispatchInternalDeviceControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)例程必须确定在驱动程序的 i/o 堆栈位置**中设置的 i/o 控制代码每个请求的 DeviceIoControl. IoControlCode。** I/o 控制代码包含在驱动程序的 i/o 堆栈位置中。

在大多数情况下，较高级别的驱动程序的*DispatchDeviceControl*或*DispatchInternalDeviceControl*例程仅将**IRP\_mj\_设备\_控件**或**irp\_MJ\_内部\_设备\_控制**请求到下一个较低的驱动程序，请在 IRP 中设置其堆栈位置。 但是，SCSI 类驱动程序必须检查某些[Scsi 端口 i/o 控制代码](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)，以便它们能够在传递这些请求之前正确设置 scsi 端口驱动程序的 i/o 堆栈位置。

 

 




