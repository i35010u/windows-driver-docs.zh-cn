---
title: 通过 I2C 的 HID 简介
description: 对于 Windows 8, Microsoft 创建了一个新的 HID 微型端口驱动程序, 该驱动程序允许设备通过集成线路 (I i2c) 总线进行通信。
ms.assetid: E8A056C0-B10F-48E2-B8E3-67B00AAC87D8
keywords:
- HID 微型端口驱动程序
- 集成线路
- I2C 总线
- HIDI2C.sys
- 简单外围总线
- SPB
- GPIO
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: af265af5a99022b0472d5429f5c2e35d49c3c84d
ms.sourcegitcommit: fec48fa5342d9cd4cd5ccc16aaa06e7c3d730112
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2019
ms.locfileid: "69565621"
---
# <a name="introduction-to-hid-over-i2c"></a>通过 I2C 的 HID 简介


对于 Windows 8, Microsoft 创建了一个新的 HID 微型端口驱动程序, 该驱动程序允许设备通过集成线路 (I i2c) 总线进行通信。

新的 HID 微型端口解决方案扩展了除 USB 和蓝牙之外的 HID 协议, 以支持 i2c 设备。 I i2c 是一个简单而有效的协议, 在手机和嵌入式平台上过去十多年使用。 Windows 8 通过名为 HIDI2C 的内置 KMDF 驱动程序支持此协议。

这是对收件箱驱动程序中的对 I-I 以上组合的支持, 允许硬件制造商使其设备在 windows 上快速运行, 而无需创建驱动程序。

为了确保具有多个 ACPI 资源的系统上的行为正确, 必须首先显示以下两个资源:

-   HID I i2c 连接
-   设备中断

定义这些资源后, 可以遵循其他类型的其他 ACPI 资源。

*重要说明:*

-   目前, HID I i2c 驱动程序针对支持简单外围总线 (SPB) 和 GPIO 的 SoC 系统。 将来, Microsoft 可能会在非 SoC 系统上支持此驱动程序。
-   HID I i2c 驱动程序经过优化, 可支持所有 HID 客户端。
-   使用 HID I i2c 驱动程序, 设备和系统制造商可以减少他们为了支持常见设备类型 (例如键盘、触摸板、触摸屏、传感器等) 而要开发的驱动程序总数。
-   HID I i2c 驱动程序在 Windows 的所有客户端 Sku 上都可用, 并包含在 WinPE 中。

 

 




