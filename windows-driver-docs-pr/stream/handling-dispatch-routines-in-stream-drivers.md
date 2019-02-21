---
title: 处理流驱动程序中的调度例程
description: 提供有关如何处理驱动程序调度例程指南。
ms.date: 05/17/2018
ms.localizationpriority: medium
ms.openlocfilehash: 47a093548a83921a7d3f49da61887c7e968a8660
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520245"
---
# <a name="handling-dispatch-routines-in-stream-drivers"></a>处理流驱动程序中的调度例程

本主题提供有关如何处理驱动程序调度例程指南。

## <a name="adddevice-routine-for-avstream-minidrivers"></a>有关 AVStream 微型驱动程序 AddDevice 例程

大多数 AVStream 微型驱动程序不提供其自己*AddDevice*例程。 相反，它们使用[ **KsAddDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksadddevice)，默认值*AddDevice*处理程序的情况下安装[ **KsInitializeDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff562683). 尽管如此希望提供其自己的微型驱动程序*AddDevice*处理程序应遵循以下指导原则。

如果该驱动程序调用[ **KsInitializeDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksinitializedriver)期间*DriverEntry*和更高版本将替换*AddDevice*微型驱动程序可以处理程序，调用[ **KsAddDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff560927)从在该例程中，执行默认添加处理。

