---
title: GPIO 控制器驱动程序的实现问题
description: GPIO 框架扩展 (GpioClx) 提供了灵活的设备驱动程序接口 (DDI)。
ms.assetid: 303A6034-7ED7-4C21-86E5-076383AF3A5B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0d598c4cead43a200638525c5370333ba7fd5786
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519924"
---
# <a name="implementation-issues-for-gpio-controller-drivers"></a>GPIO 控制器驱动程序的实现问题


GPIO 框架扩展 (GpioClx) 提供了灵活的设备驱动程序接口 (DDI)。 此 DDI 使开发人员能够在备用回调接口之间进行选择。 驱动程序开发人员应实现最适合于目标 GPIO 控制器设备的硬件体系结构的事件回调函数集。

例如，如果 GPIO 控制器驱动程序支持读取和写入 I/O GPIO 插针，开发人员可以选择实现一个回调函数的以下对：

[*客户端\_ReadGpioPins* ](https://msdn.microsoft.com/library/windows/hardware/hh439404)并[*客户端\_WriteGpioPins*](https://msdn.microsoft.com/library/windows/hardware/hh439439)
[*客户端\_ReadGpioPinsUsingMask* ](https://msdn.microsoft.com/library/windows/hardware/hh439406)并[*客户端\_WriteGpioPinsUsingMask* ](https://msdn.microsoft.com/library/windows/hardware/hh439445) *客户端\_ReadGpioPins*并*客户端\_WriteGpioPins*函数接收银行编号、 GPIO pin 数字数组和位值的数据缓冲区以读取或写入到这些引脚。 如果只有少量的 GPIO 插针通常访问的读取或写入操作中，这两个回调可能会产生最佳的实现。 通常使用此实现的 GPIO 控制器的硬件注册不是内存映射。 但是，如果在进行读访问或写入操作，可能会多个 GPIO 插针或 GPIO 控制器硬件可以有效地访问多个并行的 GPIO 插针，其他对回调函数可能会产生更好地实现。

*客户端\_ReadGpioPinsUsingMask*并*客户端\_WriteGpioPinsUsingMask*读取或写入为最多 64 个插针的插槽中一次调用回调函数。 *客户端\_ReadGpioPinsUsingMask*函数将 GPIO 的 pin 值读取到 64 位掩码。 *客户端\_WriteGpioPinsUsingMask*函数使用两个 64 位掩码。 一个屏蔽，指示哪些 GPIO 插针，以设置，和其他屏蔽，指示其 GPIO 固定清除。 此实现通常用于内存映射 GPIO 控制器。

 

 




