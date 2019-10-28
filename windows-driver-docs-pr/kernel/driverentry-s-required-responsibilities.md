---
title: DriverEntry 的必要责任
description: DriverEntry 的必要责任
ms.assetid: 6e997875-e7b7-43e2-8398-f0574f3a5816
keywords:
- DriverEntry WDK 内核，所需职责
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4b0adc60eb67d65e4c8b044ca005e7ef133fd984
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838713"
---
# <a name="driverentrys-required-responsibilities"></a>DriverEntry 的必要责任





[**DriverEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)例程所需的有序责任如下：

1.  为驱动程序的标准例程提供入口点。

    驱动程序将其许多标准例程的入口点存储在驱动程序对象或驱动程序扩展中。 此类入口点包括驱动程序的[*AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)例程、调度例程、 [*StartIo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio)例程和[*卸载*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload)例程的入口点。 例如，驱动程序会将其*AddDevice*、 [*DispatchPnP*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)和[*DispatchPower*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)例程的入口点设置为如下所示的语句（*Xxx*是供应商提供的用于标识驱动程序的前缀的占位符）：

    ```cpp
        :
    DriverObject->DriverExtension->AddDevice = XxxAddDevice;
    DriverObject->MajorFunction[IRP_MJ_PNP] = XxxDispatchPnp;
    DriverObject->MajorFunction[IRP_MJ_POWER] = XxxDispatchPower;
        :
    ```

    其他标准例程（如 Isr 或[*IoCompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)例程）通过调用系统支持例程来指定。 有关详细信息，请参阅各个[标准驱动程序例程](https://docs.microsoft.com/windows-hardware/drivers/kernel/introduction-to-standard-driver-routines)的说明。

2.  创建和/或初始化驱动程序使用的各种驱动程序范围内的对象、类型或资源。 请注意，大多数标准例程使用每个设备的对象，因此驱动程序应在其*AddDevice*例程中或在接收[**IRP\_MN\_START\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)请求后设置此类对象。

    如果驱动程序具有设备专用线程或等待任何内核定义的调度程序对象，则**DriverEntry**例程可能会初始化[内核调度程序对象](kernel-dispatcher-objects.md)。 （根据驱动程序使用对象的方式，它可能会在其*AddDevice*例程中或在接收**IRP\_MN\_START\_设备**请求之后执行此任务。）

3.  释放已分配且不再需要的任何内存。

4.  返回 NTSTATUS，指示驱动程序是否已成功加载，能否接受并处理来自 PnP 管理器的请求，以便配置、添加和启动其设备。 （请参阅[DriverEntry 返回值](driverentry-return-values.md)。）

 

 




