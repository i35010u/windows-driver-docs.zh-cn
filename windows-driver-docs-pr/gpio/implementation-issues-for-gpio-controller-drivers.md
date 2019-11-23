---
title: GPIO 控制器驱动程序的实现问题
description: GPIO framework 扩展（GpioClx）提供了一个灵活的设备驱动程序接口（DDI）。
ms.assetid: 303A6034-7ED7-4C21-86E5-076383AF3A5B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 39d7af056020240b3e89bacc13fcd3358a383ae2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824957"
---
# <a name="implementation-issues-for-gpio-controller-drivers"></a>GPIO 控制器驱动程序的实现问题


GPIO framework 扩展（GpioClx）提供了一个灵活的设备驱动程序接口（DDI）。 此 DDI 使开发人员能够在备用回调接口之间进行选择。 驱动程序开发人员应该实现最适合目标 GPIO 控制器设备硬件体系结构的一组事件回调函数。

例如，如果 GPIO 控制器驱动程序支持读取和写入 GPIO i/o 引脚，开发人员可以选择实现以下一对回调函数：

[*客户端\_ReadGpioPins*](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_read_pins)和[*客户端\_WriteGpioPins*](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_write_pins)
[*客户端\_ReadGpioPinsUsingMask*](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_read_pins_mask)和[*客户端\_WriteGpioPinsUsingMask*](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_write_pins_mask) *客户端\_ReadGpioPins*和*客户端*\_WriteGpioPins 函数接收银行号码、GPIO pin 编号的数组和用于读取或写入到这些 pin 的位值的数据缓冲区。 如果在读或写操作中通常只访问少量的 GPIO pin，则这对回调可能会产生最佳实现。 此实现通常用于其硬件寄存器未进行内存映射的 GPIO 控制器。 但是，如果在读取或写入操作过程中可能会访问多个 GPIO pin，或者如果 GPIO 控制器硬件能够有效地以并行方式访问多个 GPIO pin，则另一对回调函数可能会产生更好的实现。

*客户端\_ReadGpioPinsUsingMask*和*客户端\_WriteGpioPinsUsingMask*回调函数可以在一次调用中读取或写入最多64针的银行。 *客户端\_ReadGpioPinsUsingMask*函数将 GPIO pin 值读入64位掩码。 *客户端\_WriteGpioPinsUsingMask*函数使用 2 64 位掩码。 一个掩码指示要设置的 GPIO pin，另一个掩码指示要清除的 GPIO pin。 此实现通常用于内存映射的 GPIO 控制器。

 

 




