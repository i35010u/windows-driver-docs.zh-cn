---
title: 函数或筛选器驱动程序中的 AddDevice 例程
description: 函数或筛选器驱动程序中的 AddDevice 例程
ms.assetid: 0a095c17-2295-46df-9908-f306f7fe9f67
keywords:
- 函数驱动程序 WDK 内核
- 筛选器驱动程序 WDK 内核
- AddDevice 例程，函数驱动程序
- AddDevice 例程，筛选器驱动程序
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: c93c731e858af297dd601a5102d75b40aa98004e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837278"
---
# <a name="adddevice-routines-in-function-or-filter-drivers"></a>函数或筛选器驱动程序中的 AddDevice 例程





函数或筛选器驱动程序中的[*AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)例程应执行以下步骤：

1.  调用[**IoCreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatedevice)为所添加的设备创建功能或筛选器设备对象（FDO 或筛选器）。

    不要为设备对象指定*DeviceName* ，因为这样做会绕过 PnP 管理器的安全性。 如果用户模式组件需要到设备的符号链接，请注册设备接口（请参阅下面的下一步）。 如果内核模式组件需要旧式设备名称，则驱动程序必须命名设备对象，但不建议使用命名方式。

    包括文件\_设备\_SECURE\_在*DeviceCharacteristics*参数中打开。 此特性指示 i/o 管理器针对所有打开的请求对设备对象执行安全检查，包括相对打开和尾随文件名打开。

2.  \[可选\] 为设备创建一个或多个符号链接。

    调用[**IoRegisterDeviceInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterdeviceinterface)来注册设备功能，并创建应用程序或系统组件可用于打开设备的符号链接。 驱动程序应在处理[**IRP\_MN\_START\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)请求时，通过调用[**IoSetDeviceInterfaceState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetdeviceinterfacestate)来启用接口。 有关详细信息，请参阅[设备接口类](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)。

3.  将指针存储到设备扩展中的设备 PDO。

    PnP 管理器提供一个指向 PDO 的指针，作为*AddDevice*的*PhysicalDeviceObject*参数。 驱动程序在对例程（如[**IoGetDeviceProperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceproperty)）的调用中使用 PDO 指针。

4.  定义设备扩展中的标志以跟踪设备的特定 PnP 状态，如设备暂停、删除和意外删除。

    例如，定义一个标志，指示在设备处于暂停状态时应持有传入的 Irp。 如果驱动程序还没有用于对 Irp 进行排队的机制，请创建用于保存 Irp 的队列。 有关详细信息，请参阅[排队和出列 irp](queuing-and-dequeuing-irps.md) 。

    还需要分配**IO\_删除**设备扩展中的\_锁定结构并调用[**IoInitializeRemoveLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioinitializeremovelock)来初始化此结构。 有关详细信息，请参阅[使用删除锁](using-remove-locks.md)。

5.  将 DO\_缓冲\_IO，或在 device 对象中执行\_直接\_IO 标志位，以指定 i/o 管理器用于发送到设备堆栈的 i/o 请求的缓冲类型。 较高级别驱动程序或此成员的值与堆栈中的下一个较低驱动程序的值相同，但最高级别的驱动程序除外。 有关详细信息，请参阅[初始化设备对象](initializing-a-device-object.md)。

6.  如有必要，请将 "\_电源\_浪涌，或按电源管理\_POWER\_PAGABLE 标志。 可分页的驱动程序必须设置 DO\_POWER\_PAGABLE 标志。 设备对象标志通常由总线驱动程序在创建设备的 PDO 时设置。 但是，当高级驱动程序创建 FDO 或筛选器时，可能偶尔需要在其*AddDevice*例程中更改这些标志的值。 有关详细信息，请参阅[设置电源管理的设备对象标志](setting-device-object-flags-for-power-management.md)。

7.  创建和/或初始化驱动程序用来管理此设备的任何其他软件资源，如事件、旋转锁或其他对象。 （稍后将配置硬件资源（如 i/o 端口），以响应[**IRP\_MN\_START\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)请求。）

    由于*AddDevice*例程在系统线程上下文中以 IRQL = 被动\_级别运行，因此在初始化期间使用[**ExAllocatePoolWithTag**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag)分配的任何内存都可以从分页池进行，只要该驱动程序不控制包含系统页面文件的设备。 在*AddDevice*返回 control 之前，必须使用[**ExFreePool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exfreepool)释放此类内存分配。

8.  将设备对象附加到设备堆栈（[**IoAttachDeviceToDeviceStack**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioattachdevicetodevicestack)）。

    在*目标设备*参数中指定指向设备 PDO 的指针。

    存储**IoAttachDeviceToDeviceStack**返回的指针。 此指针指向设备的下一个较低驱动程序的设备对象，在将 Irp 向下传递到设备堆栈时，它是[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)和[**PoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver)的必需参数。

9.  清除 FDO 中的 "执行\_设备\_初始化" 标志或筛选器是否使用如下所示的语句：

    ```cpp
    FunctionalDeviceObject->Flags &= ~DO_DEVICE_INITIALIZING;
    ```

10. 准备为设备处理 PnP Irp （如[**IRP\_MN\_QUERY\_资源\_要求**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-resource-requirements)和**IRP\_MN\_START\_设备**）。

驱动程序在收到**IRP\_MN\_\_启动 IRP**后，不能开始控制设备，该设备包含 PnP 管理器分配给设备的硬件资源列表。

 

 




