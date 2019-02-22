---
title: HID I2C 转移
description: 对于 Windows 8 中，Microsoft 创建新的 HID 微型端口驱动程序允许设备通过 Inter-Integrated 线路 (I²C) 总线进行通信。
ms.assetid: E8A056C0-B10F-48E2-B8E3-67B00AAC87D8
keywords:
- HID 微型端口驱动程序
- 间集成的线路
- I2C 总线
- HIDI2C.sys
- 简单的外围总线
- SPB
- GPIO
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 06a6a6e5869eb5c95eff5bb6f5449e31d07ac975
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547089"
---
# <a name="hid-over-i2c"></a>HID I2C 转移


对于 Windows 8 中，Microsoft 创建新的 HID 微型端口驱动程序允许设备通过 Inter-Integrated 线路 (I²C) 总线进行通信。

新的 HID 微型端口解决方案将扩展的 HID 协议，超出 USB 和蓝牙，以支持 I²C 设备。 I²C 是一种简单但有效的协议和过去的十年电话和嵌入式的平台中使用的。 此协议名为 HIDI2C.sys 现成 KMDF 驱动程序支持在 Windows 8 中。

通过 HID I²C 收件箱驱动程序，在此组合的支持实现硬件制造商以获取其运行的设备快速在 windows 上不需要创建一个驱动程序。

为了确保在 ACPI 的多个资源的系统上的正确行为，以下两个资源必须首先出现：

-   HID 的 I²C 连接
-   设备中断

这些资源定义后，可能会按照 ACPI 中的其他资源，其他类型。

*重要说明：*

-   今天，HID I²C 驱动程序以目标支持简单外围总线 （存储） 和 GPIO 的 SoC 系统。 将来，Microsoft 可能会在非 SoC 系统上支持此驱动程序。
-   HID I²C 驱动程序经过优化，可支持所有隐藏客户端。
-   HID I²C 驱动程序，设备和系统制造商可以减少总的驱动程序开发以支持常见设备类型，如键盘、 触摸板，它们具有触摸屏幕、 传感器和等等。
-   HID I²C 驱动程序可在所有客户端 Sku 的 Windows 上，并包含在 WinPE 中。

 

 




