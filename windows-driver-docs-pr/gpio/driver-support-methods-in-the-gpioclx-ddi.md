---
title: GpioClx DDI 中的驱动程序支持方法
description: 可从 Windows 8 开始 GPIO 框架扩展 (GpioClx)。
ms.assetid: 179EFB06-6122-4EB0-B9F8-D5A3089D75EE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1cf41f9041ec4305431baeb2819344a8b98ad2aa
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363639"
---
# <a name="driver-support-methods-in-the-gpioclx-ddi"></a>GpioClx DDI 中的驱动程序支持方法


可从 Windows 8 开始 GPIO 框架扩展 (GpioClx)。 GpioClx 内核模式驱动程序 Msgpioclx.sys 中实现 GpioClx DDI 中系统提供的方法。 此驱动程序将导出的入口点[GpioClx 驱动程序支持的方法](https://docs.microsoft.com/previous-versions/hh439460(v=vs.85))。 从 Windows 8 开始，Msgpioclx.sys 是操作系统的一个标准组件。

在生成时，GPIO 控制器驱动程序静态链接到在 GpioClx 存根 （stub） 库中，Msgpioclxstub.lib DDI 入口点。 在运行时，此库执行必要的驱动程序版本协商以动态链接到 Msgpioclx.sys 中相应的入口点。

需要特定版本的 Msgpioclx.sys GPIO 控制器驱动程序可以安全地链接到具有更高版本的版本号的 Msgpioclx.sys 的版本。 但是，此驱动程序无法链接到 Msgpioclx.sys 具有较低版本号的版本。

## <a name="driver-registration"></a>驱动程序注册


若要注册为 GpioClx 的客户端，GPIO 控制器驱动程序调用[ **GPIO\_CLX\_RegisterClient** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nf-gpioclx-gpio_clx_registerclient)方法。 通常情况下，该驱动程序调用此方法从其[ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)例程。 在此调用，该驱动程序将注册数据包传递给方法。 此数据包包含一组的驱动程序实现事件回调函数的指针。 这些函数访问 GPIO 控制器设备中的硬件寄存器。 GpioClx 调用这些函数来处理 I/O 请求并管理中断。

GPIO 控制器驱动程序调用[ **GPIO\_CLX\_UnregisterClient** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nf-gpioclx-gpio_clx_unregisterclient)方法来取消 GpioClx 其注册。 通常情况下，该驱动程序调用此方法从其[ *EvtDriverUnload* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_unload)事件回调函数。

## <a name="device-object-initialization"></a>设备对象初始化


若要初始化 GpioClx，GPIO 控制器驱动程序必须调用中的两个 GpioClx 方法及其[ *EvtDriverDeviceAdd* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)回调函数。 第一种方法， [ **GPIO\_CLX\_ProcessAddDevicePreDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nf-gpioclx-gpio_clx_processadddevicepredevicecreate)，必须在调用之前调用[ **WdfDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicecreate)方法，用于创建设备对象。 第二种方法， [ **GPIO\_CLX\_ProcessAddDevicePostDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nf-gpioclx-gpio_clx_processadddevicepostdevicecreate)之后, 必须调用**WdfDeviceCreate**调用。

## <a name="interrupt-lock"></a>中断锁


大多数驱动程序实现事件回调函数调用仅在 IRQL = 被动\_GpioClx 的级别。 但是，以下列表中的回调函数将调用在被动\_级别或 DIRQL，具体取决于设备信息的[*客户端\_QueryControllerBasicInformation*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_query_controller_basic_information)回调函数为 GpioClx 提供了：

-   [*CLIENT\_ClearActiveInterrupts*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_clear_active_interrupts)
-   [*客户端\_MaskInterrupts*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_mask_interrupts)
-   [*CLIENT\_QueryActiveInterrupts*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_query_active_interrupts)
-   [*CLIENT\_QueryEnabledInterrupts*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_query_enabled_interrupts)
-   [*客户端\_UnmaskInterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_unmask_interrupt)

GpioClx，运行在 DIRQL 或被动中调用这些函数从中断服务例程 (ISR)\_级别，具体取决于是否 GPIO 控制器的硬件的寄存器内存映射。

*客户端\_QueryControllerBasicInformation*函数提供了设备中的窗体的信息[**客户端\_控制器\_BASIC\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/ns-gpioclx-_client_controller_basic_information)结构。 如果**MemoryMappedController**中设置标志位**标志**此结构的成员，GpioClx ISR 调用的回调函数 DIRQL 在上述列表中。 否则，在被动 ISR 调用的所有驱动程序实现回调函数\_级别。 有关此标志位的详细信息，请参阅[Interrupt-Related 回调](https://docs.microsoft.com/windows-hardware/drivers/gpio/interrupt-related-callbacks)。

GpioClx 会自动同步对运行在被动的驱动程序实现回调函数的调用\_级别并不能从 GpioClx ISR 调用 因此，这些函数之一可运行一次。 但是，GpioClx 不会自动同步这些被动\_具有从其 ISR.GpioClx 生成回调的级别回调 如果需要，GPIO 控制器驱动程序必须显式提供此类同步。

若要避免潜在的同步错误，GpioClx 实现*中断锁*的 GPIO 控制器驱动程序可以获取和释放。 主要由驱动程序的使用中断锁[*客户端\_EnableInterrupt* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_enable_interrupt)并[*客户端\_DisableInterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_disable_interrupt)回调函数。 驱动程序调用[ **GPIO\_CLX\_AcquireInterruptLock** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nf-gpioclx-gpio_clx_acquireinterruptlock)方法获取锁，以及调用[ **GPIO\_CLX\_ReleaseInterruptLock** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nf-gpioclx-gpio_clx_releaseinterruptlock)方法才能释放锁。 该驱动程序在被动调用回调函数的调用这些方法\_级别且不会从在 GpioClx ISR 调用。 该驱动程序持有锁，而不能运行 GpioClx ISR。 该驱动程序应只是暂时持有锁并且只有在执行关键操作，必须同步与 ISR

如果 GpioClx ISR 调用驱动程序实现回调函数，此函数则不需要获取 （或释放） 中断锁定因为 ISR 已经持有锁 （并将其释放）。 调用[ **GPIO\_CLX\_AcquireInterruptLock** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nf-gpioclx-gpio_clx_acquireinterruptlock)并[ **GPIO\_CLX\_ReleaseInterruptLock** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nf-gpioclx-gpio_clx_releaseinterruptlock)此函数的方法不起作用，但不是被视为错误。

 

 




