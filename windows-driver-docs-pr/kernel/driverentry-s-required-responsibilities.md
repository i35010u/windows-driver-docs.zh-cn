---
title: DriverEntry 的必要责任
description: DriverEntry 的必要责任
ms.assetid: 6e997875-e7b7-43e2-8398-f0574f3a5816
keywords:
- DriverEntry WDK 内核，所需职责
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7121dbf1fe6094e2223de17388529c2eeba59d85
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89186011"
---
# <a name="driverentrys-required-responsibilities"></a>DriverEntry 的必要责任





[**DriverEntry**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)例程所需的有序责任如下：

1.  为驱动程序的标准例程提供入口点。

    驱动程序将其许多标准例程的入口点存储在驱动程序对象或驱动程序扩展中。 此类入口点包括驱动程序的 [*AddDevice*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device) 例程、调度例程、 [*StartIo*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio) 例程和 [*卸载*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload) 例程的入口点。 例如，驱动程序将设置其 *AddDevice*、 [*DispatchPnP*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)和 [*DispatchPower*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) 例程的入口点，其中语句如下 (*Xxx* 是供应商提供的用于标识驱动程序) 的前缀的占位符：

    ```cpp
        :
    DriverObject->DriverExtension->AddDevice = XxxAddDevice;
    DriverObject->MajorFunction[IRP_MJ_PNP] = XxxDispatchPnp;
    DriverObject->MajorFunction[IRP_MJ_POWER] = XxxDispatchPower;
        :
    ```

    其他标准例程（如 Isr 或 [*IoCompletion*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine) 例程）通过调用系统支持例程来指定。 有关详细信息，请参阅各个 [标准驱动程序例程](./introduction-to-standard-driver-routines.md)的说明。

2.  创建和/或初始化驱动程序使用的各种驱动程序范围内的对象、类型或资源。 请注意，大多数标准例程使用每个设备的对象，因此驱动程序应在其 *AddDevice* 例程中或在收到 [**IRP \_ MN \_ START \_ 设备**](./irp-mn-start-device.md) 请求后设置此类对象。

    如果驱动程序具有设备专用线程或等待任何内核定义的调度程序对象，则 **DriverEntry** 例程可能会初始化 [内核调度程序对象](./introduction-to-kernel-dispatcher-objects.md)。  (具体取决于驱动程序如何使用对象 () ，它可能改为在 *AddDevice* 例程中或在收到 **IRP \_ MN \_ START \_ DEVICE** 请求后执行此任务。 ) 

3.  释放已分配且不再需要的任何内存。

4.  返回 NTSTATUS，指示驱动程序是否已成功加载，能否接受并处理来自 PnP 管理器的请求，以便配置、添加和启动其设备。  (参阅 [DriverEntry 返回值](driverentry-return-values.md)。 ) 

 

