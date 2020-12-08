---
title: 主要和次要中断
description: GPIO 中断处理本质上是一个两阶段过程。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0f9502fc391187fcbf1edff6965419021dcb771e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96827201"
---
# <a name="primary-and-secondary-interrupts"></a>主要和次要中断


GPIO 中断处理本质上是一个两阶段过程。 从常规用途 i/o (GPIO) 控制器的中断会导致 GPIO framework 扩展 (GpioClx) 中断服务例程 (ISR) 运行，被称为 *主中断*。 此 ISR 将中断的 GPIO pin 映射到全局系统中断 (GSI) ，并将此 GSI 传递到硬件抽象层 (HAL) 。 HAL 通过此 GSI 生成一个 *辅助中断* ，以运行通过逻辑方式连接到 GPIO pin 的第二个 ISR。 此过程显示在 [GPIO 驱动程序支持概述](./gpio-driver-support-overview.md)的关系图中。

GpioClx 实现 ISR 来服务中断请求，GPIO 控制器通过使用配置为中断输入的 GPIO pin 接收该请求。 当外围设备在 gpio pin 上断言中断，并且在 GPIO 控制器中启用并取消阻止中断时，GPIO 控制器硬件会对处理器断言中断。 为响应此中断，GpioClx 中的 ISR 会查询 GPIO 控制器以标识生成中断的 GPIO pin，然后确定分配给此 pin 的 GSI。 GpioClx ISR 将此 GSI 传递到 HAL，HAL 调用以逻辑方式连接到 GSI 的 ISR。

通常，此第二个 ISR 属于外围设备的驱动程序，该驱动程序已在 GPIO pin 上断言中断。 有关外围设备驱动程序如何以逻辑方式将其 ISR 连接到 GPIO 中断 pin 的信息，请参阅 [基于 gpio 的中断资源](./gpio-based-interrupt-resources.md)。

 