微型驱动程序可以调用[ **KsCreateDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-kscreatedevice)在该例程，传递在名义上可选[ **KSDEVICE\_描述符**](https://msdn.microsoft.com/library/windows/hardware/ff561691). 如果[ **KsInitializeDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff562683)是不会调用，这是将创建一个描述符所描述的 AVStream 设备的最高级别调用。

如果微型驱动程序创建其自己 FDO 并手动将其自身附加到设备堆栈，则应调用[ **KsInitializeDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksinitializedevice)创建 AVStream 设备。

如果该驱动程序未提供[ **KSDEVICE\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_ksdevice_descriptor) ，同时仍将创建一个设备，AVStream 创建默认 AVStream 设备。 此设备包含任何筛选器工厂，永远不会调度到微型驱动程序。 微型驱动程序仍可以实例化[ **KSFILTERFACTORY** ](https://msdn.microsoft.com/library/windows/hardware/ff562530)通过调用设备上的结构[ **KsCreateFilterFactory**](https://msdn.microsoft.com/library/windows/hardware/ff561650)。

若要安装你自己*AddDevice*处理程序：

```cpp
DriverObject->DriverExtension->AddDevice=MyAddDevice();
```
我们建议使用 AVStream 微型驱动程序使用提供的功能[ **KsInitializeDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksinitializedriver)，而不是不是重写默认*AddDevice*例程提供的类驱动程序。

有关详细信息，请参阅[DRIVER_INITIALIZE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)回调函数。

## <a name="driverentry-routine-for-stream-class-minidrivers"></a>Stream 类微型驱动程序的 DriverEntry 例程

**DriverEntry**是初始入口点的流类微型驱动程序。 此例程是必需的。

由于[ **StreamClassRegisterMinidriver** ](https://msdn.microsoft.com/library/windows/hardware/ff568263)执行的所需的驱动程序初始化，主要任务的流类微型驱动程序的大部分**DriverEntry**例程是分配，并填写[ **HW\_初始化\_数据**](https://msdn.microsoft.com/library/windows/hardware/ff559682)带有特定于驱动程序常量和入口点的结构。 **DriverEntry**然后应调用**StreamClassRegisterMinidriver**。

有关详细信息，请参阅[DRIVER_INITIALIZE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)回调函数。

## <a name="driverentry-function-of-avstream-minidriver-function"></a>DriverEntry 函数的 AVStream 微型驱动程序函数

*DriverEntry*函数是 AVStream 微型驱动程序的初始入口点。

每个 AVStream 微型驱动程序必须具有显式命名的函数*DriverEntry*才能加载。 *DriverEntry*由 I/O 系统直接调用。 通常情况下， *DriverEntry*调用[ **KsInitializeDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff562683) ，然后返回返回的值**KsInitializeDriver**。

有关详细信息，请参阅[DRIVER_INITIALIZE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)回调函数。

## <a name="kscancelroutine-function"></a>KsCancelRoutine 函数

**KsCancelRoutine**函数执行标准 IRP 取消功能： 移除的项，然后取消和完成请求。 函数定义为 PDRIVER\_取消例程。 它是用于默认函数**KsAddIrpToCancelableQueue**如果未提供任何内容。

此函数通常会由 I/O 子系统上取消 IRP 调用，但可以调用直接以响应 KSMETHOD\_流\_演示文稿设置请求。 与任何典型的取消例程，此函数需要 I/O 取消自旋锁以获得在输入函数。

请注意此例程需要 KSQUEUE\_SPINLOCK\_IRP\_STORAGE(Irp) 中提供指向列表访问自旋锁**KsAddIrpToCancelableQueue**。

**KsCancelRoutine**可以用于执行处理，但实际上并未完成 IRP 初步列表删除。 如果 Irp-&gt;IoStatus.Status 设置状态为\_输入此函数时已取消，然后 IRP 将无法完成。 否则，状态将设置为状态\_已取消和 IRP 将完成。 这**KsCancelRoutine**可以在取消例程中使用以执行操作的初始列表和旋转锁操作并返回到驱动程序的完成例程，以执行特定的处理和最终的 IRP 完成。

有关详细信息，请参阅[DRIVER_CANCEL](https://msdn.microsoft.com/library/windows/hardware/ff540742)例程。

## <a name="ksdefaultdispatchpnp-function"></a>KsDefaultDispatchPnp 函数

```cpp
KSDDKAPI
_Dispatch_type_(IRP_MJ_PNP) DRIVER_DISPATCH KsDefaultDispatchPnp;
```

**KsDefaultDispatchPnp**函数是默认的即插即用的主调度处理程序; 有关功能的设备对象的通知可以定向到此处理程序。 此函数将所有通知都传递到与以前设置的即插即用设备对象**KsSetDevicePnpAndBaseObject** ，并假定设备标头的使用。 当该函数传递 IRP\_MN\_删除\_删除设备，设备对象。

**KsDefaultDispatchPnp**函数返回的基础物理设备对象 IRP 处理状态。

**KsDefaultDispatchPnp**时不删除超出释放设备标头和删除实际的设备对象的设备时，需要执行额外清理函数很有用。

有关详细信息，请参阅[DRIVER_DISPATCH](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程。


## <a name="ksdefaultdispatchpower-function"></a>KsDefaultDispatchPower 函数

```cpp
KSDDKAPI
_Dispatch_type_(IRP_MJ_POWER) DRIVER_DISPATCH KsDefaultDispatchPower;
```

**KsDefaultDispatchPower**函数是默认主电源调度处理程序。 可以在此处定向通知有关功能的设备对象。 此函数将所有通知都传递到与以前设置的即插即用设备对象**KsSetDevicePnpAndBaseObject**，并假定设备标头的使用。

**KsDefaultDispatchPower**时不需要在 power Irp，或只是作为一种方法完成任何电源 IRP 的额外清理函数很有用。 它还允许特定的文件对象，如默认时钟实施已，若要将自身附加到使用 power Irp **KsSetPowerDispatch**，并在它们完成此例程之前对其采取措施。 此函数在完成 IRP 之前将调用每个 power 调度例程。

有关详细信息，请参阅[DRIVER_DISPATCH](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程。

## <a name="ksdefaultforwardirp-routine"></a>KsDefaultForwardIrp 例程

```cpp
KSDDKAPI
_Dispatch_type_(IRP_MJ_SYSTEM_CONTROL)
_Dispatch_type_(IRP_MJ_DEVICE_CONTROL)
DRIVER_DISPATCH KsDefaultForwardIrp;
```

此默认处理程序允许调度例程将 I/O 请求转发到相应的物理设备对象。

此默认处理程序提供了一种方法对于调度例程来满足需求驱动程序具有 IRP\_MJ\_ \*主要的特定函数的函数处理程序。

有关详细信息，请参阅[DRIVER_DISPATCH](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程。

<a name="see-also"></a>另请参阅
--------

[KsAddDevice](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksadddevice)

[KsCreateDevice](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-kscreatedevice)

[KSDEVICE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_ksdevice)

[KsDispatchIrp](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksdispatchirp)

[KsInitializeDevice](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksinitializedevice)

[KsInitializeDriver](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksinitializedriver)

[KsAddIrpToCancelableQueue](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksaddirptocancelablequeue)

[DriverEntry](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)

[DRIVER\_OBJECT](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_driver_object)

[设备\_对象](https://msdn.microsoft.com/library/windows/hardware/ff543147)

[StreamClassRegisterMinidriver](https://msdn.microsoft.com/library/windows/hardware/ff568263)

[HW\_INITIALIZATION\_DATA](https://msdn.microsoft.com/library/windows/hardware/ff559682)

[编写 DriverEntry 例程](https://docs.microsoft.com/windows-hardware/drivers/kernel/writing-a-driverentry-routine)








