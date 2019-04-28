---
title: 何时检查驱动程序的 I/O 堆栈位置
description: 何时检查驱动程序的 I/O 堆栈位置
ms.assetid: ca084221-7b07-4db0-a987-9dd8a66d169c
keywords:
- 调度例程 WDK 内核，I/O 堆栈位置
- I/O 堆栈位置 WDK 调度例程
- 驱动程序 I/O 堆栈位置 WDK 调度例程
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 527f3bc56d1b775828426bc59a4e0764cfc0d5c7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341425"
---
# <a name="when-to-check-the-drivers-io-stack-location"></a>何时检查驱动程序的 I/O 堆栈位置





主要的 I/O 函数代码中的驱动程序设置[I/O 堆栈位置](i-o-stack-locations.md)为每个传入 IRP。

驱动程序的调度例程必须检查驱动程序的 I/O 的 IRP 来确定要执行的操作如果以下条件的任何保存的堆栈位置：

-   调度例程处理多个主要的 I/O 函数代码。

-   调度例程必须处理一组的次要函数代码的某些主要函数代码。 使用次要函数代码包括 Irp [ **IRP\_MJ\_PNP** ](https://msdn.microsoft.com/library/windows/hardware/ff550772)并[ **IRP\_MJ\_POWER** ](https://msdn.microsoft.com/library/windows/hardware/ff550784)，以及为某些 Irp 的 SCSI 端口驱动程序和文件系统驱动程序必须处理的。

-   调度例程或紧密耦合的更高级别的驱动程序的设备驱动程序处理[ **IRP\_MJ\_设备\_控制**](https://msdn.microsoft.com/library/windows/hardware/ff550744)或[ **IRP\_MJ\_内部\_设备\_控制**](https://msdn.microsoft.com/library/windows/hardware/ff550766)具有一组关联的 I/O 控制代码的请求。

若要获取指向驱动程序的 I/O 堆栈位置，其调度例程调用[ **IoGetCurrentIrpStackLocation**](https://msdn.microsoft.com/library/windows/hardware/ff549174)。

更高级别的驱动程序的调度例程始终调用**IoGetCurrentIrpStackLocation** ，调用[ **IoGetNextIrpStackLocation** ](https://msdn.microsoft.com/library/windows/hardware/ff549266)若要获取的指针到下一步越低设置为下一步较低的驱动程序，Irp 的驱动程序的 I/O 堆栈位置时[驱动程序堆栈的下层传递 Irp](passing-irps-down-the-driver-stack.md)。

[ *DispatchDeviceControl* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程或[ *DispatchInternalDeviceControl* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程的设备驱动程序，或可能的其紧密耦合的类驱动程序，必须确定在驱动程序的 I/O 堆栈位置在中设置的 I/O 控制代码**Parameters.DeviceIoControl.IoControlCode**为每个请求。 I/O 控制代码包含在驱动程序的 I/O 堆栈位置。

在大多数情况下， *DispatchDeviceControl*或*DispatchInternalDeviceControl*例程的更高级别的驱动程序只是将传递**IRP\_MJ\_设备\_控制**或**IRP\_MJ\_内部\_设备\_控件**到较低的下一步驱动程序的设置其堆栈后，请求中的位置。 但是，SCSI 类驱动程序必须检查是否有某些[SCSI 端口 I/O 控制代码](https://msdn.microsoft.com/library/windows/hardware/ff565367)，以便它们可以正确设置了 SCSI 端口驱动程序的 I/O 堆栈位置然后再将这些请求上传递。

 

 




