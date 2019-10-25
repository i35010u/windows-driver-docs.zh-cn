---
title: 处理流驱动程序中的调度例程
description: 提供处理驱动程序调度例程的指导。
ms.date: 05/17/2018
ms.localizationpriority: medium
ms.openlocfilehash: 69300a688cebcb5c2a21917f077247b6fb1a3da6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843358"
---
# <a name="handling-dispatch-routines-in-stream-drivers"></a>处理流驱动程序中的调度例程

本主题提供处理驱动程序调度例程的指导。

## <a name="adddevice-routine-for-avstream-minidrivers"></a>AVStream 微型驱动程序的 AddDevice 例程

大多数 AVStream 微型驱动程序不提供自己的*AddDevice*例程。 相反，它们使用[**KsInitializeDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksinitializedriver)安装的默认*AddDevice*处理程序[**KsAddDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksadddevice)。 但希望提供其自己的*AddDevice*处理程序的微型驱动程序应遵循以下准则。

如果驱动程序在*DriverEntry*期间调用[**KsInitializeDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksinitializedriver) ，并在以后替换*AddDevice*处理程序，则微型驱动程序可以在此例程内调用[**KsAddDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksadddevice)以执行默认添加处理。

微型驱动程序可以从此例程调用[**KsCreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-kscreatedevice) ，并传入通常可选[**KSDEVICE\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_ksdevice_descriptor)。 如果未调用[**KsInitializeDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksinitializedriver) ，则这是将创建由描述符描述的 AVStream 设备的最高级别的调用。

如果微型驱动程序创建自己的 FDO 并手动将其附加到设备堆栈，则它应调用[**KsInitializeDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksinitializedevice)来创建 AVStream 设备。

如果驱动程序未提供[**KSDEVICE\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_ksdevice_descriptor)，但仍在创建设备，AVStream 将创建默认 AVStream 设备。 此设备不包含筛选器工厂，并且永远不会调度到微型驱动程序。 微型驱动程序仍可通过调用[**KsCreateFilterFactory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-kscreatefilterfactory)来实例化设备上的[**KSFILTERFACTORY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_ksfilterfactory)结构。

安装自己的*AddDevice*处理程序：

```cpp
DriverObject->DriverExtension->AddDevice=MyAddDevice();
```
建议 AVStream 微型驱动程序使用[**KsInitializeDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksinitializedriver)提供的功能，而不是替代类驱动程序提供的默认*AddDevice*例程。

有关详细信息，请参阅[DRIVER_INITIALIZE](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)回调函数。

## <a name="driverentry-routine-for-stream-class-minidrivers"></a>Stream 类微型驱动程序的 DriverEntry 例程

**DriverEntry**是微型驱动程序的流类的初始入口点。 此例程是必需的。

由于[**StreamClassRegisterMinidriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/nf-strmini-streamclassregisteradapter)执行大部分必需的驱动程序初始化，因此 stream 类微型驱动程序的**DriverEntry**例程的主要任务是在\_数据的情况下分配并填充[**HW\_初始化**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_initialization_data)包含驱动程序特定的常量和入口点的结构。 然后， **DriverEntry**应调用**StreamClassRegisterMinidriver**。

有关详细信息，请参阅[DRIVER_INITIALIZE](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)回调函数。

## <a name="driverentry-function-of-avstream-minidriver-function"></a>AVStream 微型驱动程序函数的 DriverEntry 函数

*DriverEntry*函数是 AVStream 微型驱动程序的初始入口点。

要加载每个 AVStream 微型驱动程序，必须具有显式命名为*DriverEntry*的函数。 *DriverEntry*是由 i/o 系统直接调用的。 通常， *DriverEntry*调用[**KsInitializeDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksinitializedriver) ，然后返回**KsInitializeDriver**返回的值。

有关详细信息，请参阅[DRIVER_INITIALIZE](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)回调函数。

## <a name="kscancelroutine-function"></a>KsCancelRoutine 函数

**KsCancelRoutine**函数执行标准 IRP 取消功能：删除该条目，然后取消并完成该请求。 函数被定义为 PDRIVER\_取消例程。 如果未提供任何值，则它是用于**KsAddIrpToCancelableQueue**的默认函数。

此函数通常由 i/o 子系统在取消 IRP 时调用，但是可以直接调用以响应 KSMETHOD\_STREAM\_演示集请求。 与任何典型的 cancel 例程一样，此函数期望在输入函数时获得 i/o cancel 自旋锁。

