---
title: 将 GPIO 控制器分区为管脚库
description: 作为一个选项，驱动程序开发人员可以将常规用途 i/o （GPIO）控制器设备分为两个或多个 GPIO 端口块。
ms.assetid: D9425459-E052-48D8-A4F3-91387AE7059A
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0901bbbc43aa34f99d6bb0d3cb699d548ca0c294
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824922"
---
# <a name="partitioning-a-gpio-controller-into-banks-of-pins"></a>将 GPIO 控制器分区为管脚库


作为一个选项，驱动程序开发人员可以将常规用途 i/o （GPIO）控制器设备分为两个或多个 GPIO 端口块。 例如，gpio 控制器驱动程序可以将具有 64 GPIO pin 的 GPIO 控制器设备描述为两个 bank，其中每个都具有 32 GPIO pin。 开发人员可以提供单个驱动程序来管理 GPIO 控制器设备中的所有银行，此驱动程序通常使用一个设备对象来表示整个设备。 但是，可以独立于设备中的其他银行管理设备中的部分或全部银行。

通常，GPIO 控制器驱动程序出于以下原因之一，选择将 GPIO 控制器分区为两个或更多个 bank：

-   银行内 GPIO 引脚的电源状态可以独立于其他银行的 pin 进行管理。
-   GPIO 控制器中的引脚总数大于64。

GPIO framework 扩展（GpioClx）支持的最大银行大小为64个 pin。 包含64个以上的 pin 的 GPIO 控制器设备必须按驱动程序分区到两个或更多的 bank 中，其中每个都包含64个 pin。

若要确定 GPIO 控制器如何分区到银行，GpioClx 调用[*客户端\_QueryControllerBasicInformation*](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_query_controller_basic_information)事件回调函数。 此函数由 GPIO 控制器驱动程序实现，它提供了一个[**客户端\_控制器\_基本\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/ns-gpioclx-_client_controller_basic_information)结构，该结构描述 GPIO 控制器的特性和功能。 此结构的两个成员（ **TotalPins**和**NUMBEROFPINSPERBANK**）指定 GPIO 控制器中的 pin 如何分区到银行。 **TotalPins**指定 GPIO 控制器中的 pin 总数， **NumberOfPinsPerBank**指定每个银行的 pin 数目。 如果 N 是控制器中的银行数量，则这些银行的编号为0到 N-1。 除最后一个银行（即，银行号为 N –1）之外的所有银行都必须包含**NumberOfPinsPerBank**成员中指定的 pin 数目。 最后一个银行可以有任意数量的 pin，从一个到**NumberOfPinsPerBank**。

GpioClx 从**TotalPins**和**NumberOfPinsPerBank**成员的值确定 GPIO 控制器中的银行总数。 GpioClx 使用以下整数公式来计算银行总数：

（**TotalPins** + **NumberOfPinsPerBank** –1）/ **NumberOfPinsPerBank**在某些 GPIO 控制器设备中，可以打开设备中的 pin bank，或将其切换到同一个设备中的其他银行。 因此，当某个银行处于空闲状态时，可以将此银行切换到低功耗状态，以降低功率消耗。 为了容纳此类设备，GpioClx 支持[组件级电源管理](https://docs.microsoft.com/windows-hardware/drivers/kernel/component-level-power-management)。 GpioClx 定义了两个组件级别电源状态： F0 （完全打开）和 F1 （低功耗或关闭）。

若要确定 GPIO pin bank 是否支持组件级电源管理，GpioClx 将调用[*客户端\_QuerySetControllerInformation*](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_query_set_controller_information)事件回调函数。 此函数的*InputBuffer*参数是指向[**客户端\_控制器\_查询\_集\_信息\_输入**](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/ns-gpioclx-_client_controller_query_set_information_input)结构的指针。 若要请求电源管理信息，调用方将此结构的**RequestType**成员设置为**QueryBankPowerInformation**。

如果 GPIO 银行支持组件级电源管理，GpioClx 将在银行空闲时，转换为 F1 电源状态。 在银行进入 F1 状态之前，GpioClx 会调用[*客户端\_SaveBankHardwareContext*](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_save_bank_hardware_context)事件回调函数，告知驱动程序保存银行的硬件上下文（主要、寄存器内容）。 稍后，在银行进入 F0 状态后，GpioClx 将调用[*客户端\_RestoreBankHardwareContext*](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_restore_bank_hardware_context)事件回调函数，以告知驱动程序还原以前保存的硬件上下文。

 

 




