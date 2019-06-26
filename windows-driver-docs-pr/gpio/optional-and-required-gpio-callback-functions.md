---
title: 可选和必需的 GPIO 回调函数
description: 通用 I/O (GPIO) 控制器驱动程序调用 GPIO_CLX_RegisterClient 方法以将注册为 GPIO 框架扩展 (GpioClx) 的客户端。
ms.assetid: 2F126431-13AB-4E3F-9E5E-56DC7D9AF024
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3f481b34385b8bdd6cf83bae94457477578307ba
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383415"
---
# <a name="optional-and-required-gpio-callback-functions"></a>可选和必需的 GPIO 回调函数


通用 I/O (GPIO) 控制器驱动程序调用[ **GPIO\_CLX\_RegisterClient** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nf-gpioclx-gpio_clx_registerclient)方法将注册为 GPIO 框架扩展 (GpioClx) 的客户端。 在此调用，驱动程序将注册数据包传递给 GpioClx 指定由驱动程序实现的事件回调函数的列表。 GpioClx 调用这些回调函数来配置 GPIO 控制器硬件、 执行 I/O 操作和管理中断。 GpioClx 需要 GPIO 控制器驱动程序，以实现特定的回调函数，但支持其他回调函数是可选的。

注册数据包[ **GPIO\_客户端\_注册\_数据包**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/ns-gpioclx-_gpio_client_registration_packet)结构。 如果 GPIO 控制器驱动程序实现特定的回调函数，它将函数指针写入该回调函数到此结构的相应成员。 或者，若要指示不支持特定的回调函数，该驱动程序将 NULL 写入相应的成员。

必须在注册包中包括以下回调函数：

[*客户端\_PrepareController*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_prepare_controller)
[*客户端\_QueryControllerBasicInformation* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_query_controller_basic_information) 
 [*客户端\_StartController*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_start_controller)
[*客户端\_StopController* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_stop_controller) 
 [*客户端\_ReleaseController* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_release_controller) （即，如果相应函数注册中的指针，上面的列表中的任何回调函数是否缺失数据包为 NULL）， **GPIO\_CLX\_RegisterClient**方法失败。

GPIO 控制器驱动程序不需要支持读取或写入到 I/O GPIO 插针，哪些是插针配置为数据输入或数据的输出。 （没有 I/O 端口使用的 GPIO 控制器可以仍然中继中断请求从外围设备。）但是，如果注册包包括以下 O 相关回调函数，该数据包必须包含两个以下的回调函数：

[*客户端\_ConnectIoPins*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_connect_io_pins)
[*客户端\_DisconnectIoPins* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_disconnect_io_pins)此外，如果注册数据包包括上面的列表中的两个回调函数，该驱动程序必须此外支持 GPIO I/O 插针，写入 GPIO I/O 的 pin，或同时从读取。 具体而言，注册数据包必须包含至少一个回调函数，下面的列表中：

[*客户端\_ReadGpioPins* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_read_pins)或[*客户端\_ReadGpioPinsUsingMask*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_read_pins_mask)
[*客户端\_WriteGpioPins* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_write_pins)或[*客户端\_WriteGpioPinsUsingMask* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_write_pins_mask)支持读取的驱动程序必须实现之一两个*客户端\_ReadGpioPins*Xxx 上述列表中的回调函数。 支持写入的驱动程序必须实现两种状态之一*客户端\_WriteGpioPins*Xxx 上述列表中的回调函数。

实现一个驱动程序*客户端\_ReadGpioPinsUsingMask*，*客户端\_WriteGpioPinsUsingMask*，或两者，必须设置**FormatIoRequestsAsMasks**中提供的设备信息的标志位[*客户端\_QueryControllerBasicInformation* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_query_controller_basic_information)回调函数。 实现一个驱动程序*客户端\_ReadGpioPins*，*客户端\_WriteGpioPins*，或两者，不能设置此标志位。 有关详细信息，请参阅的说明**标志**中的成员[**客户端\_控制器\_BASIC\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/ns-gpioclx-_client_controller_basic_information)。

GPIO 控制器驱动程序不需要支持 GPIO 中断。 但是，如果注册数据包中包含的任何以下与中断相关的回调函数，该数据包必须包括所有以下回调函数：

[*客户端\_EnableInterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_enable_interrupt)
[*客户端\_DisableInterrupt* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_disable_interrupt) 
 [ *客户端\_MaskInterrupts*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_mask_interrupts)
[*客户端\_QueryActiveInterrupts* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_query_active_interrupts) 
 [*客户端\_UnmaskInterrupt* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_unmask_interrupt)支持的屏蔽的中断的驱动程序必须实现*客户端\_MaskInterrupts*回调函数。 支持活动中断的查询的驱动程序必须实现*客户端\_QueryActiveInterrupts*回调函数。

[*客户端\_ClearActiveInterrupts* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_clear_active_interrupts)回调函数是一种特殊情况。 如果在读取时 GPIO 控制器硬件，会自动清除活动中断*客户端\_ClearActiveInterrupts*函数，则不需要和注册中的相应函数指针数据包应设置为 NULL。 但是，注册数据包中提供活动中断不会自动清除它们在读取时，如果和前面的列表中的中断相关的回调函数*客户端\_ClearActiveInterrupts*函数必须包含在数据包。 若要指示硬件自动清除活动中断，它们在读取时，该驱动程序集**ActiveInterruptsAutoClearOnRead**中提供的设备信息的标志位[ *客户端\_QueryControllerBasicInformation* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_query_controller_basic_information)回调函数。 有关详细信息，请参阅的说明**标志**中的成员[**客户端\_控制器\_BASIC\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/ns-gpioclx-_client_controller_basic_information)。

如果 GPIO 控制器驱动程序支持 GPIO 中断，注册数据包可以作为一个选项，包括以下回调函数：

[*客户端\_QueryEnabledInterrupts* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_query_enabled_interrupts) GpioClx 支持*客户端\_QueryEnabledInterrupts*函数从 Windows 8.1。

支持的驱动程序[组件级别电源管理](https://docs.microsoft.com/windows-hardware/drivers/kernel/component-level-power-management)必须实现两个以下的回调函数：

[*客户端\_RestoreBankHardwareContext*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_restore_bank_hardware_context)
[*客户端\_SaveBankHardwareContext* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_save_bank_hardware_context)表示硬件支持的驱动程序集的组件级电源管理**BankIdlePowerMgmtSupported**中提供的设备信息的标志位[*客户端\_QueryControllerBasicInformation* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_query_controller_basic_information)回调函数。 有关详细信息，请参阅的说明**标志**中的成员[**客户端\_控制器\_BASIC\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/ns-gpioclx-_client_controller_basic_information)。

[*客户端\_PreProcessControllerInterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_pre_process_controller_interrupt)， [*客户端\_ReconfigureInterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_reconfigure_interrupt)，和[*客户端\_ControllerSpecificFunction* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_controller_specific_function)回调函数是可选的受 GpioClx 解决一些 GPIO 控制器中的特定于硬件的问题实现。 仅 GPIO 控制器驱动程序具有特殊需求实现这些功能。

 

 




