---
title: DispatchDeviceControl 和 DispatchInternalDeviceControl 例程
description: DispatchDeviceControl 和 DispatchInternalDeviceControl 例程
ms.assetid: 0bf8868e-bc5a-4fa7-9ff6-270f7a7bc850
keywords:
- 调度例程 WDK 内核，DispatchDeviceControl 例程
- 调度例程 WDK 内核，DispatchInternalDeviceControl 例程
- DispatchDeviceControl 例程
- DispatchInternalDeviceControl 例程
- IRP_MJ_DEVICE_CONTROL I/O 函数代码
- IRP_MJ_INTERNAL_DEVICE_CONTROL I/O 函数代码
- 内部设备控制调度例程 WDK 内核
- 设备控制调度例程 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: f9cd9fc4afcf5b0a8483b767409bbe5d9eeb9360
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575525"
---
# <a name="dispatchdevicecontrol-and-dispatchinternaldevicecontrol-routines"></a>DispatchDeviceControl 和 DispatchInternalDeviceControl 例程


驱动程序的调度例程 (请参阅[ **DRIVER_DISPATCH**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)) 使用的 I/O 函数代码来处理 Irp [ **IRP\_MJ\_设备\_控制**](https://msdn.microsoft.com/library/windows/hardware/ff550744)并[ **IRP\_MJ\_内部\_设备\_控件**](https://msdn.microsoft.com/library/windows/hardware/ff550766)分别.

对于每个常见的类型的外围设备，系统定义的 I/O 控制代码的一组**IRP\_MJ\_设备\_控制**请求。 每种类型的设备的新驱动程序必须支持这些请求。 在大多数情况下，每种类型的设备这些公共 I/O 控制代码不会导出到用户模式应用程序。 


这些系统定义的 I/O 控制代码的一些由更高级别的驱动程序为基础的设备驱动程序通过调用创建 Irp [ **IoBuildDeviceIoControlRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548318)。 其他由 Win32 组件通过调用 Win32 函数与基础的设备驱动程序进行通信[ **DeviceIoControl** ](https://msdn.microsoft.com/library/windows/desktop/aa363216) （Microsoft Windows SDK 文档中所述） 在轮次，调用系统服务。 I/O 管理器设置 IRP，并将存储主要函数代码**IRP\_MJ\_设备\_控制**中的给定 I/O 控制代码[ **IO\_堆栈\_位置**](https://msdn.microsoft.com/library/windows/hardware/ff550659)结构，在**Parameters.DeviceIoControl.IoControlCode**。 然后，I/O 管理器调用*DispatchDeviceControl*例程链中的最高级别的驱动程序。

对于某些系统提供驱动程序旨在与进行互操作和支持新的驱动程序，操作系统还定义了一系列的 I/O 控制代码**IRP\_MJ\_内部\_设备\_控制**请求。 在大多数情况下，这些公共的 I/O 控制代码允许外接程序更高级别的驱动程序与基础的设备驱动程序进行互操作。

例如，系统提供并行驱动程序支持一组内部供应商提供的驱动程序中发送的 I/O 控制代码**IRP\_MJ\_内部\_设备\_控件**请求。 有关详细信息，请参阅[并行端口的内部设备控制请求](https://msdn.microsoft.com/library/windows/hardware/ff543963)并[内部的并行设备的设备控制请求](https://msdn.microsoft.com/library/windows/hardware/ff543959)。

通过系统定义的 I/O 控制代码所请求的几乎所有操作都使用缓冲的 I/O，因为此类请求很少需要大量的数据传输。 即使为直接 I/O 设置其设备对象的驱动程序，即的设备控制请求的数据传入或传出在缓冲区的传输发送 Irp **Irp-&gt;AssociatedIrp.SystemBuffer** （除适用于某些类型的紧密耦合的 Win32 多媒体驱动程序使用的最高级别的设备驱动程序）。

此外，驱动程序可以定义一组其他驱动程序可用来与之进行通信的专用 I/O 控制代码。 新的公共 I/O 控制代码可以添加到仅与 Microsoft Corporation 的协作系统中，因为公共 I/O 控制代码已内置到操作系统本身。

有关集的不同类型的驱动程序必须支持的公共 I/O 控制代码以及定义专用的 I/O 控制代码的特定信息，请参阅特定于设备的参考部分的 Windows Driver Kit (WDK)。

 

 