请注意，此例程需要 KSQUEUE\_旋转锁\_IRP\_存储（Irp）以指向**KsAddIrpToCancelableQueue**中提供的列表访问自旋锁。

**KsCancelRoutine**可用于执行初步列表删除处理，而无需实际完成 IRP。 如果 Irp&gt;IoStatus 设置为 "状态"\_在输入此函数时取消，则 IRP 将不会完成。 否则，状态将设置为 "状态\_已取消，并且 IRP 将完成。 此**KsCancelRoutine**可用于执行初始列表和旋转锁定操作，并返回到驱动程序的完成例程以执行特定处理和最终 IRP 完成。

有关详细信息，请参阅[DRIVER_CANCEL](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_cancel)例程。

## <a name="ksdefaultdispatchpnp-function"></a>KsDefaultDispatchPnp 函数

```cpp
KSDDKAPI
_Dispatch_type_(IRP_MJ_PNP) DRIVER_DISPATCH KsDefaultDispatchPnp;
```

**KsDefaultDispatchPnp**函数是默认的主 PnP 调度处理程序;与功能设备对象相关的通知可以定向到此处理程序。 此函数将所有通知传递到以前使用**KsSetDevicePnpAndBaseObject**设置的 PnP 设备对象，并假定使用设备标头。 如果向函数传递了 IRP\_MN\_删除\_设备，则会删除该设备对象。

**KsDefaultDispatchPnp**函数返回基础物理设备对象 IRP 处理的状态。

当除了释放设备标头并删除实际设备对象之外，在删除设备时不需要额外的清理时， **KsDefaultDispatchPnp**函数将非常有用。

有关详细信息，请参阅[DRIVER_DISPATCH](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)例程。


## <a name="ksdefaultdispatchpower-function"></a>KsDefaultDispatchPower 函数

```cpp
KSDDKAPI
_Dispatch_type_(IRP_MJ_POWER) DRIVER_DISPATCH KsDefaultDispatchPower;
```

**KsDefaultDispatchPower**函数是一个默认的主电源调度处理程序。 可在此处定向有关功能设备对象的通知。 此函数将所有通知传递到以前使用**KsSetDevicePnpAndBaseObject**设置的 PnP 设备对象，并假定使用设备标头。

当电源 Irp 上无需额外的清理，或仅仅是一种完成任何电源 IRP 的方法时， **KsDefaultDispatchPower**函数将非常有用。 它还允许特定文件对象（如默认时钟 imlementation）使用**KsSetPowerDispatch**附加到 power irp，并在此例程完成之前对其执行操作。 此函数在完成 IRP 之前调用每个电源调度例程。

有关详细信息，请参阅[DRIVER_DISPATCH](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)例程。

## <a name="ksdefaultforwardirp-routine"></a>KsDefaultForwardIrp 例程

```cpp
KSDDKAPI
_Dispatch_type_(IRP_MJ_SYSTEM_CONTROL)
_Dispatch_type_(IRP_MJ_DEVICE_CONTROL)
DRIVER_DISPATCH KsDefaultForwardIrp;
```

此默认处理程序允许调度例程将 i/o 请求转发到相应的物理设备对象。

此默认处理程序提供了一种方法，用于调度例程，以满足驱动程序具有 IRP\_MJ\_用于特定主要功能的\* 函数处理程序的要求。

有关详细信息，请参阅[DRIVER_DISPATCH](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)例程。

<a name="see-also"></a>另请参阅
--------

[KsAddDevice](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksadddevice)

[KsCreateDevice](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-kscreatedevice)

[KSDEVICE](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_ksdevice)

[KsDispatchIrp](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksdispatchirp)

[KsInitializeDevice](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksinitializedevice)

[KsInitializeDriver](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksinitializedriver)

[KsAddIrpToCancelableQueue](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksaddirptocancelablequeue)

[DriverEntry](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)

[驱动\_对象](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_driver_object)

[设备\_对象](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_object)

[StreamClassRegisterMinidriver](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/nf-strmini-streamclassregisteradapter)

[\_数据的 HW\_初始化](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_initialization_data)

[编写 DriverEntry 例程](https://docs.microsoft.com/windows-hardware/drivers/kernel/writing-a-driverentry-routine)








