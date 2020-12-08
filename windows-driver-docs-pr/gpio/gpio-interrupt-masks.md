---
title: GPIO 中断掩码
description: 除了启用和禁用以外，配置为中断输入的常规用途 i/o (GPIO) pin。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cbefbf780da6775101fd3794c1a3547a918e8257
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96821501"
---
# <a name="gpio-interrupt-masks"></a>GPIO 中断掩码


除了启用和禁用以外，配置为中断输入的常规用途 i/o (GPIO) pin。

如果已启用并激活某个外设的已触发中断，但内核陷阱处理程序不能立即运行设备的中断服务例程 (ISR) 清除中断，则处理程序将在 GPIO pin 处屏蔽中断，以防止 pin 重复导致更多的中断。 以后，当 ISR 运行并清除中断后，就可以安全地取消屏蔽中断。

屏蔽中断不会清除或禁用中断。 如果已启用、处于活动状态且屏蔽中断，取消屏蔽此中断会导致 GPIO 控制器设备向处理器发出中断请求信号。

当 GPIO 中断处于禁用状态时，GPIO 中断掩码位不起作用。 [*客户端 \_ EnableInterrupt*](/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_enable_interrupt)回调函数将中断的掩码位设置为零; 即，在启用后，中断最初会被屏蔽。

屏蔽和禁用 GPIO 中断 pin 之间的重要区别在于掩码会保留 pin 的中断配置设置，而禁用 pin 则不会。 当 GPIO 中断 pin 被屏蔽时，它会将其以前编程的中断模式保留 (边缘触发或级别触发的) 、极性 (主动-高、主动-低或主动-两者) 和反应进行设置。 如果解除屏蔽中断，这些设置将立即生效。 但是，禁用中断后，所有 pin 中断配置设置都将丢失。 启用 pin 后，必须再次用所需的中断配置设置对其进行编程。

某些 GPIO 控制器在硬件中实现中断屏蔽寄存器，它们独立于中断启用寄存器。

但是，其他 GPIO 控制器提供了一组硬件寄存器，它们将中断掩码和中断启用功能组合在一起。 这些控制器的驱动程序会在软件中模拟单独的中断掩码和中断启用寄存器。 为此，这些驱动程序跟踪中断启用位和中断掩码位的逻辑状态，并操纵硬件寄存器中的相应位，以准确反映每个 GPIO 中断的组合逻辑中断启用和中断掩码位的行为。

 

