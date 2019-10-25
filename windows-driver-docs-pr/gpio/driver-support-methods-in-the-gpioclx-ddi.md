---
title: GpioClx DDI 中的驱动程序支持方法
description: 从 Windows 8 开始，使用 GPIO framework 扩展（GpioClx）。
ms.assetid: 179EFB06-6122-4EB0-B9F8-D5A3089D75EE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9162210aa3a1eb0ad0141346057d6f35f6eceebe
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825051"
---
# <a name="driver-support-methods-in-the-gpioclx-ddi"></a>GpioClx DDI 中的驱动程序支持方法


从 Windows 8 开始，使用 GPIO framework 扩展（GpioClx）。 GpioClx DDI 中系统提供的方法在 GpioClx 内核模式驱动程序 Msgpioclx 中实现。 此驱动程序为[GpioClx 驱动程序支持方法](https://docs.microsoft.com/previous-versions/hh439460(v=vs.85))导出入口点。 从 Windows 8 开始，Msgpioclx 是操作系统的标准组件。

在生成时，GPIO 控制器驱动程序静态链接到 GpioClx 存根库 Msgpioclxstub 中的 DDI 入口点。 在运行时，此库执行必要的驱动程序版本协商以动态链接到 Msgpioclx 中的相应入口点。

需要 Msgpioclx 的特定版本的 GPIO 控制器驱动程序可以安全地链接到版本号更高的 Msgpioclx 版本。 但是，此驱动程序无法链接到版本号较低的 Msgpioclx 版本。

## <a name="driver-registration"></a>驱动程序注册


若要注册为 GpioClx 的客户端，GPIO 控制器驱动程序将调用[**GPIO\_CLX\_RegisterClient**](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nf-gpioclx-gpio_clx_registerclient)方法。 通常，驱动程序从其[**DriverEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)例程调用此方法。 在此调用期间，驱动程序将注册数据包传递到方法。 此数据包包含指向一组驱动程序实现的事件回调函数的指针。 这些函数访问 GPIO 控制器设备中的硬件寄存器。 GpioClx 调用这些函数来处理 i/o 请求并管理中断。

GPIO 控制器驱动程序将调用[**GPIO\_CLX\_UnregisterClient**](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nf-gpioclx-gpio_clx_unregisterclient)方法来取消使用 GpioClx 的注册。 通常，驱动程序从其[*EvtDriverUnload*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_unload)事件回调函数调用此方法。

## <a name="device-object-initialization"></a>设备对象初始化


若要初始化 GpioClx，GPIO 控制器驱动程序必须从其[*EvtDriverDeviceAdd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)回调函数调用两个 GpioClx 方法。 第一种方法（ [**GPIO\_CLX\_ProcessAddDevicePreDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nf-gpioclx-gpio_clx_processadddevicepredevicecreate)）必须在调用[**WdfDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)方法之前调用，这将创建设备对象。 第二\_种方法[**CLX\_ProcessAddDevicePostDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nf-gpioclx-gpio_clx_processadddevicepostdevicecreate)，必须在**WdfDeviceCreate**调用后调用。

## <a name="interrupt-lock"></a>中断锁


大多数驱动程序实现的事件回调函数仅在 IRQL = 被动\_级别按 GpioClx 进行调用。 但是，以下列表中的回调函数在被动\_LEVEL 或 DIRQL 上调用，具体取决于[*客户端\_QueryControllerBasicInformation*](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_query_controller_basic_information)回调函数为 GpioClx 提供的设备信息：

-   [*客户端\_ClearActiveInterrupts*](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_clear_active_interrupts)
-   [*客户端\_MaskInterrupts*](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_mask_interrupts)
-   [*客户端\_QueryActiveInterrupts*](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_query_active_interrupts)
-   [*客户端\_QueryEnabledInterrupts*](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_query_enabled_interrupts)
-   [*客户端\_UnmaskInterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_unmask_interrupt)

这些函数是从 GpioClx 中的中断服务例程（ISR）调用的，它在 DIRQL 或被动\_级别运行，具体取决于 GPIO 控制器的硬件寄存器是否为内存映射。

*客户端\_QueryControllerBasicInformation*函数以客户端\_控制器的形式提供设备信息[ **\_基本\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/ns-gpioclx-_client_controller_basic_information)结构。 如果在此结构的**Flags**成员中设置了**MemoryMappedController**标志位，则 GPIOCLX ISR 会调用 DIRQL 上前面列表中的回调函数。 否则，ISR 在被动\_级别调用所有驱动程序实现的回调函数。 有关此标志位的详细信息，请参阅[与中断相关的回调](https://docs.microsoft.com/windows-hardware/drivers/gpio/interrupt-related-callbacks)。

GpioClx 会自动同步对驱动程序实现的回调函数的调用，这些回调函数在被动\_级别运行，不从 GpioClx ISR 调用。 因此，一次只能运行其中一项函数。 但是，GpioClx 不会自动将这些被动\_级别回调与 GpioClx 从其 ISR 发出的回调同步。 如果需要，GPIO 控制器驱动程序必须显式提供此类同步。

为了避免潜在的同步错误，GpioClx 实现了 GPIO 控制器驱动程序可以获取和释放的*中断锁*。 中断锁主要由驱动程序的[*客户端\_EnableInterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_enable_interrupt)和[*客户端\_DisableInterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_disable_interrupt)回调函数使用。 驱动程序将调用[**gpio\_CLX\_AcquireInterruptLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nf-gpioclx-gpio_clx_acquireinterruptlock)方法获取锁定，并调用[**gpio\_CLX\_ReleaseInterruptLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nf-gpioclx-gpio_clx_releaseinterruptlock)方法来释放该锁。 驱动程序从在被动\_级别调用的回调函数中调用这些方法，不从 GpioClx 中的 ISR 调用这些方法。 当驱动程序持有锁时，GpioClx ISR 将无法运行。 驱动程序只应在必须与 ISR 同步的关键操作期间短暂地保存锁。

如果 GpioClx ISR 调用驱动程序实现的回调函数，则此函数无需获取（或释放）中断锁，因为 ISR 已经持有锁（并将释放该锁）。 通过此函数对[**GPIO\_CLX\_AcquireInterruptLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nf-gpioclx-gpio_clx_acquireinterruptlock)和[**gpio\_CLX\_ReleaseInterruptLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nf-gpioclx-gpio_clx_releaseinterruptlock)方法的调用不起作用，但不会被视为错误。

 

 




