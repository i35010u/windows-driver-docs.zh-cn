---
title: 将 GPIO 控制器分区为管脚库
description: 驱动程序开发人员可以，作为一个选项，分区到两个或多个银行的 GPIO 插针的通用 I/O (GPIO) 控制器设备。
ms.assetid: D9425459-E052-48D8-A4F3-91387AE7059A
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a53a07d0450326ffdb2fda08c6eaeeeeef73fc89
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363570"
---
# <a name="partitioning-a-gpio-controller-into-banks-of-pins"></a>将 GPIO 控制器分区为管脚库


驱动程序开发人员可以，作为一个选项，分区到两个或多个银行的 GPIO 插针的通用 I/O (GPIO) 控制器设备。 例如，具有 64 GPIO 插针的 GPIO 控制器设备可以描述 GPIO 控制器驱动程序中，为两个银行，其中每个 32 GPIO 插针。 开发人员可以提供单个驱动程序管理的银行公会 GPIO 控制器设备，所有和此驱动程序通常使用一个设备对象来表示整个设备。 但是，部分或全部设备中银行可以独立于其他银行公会设备进行管理。

通常情况下，GPIO 控制器驱动程序将选择分区为两个或多个银行的 GPIO 控制器，出于以下原因之一：

-   可以独立于其他银行中的针管理 bank 中的 GPIO 插针的电源状态。
-   引脚 GPIO 控制器中的总数大于 64。

GPIO 框架扩展 (GpioClx) 支持的最大银行大小是 64 的 pin。 包含 64 个以上的引脚 GPIO 控制器设备必须将分区由驱动程序到两个或多个银行，其中每个包含不超过 64 pin。

若要确定 GPIO 控制器到银行的分区方式，GpioClx 调用[*客户端\_QueryControllerBasicInformation* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_query_controller_basic_information)事件回调函数。 此函数，由 GPIO 控制器驱动程序实现，提供[**客户端\_控制器\_BASIC\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/ns-gpioclx-_client_controller_basic_information)描述结构特性和功能的 GPIO 控制器。 此结构的两个成员**TotalPins**并**NumberOfPinsPerBank**，指定如何将 GPIO 控制器中的针分区到银行。 **TotalPins** GPIO 控制器中指定的 pin 的总数和**NumberOfPinsPerBank**指定的每个银行的 pin 的数量。 如果 N 是银行控制器中的数字，银行编号从 0 到 N-1。 除最后一个银行 （即，银行编号 N-1） 必须包含在指定的 pin 数**NumberOfPinsPerBank**成员。 最后一个银行可以有任意数量的插针从一到**NumberOfPinsPerBank**。

GpioClx 确定的 GPIO 控制器中的值中的银行总数**TotalPins**并**NumberOfPinsPerBank**成员。 GpioClx 使用下面的整数公式来计算的银行总数：

(**TotalPins** + **NumberOfPinsPerBank** – 1) / **NumberOfPinsPerBank**部分 GPIO 控制器设备，启用设备 pin 的银行或切换到独立于其他银行公会同一设备的低功率状态。 因此，当特定银行处于空闲状态，该银行可以切换到低功耗状态，以降低能耗。 为了适应此类设备，GpioClx 支持[组件级别电源管理](https://docs.microsoft.com/windows-hardware/drivers/kernel/component-level-power-management)。 GpioClx 定义两个组件级别的电源状态，F0 （完全启用） 和 F1 （低电源或关闭）。

若要确定的 GPIO 插针银行是否支持组件级别电源管理，GpioClx 调用[*客户端\_QuerySetControllerInformation* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_query_set_controller_information)事件回调函数。 *InputBuffer*的此函数的参数是指向指针[**客户端\_控制器\_查询\_设置\_信息\_输入**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/ns-gpioclx-_client_controller_query_set_information_input)结构。 请求电源管理信息，调用方集**RequestType**到此结构的成员**QueryBankPowerInformation**。

如果 GPIO bank 支持在组件级电源管理，GpioClx 银行处于空闲状态时，启用过渡到 F1 电源状态。 银行进入 F1 状态之前，调用 GpioClx [*客户端\_SaveBankHardwareContext* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_save_bank_hardware_context)告知驱动程序来保存硬件上下文 （主要，注册的事件回调函数内容） 的银行。 更高版本，该银行进入 F0 状态后，GpioClx 会调用[*客户端\_RestoreBankHardwareContext* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_restore_bank_hardware_context)事件回调函数，以告知要还原以前保存的硬件的驱动程序上下文。

 

 




