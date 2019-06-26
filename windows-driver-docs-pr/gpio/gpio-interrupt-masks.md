---
title: GPIO 中断掩码
description: 因为中断输入可能是屏蔽和解除屏蔽除了启用和禁用配置的通用 I/O (GPIO) 插针。
ms.assetid: FD6537DA-2AAA-4646-896D-D5BC834526B6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: da6e0e04a2a6dc3741bf168f267f4fce59175af8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383418"
---
# <a name="gpio-interrupt-masks"></a>GPIO 中断掩码


因为中断输入可能是屏蔽和解除屏蔽除了启用和禁用配置的通用 I/O (GPIO) 插针。

如果从外围设备的级别触发中断已启用并处于活动状态，但内核的陷阱处理程序不能立即运行设备的中断服务例程 (ISR) 若要清除中断，则处理程序会屏蔽在 GPIO 插针，以防止 pin 中断从重复导致更多的中断。 稍后，ISR 运行并清除中断后，你可以安全地解除屏蔽中断。

屏蔽中断不会清除或禁用中断。 如果启用了 GPIO 中断，处于活动状态，并屏蔽，unmasking 此中断导致 GPIO 控制器设备，以指示对处理器的中断请求。

GPIO 中断掩码位禁用 GPIO 中断时，没有任何影响。 [*客户端\_EnableInterrupt* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_enable_interrupt)回调函数设置为零的中断的位掩码; 即，中断为最初未屏蔽后启用它。

屏蔽和禁用 GPIO 中断 pin 之间的重要区别是屏蔽保留 pin 的中断配置设置，而禁用 pin 却没有。 虽然 GPIO 中断 pin 被屏蔽，它将保留其以前通过编程方式设置的中断模式下 （edge 触发或级别触发），极性 （主动高、 活动性低，或同时处于活动状态），并 debounce 设置。 这些设置才会生效再次立即中断已取消屏蔽。 但是，当禁用中断时，所有插针的中断配置设置都会丢失。 启用 pin 后，它必须进行编程，再次使用所需的中断的配置设置。

一些 GPIO 控制器中的硬件，实现彼此独立，截然不同中断启用寄存器的中断掩码寄存器。

但是，其他 GPIO 控制器提供一组将中断掩码和中断启用函数组合使用硬件寄存器。 这些控制器的驱动程序模拟软件中的单独中断掩码和中断启用寄存器。 若要执行此操作，这些驱动程序将跟踪中断启用 bits 和中断掩码位的逻辑状态和操作以准确地反映组合的逻辑中断启用和中断掩码的行为的硬件寄存器中的相应位每个 GPIO 中断的位。

 

 




