---
title: DispatchDeviceControl 和 DispatchInternalDeviceControl 例程
description: DispatchDeviceControl 和 DispatchInternalDeviceControl 例程
ms.assetid: 0bf8868e-bc5a-4fa7-9ff6-270f7a7bc850
keywords:
- 调度例程 WDK 内核，DispatchDeviceControl 例程
- 调度例程 WDK 内核，DispatchInternalDeviceControl 例程
- DispatchDeviceControl 例程
- DispatchInternalDeviceControl 例程
- IRP_MJ_DEVICE_CONTROL i/o 函数代码
- IRP_MJ_INTERNAL_DEVICE_CONTROL i/o 函数代码
- 内部设备控制调度例程 WDK 内核
- 设备控制调度例程 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: ba48ea056877215bcd8ea7b9445658552c57bce1
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90715258"
---
# <a name="dispatchdevicecontrol-and-dispatchinternaldevicecontrol-routines"></a>DispatchDeviceControl 和 DispatchInternalDeviceControl 例程


驱动程序的调度例程 (参阅 [**DRIVER_DISPATCH**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)) 使用 [**irp \_ mj \_ 设备 \_ 控制**](./irp-mj-device-control.md) 的 I/o 函数代码和 [**irp \_ mj \_ 内部 \_ 设备 \_ 控制**](./irp-mj-internal-device-control.md)来处理 irp。

对于每种通用类型的外围设备，系统会为 **IRP \_ MJ \_ 设备 \_ 控制** 请求定义一组 i/o 控制代码。 每种类型的设备的新驱动程序必须支持这些请求。 在大多数情况下，每种类型的设备的这些公共 i/o 控制代码不会导出到用户模式应用程序。 


其中一些系统定义的 i/o 控制代码由较高级别的驱动程序使用，通过调用 [**IoBuildDeviceIoControlRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuilddeviceiocontrolrequest)为基础设备驱动程序创建 irp。 其他方法由 Win32 组件用来与基础设备驱动程序进行通信，方法是调用 Microsoft Windows SDK 文档中所述的 Win32 函数 [**DeviceIoControl**](/windows/win32/api/ioapiset/nf-ioapiset-deviceiocontrol) () 这反过来会调用系统服务。 I/o 管理器设置 IRP，并将主函数代码 **IRP \_ MJ \_ 设备 \_ 控件** 和 I/o 控制代码存储在 [**IO \_ 堆栈 \_ 位置**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location) 结构中的 **DeviceIoControl. IoControlCode**。 然后，i/o 管理器会调用链中最高级别的驱动程序的 *DispatchDeviceControl* 例程。

对于某些系统提供的驱动程序，旨在与和支持新的驱动程序，操作系统还定义了一组用于 **IRP \_ MJ \_ 内部 \_ 设备 \_ 控制** 请求的 i/o 控制代码。 在大多数情况下，这些公共 i/o 控制代码允许附加的高级驱动程序与基础设备驱动程序进行互操作。

例如，系统提供的并行驱动程序支持供应商提供的驱动程序在 **IRP \_ MJ \_ 内部 \_ 设备 \_ 控制** 请求中发送的一组内部 i/o 控制代码。 有关详细信息，请参阅 [内部设备控制对并行端口的请求](/windows-hardware/drivers/ddi/index) 和 [对并行设备的内部设备控制请求](/windows-hardware/drivers/ddi/index)。

几乎通过系统定义的 i/o 控制代码请求的所有操作都使用缓冲 i/o，因为这种类型的请求很少需要传输大量的数据。 也就是说，即使是为直接 i/o 设置其设备对象的驱动程序，也会为设备控制请求发送 Irp，并将数据传输到缓冲区中的数据，并将数据传输到 ** &gt;AssociatedIrp.SystemBuffer** (，但具有紧密耦合的 Win32 多媒体驱动) 程序的特定类型的高级设备驱动程序除外。

此外，驱动程序还可以定义一组专用 i/o 控制代码，其他驱动程序可以使用这些代码与之通信。 只能将新的公共 i/o 控制代码添加到系统中，这是因为公共 i/o 控制代码内置于操作系统本身中。

有关不同类型的驱动程序必须支持和定义专用 i/o 控制代码的一组公共 i/o 控制代码的特定信息，请参阅 Windows 驱动程序工具包的特定于设备的参考部分 (WDK) 。

 

