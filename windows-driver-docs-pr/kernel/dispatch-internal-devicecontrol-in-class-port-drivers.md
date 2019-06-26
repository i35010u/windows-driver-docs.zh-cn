---
title: 类/端口驱动程序中的 Dispatch(Internal)DeviceControl
description: 类/端口驱动程序中的 Dispatch(Internal)DeviceControl
ms.assetid: 94f6050d-c47e-4fb2-8b7f-afadcf12e0b8
keywords:
- 调度例程 WDK 内核，DispatchDeviceControl 例程
- 调度 DispatchDeviceControl 例程
- IRP_MJ_DEVICE_CONTROL I/O 函数代码
- 设备控制调度例程 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1a1a5821b34d1195b18ca3c2d80679204b0a5f56
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384994"
---
# <a name="dispatchinternaldevicecontrol-in-classport-drivers"></a>类/端口驱动程序中的 Dispatch(Internal)DeviceControl





类/端口对的更高级别的驱动程序有时可以完成 Irp 中的其[ *DispatchDeviceControl* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程。 例如类驱动程序可以在初始化期间，收集和存储信息的功能的基础设备，可能会在后面的求[ **IRP\_MJ\_设备\_控件**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)请求，并因此通过满足请求，而无需将它传递到基础设备驱动程序来节省处理时间。 类驱动程序还可以设计为检查 IRP 的参数，将仅使用有效的参数的请求发送到端口驱动程序。

紧密耦合的类/端口驱动程序还可以定义一组特定于驱动程序或特定于设备的内部 I/O 控制代码的类驱动程序可用于[ **IRP\_MJ\_内部\_设备\_控制**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)端口驱动程序的请求。

例如， *DispatchCreateClose*系统键盘和鼠标类驱动程序中的例程发送系统定义的内部的设备控制请求，以启用或禁用基础端口驱动程序的键盘和鼠标中断。 这些系统类驱动程序设置**IRP\_MJ\_内部\_设备\_控制**基础端口驱动程序的请求。 任何新的键盘或鼠标端口驱动程序的互操作使用这些系统类驱动程序还必须支持这些公共内部设备控制请求。

系统并行类/端口驱动程序模型具有类似功能。 新 parallel 类驱动程序支持通过可以从获取系统并行端口驱动程序设置为的 Irp **IRP\_MJ\_内部\_设备\_控制**具有公共 IOCTL 的请求\_并行\_端口\_*XXX*控制代码。 可以将系统并行端口驱动程序，但任何新的驱动程序还必须支持此组的公共内部设备控制请求。

有关这些公共内部设备控制请求的详细信息，请参阅特定于设备的文档中 Windows Driver Kit (WDK)。 有关如何定义专用的 I/O 控制代码的信息，请参阅[使用的 I/O 控制代码](using-i-o-control-codes.md)。

端口/类驱动程序的紧密耦合对，类驱动程序可能会处理某些设备控制请求的处理，而无需将它们传递到端口驱动程序。 对中的新类/端口驱动程序，在类驱动程序的*DispatchDeviceControl*例程可以执行以下任一操作：

-   检查其自己的 I/O 堆栈位置中的参数的有效性，如果找到任何参数错误，并调用设置 I/O 状态块[ **IoCompleteRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest)与*PriorityBoost*的 IO\_否\_递增; 否则，调用[ **IoGetNextIrpStackLocation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetnextirpstacklocation)将其自己的 I/O 堆栈位置复制到在端口驱动程序，并将传递与上的 IRP [ **IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)。

-   或者，不执行任何操作多个不检查参数的情况下设置端口驱动程序的 I/O 堆栈位置中并将其传递向端口驱动程序进行处理。

SCSI 类驱动程序必须处理设备控制请求的特殊要求。 有关这些要求的详细信息，请参阅[存储设备驱动程序](https://docs.microsoft.com/windows-hardware/drivers/storage/storage-drivers)。

 

 




