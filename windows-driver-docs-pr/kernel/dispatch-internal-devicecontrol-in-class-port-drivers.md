---
title: 类/端口驱动程序中的 Dispatch(Internal)DeviceControl
description: 类/端口驱动程序中的 Dispatch(Internal)DeviceControl
ms.assetid: 94f6050d-c47e-4fb2-8b7f-afadcf12e0b8
keywords:
- 调度例程 WDK 内核，DispatchDeviceControl 例程
- 调度 DispatchDeviceControl 例程
- IRP_MJ_DEVICE_CONTROL i/o 函数代码
- 设备控制调度例程 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1b1c3a81ccef57a428b88de496e5f8506f2c93dc
ms.sourcegitcommit: 7ca2d3e360a4ae1d4d3c3092bd34492a2645ef74
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89403134"
---
# <a name="dispatchinternaldevicecontrol-in-classport-drivers"></a>类/端口驱动程序中的 Dispatch(Internal)DeviceControl





类/端口对的较高级别的驱动程序有时可以在其 [*DispatchDeviceControl*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) 例程中完成 irp。 例如，类驱动程序在初始化期间可以收集并存储有关底层设备功能的信息，这些信息可能会在后续的 [**IRP \_ MJ \_ 设备 \_ 控制**](./irp-mj-device-control.md) 请求中寻找，因而通过满足请求来节省处理时间，而无需将请求传递到基础设备驱动程序。 类驱动程序还可以用于检查 IRP 的参数，并仅向端口驱动程序发送带有有效参数的请求。

紧耦合的类/端口驱动程序还可以定义一组特定于驱动程序的或特定于设备的内部 i/o 控制代码，类驱动程序可将其用于 [**IRP \_ MJ \_ 内部 \_ 设备 \_ 控制**](./irp-mj-internal-device-control.md) 请求发送到端口驱动程序。

例如，系统键盘和鼠标类驱动程序中的 *DispatchCreateClose* 例程发送系统定义的内部设备控制请求，以启用或禁用对基础端口驱动程序的键盘和鼠标中断。 这些系统类驱动程序为底层端口驱动程序设置 **IRP \_ MJ \_ 内部 \_ 设备 \_ 控制** 请求。 任何与这些系统类驱动程序互操作的新键盘或鼠标端口驱动程序也必须支持这些公共内部设备控制请求。

系统并行类/端口驱动程序模型具有相似的功能。 新的并行类驱动程序可以通过使用公共 IOCTL 并行端口 XXX 控制代码为**irp \_ MJ \_ 内部 \_ 设备 \_ 控制**请求设置 irp，从而从系统并行端口驱动程序获得支持 \_ \_ \_ *XXX* 。 可以替换系统并行端口驱动程序，但任何新的驱动程序也必须支持这组公共内部设备控制请求。

有关这些公共内部设备控制请求的详细信息，请参阅 Windows 驱动程序工具包中的设备特定文档 (WDK) 。 有关如何定义专用 i/o 控制代码的信息，请参阅 [使用 I/o 控制代码](introduction-to-i-o-control-codes.md)。

对于紧密耦合的端口/类驱动程序，类驱动程序可能会处理某些设备控制请求的处理，而不会将这些请求传递到端口驱动程序。 在新的类/端口驱动程序对中，类驱动程序的 *DispatchDeviceControl* 例程可以执行以下任一操作：

-   检查其自己的 i/o 堆栈位置中参数的有效性，如果找到任何参数错误，则设置 i/o 状态块，并使用 IO 的*PriorityBoost*调用[**IoCompleteRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)而 \_ 无 \_ 增量; 否则，调用[**IoGetNextIrpStackLocation**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetnextirpstacklocation)将其自己的 i/o 堆栈位置复制到端口驱动程序中，并通过[**IoCallDriver**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)传递 IRP。

-   或者，不要在 IRP 中设置端口驱动程序的 i/o 堆栈位置，而不检查参数，然后将其传递到端口驱动程序进行处理。

SCSI 类驱动程序具有处理设备控制请求的特殊要求。 有关这些要求的详细信息，请参阅 [存储驱动程序](../storage/storage-drivers.md)。

 

