---
title: DriverEntry 的必要责任
description: DriverEntry 的必要责任
ms.assetid: 6e997875-e7b7-43e2-8398-f0574f3a5816
keywords:
- DriverEntry WDK 内核，必须承担的责任
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8791b91870821e057743b29319fdee8b09565eee
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384952"
---
# <a name="driverentrys-required-responsibilities"></a>DriverEntry 的必要责任





所需的排序的责任[ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)例程如下所示：

1.  提供驱动程序的标准例程的入口点。

    驱动程序存储的许多驱动程序对象或驱动程序扩展中其标准例程的入口点。 此类的入口点包括驱动程序的那些[ *AddDevice* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_add_device)例程、 调度例程[ *StartIo* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_startio)例程，并[ *Unload* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_unload)例程。 例如，驱动程序将设置作为入口点及其*AddDevice*， [ *DispatchPnP*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)，以及[ *DispatchPower*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程与语句如下所示 (*Xxx*是标识该驱动程序的供应商提供的前缀的占位符):

    ```cpp
        :
    DriverObject->DriverExtension->AddDevice = XxxAddDevice;
    DriverObject->MajorFunction[IRP_MJ_PNP] = XxxDispatchPnp;
    DriverObject->MajorFunction[IRP_MJ_POWER] = XxxDispatchPower;
        :
    ```

    其他标准例程，如 Isr 或[ *IoCompletion* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine)例程，指定通过调用系统支持例程。 有关详细信息，请参阅个人的说明[标准驱动程序例程](https://docs.microsoft.com/windows-hardware/drivers/kernel/introduction-to-standard-driver-routines)。

2.  创建和/或初始化各种驱动程序级对象、 类型或驱动程序使用的资源。 请注意大多数标准例程，因此驱动程序应设置此类对象在基于每个设备使用了对象及其*AddDevice*例程或之后接收[ **IRP\_MN\_启动\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)请求。

    如果驱动程序都有设备专用线程或对任何内核定义调度程序对象，在等待**DriverEntry**例程可以初始化[内核调度程序对象](kernel-dispatcher-objects.md)。 (具体取决于如何驱动程序使用对象，它可能会改为执行此任务中的其*AddDevice*例程或之后接收**IRP\_MN\_启动\_设备**请求。)

3.  释放它分配并不再需要的任何内存。

4.  返回 NTSTATUS，该值指示是否该驱动程序已成功加载并可以接受和处理来自要配置、 添加和启动其设备的即插即用管理器的请求。 (请参阅[DriverEntry 返回值](driverentry-return-values.md)。)

 

 




