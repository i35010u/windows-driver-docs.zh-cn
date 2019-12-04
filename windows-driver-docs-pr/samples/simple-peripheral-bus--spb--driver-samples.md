---
title: 简单外设总线 (SPB) 驱动程序示例
description: 此目录中的驱动程序示例提供了为设备编写自定义 SPB 驱动程序的起点。
ms.assetid: E9A667EA-3AE5-4A0E-BC3F-CD442141886B
ms.date: 11/21/2019
ms.localizationpriority: medium
ms.openlocfilehash: 08b3a11fec5f6c4ebae4c842f25dc09c462c9292
ms.sourcegitcommit: 30fa63ad13fd5e2e883b76a44f0703e01049ffa1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2019
ms.locfileid: "74735183"
---
# <a name="simple-peripheral-bus-spb-driver-samples"></a>简单外设总线 (SPB) 驱动程序示例

此目录中的驱动程序示例提供了为设备编写自定义 SPB 驱动程序的起点。

| 示例 | 描述 |
| --- | --- |
| [主干 I2C 示例驱动程序](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/skeleton-i2c-sample-driver) | 演示如何设计符合简单外围总线（SPB）设备驱动程序接口（DDI）的适用于 Windows 的 KMDF 控制器驱动程序。 SPB 是用于实现跨平台使用的低速串行总线（例如 I2C 和 SPI）的抽象，无需了解底层总线硬件或设备连接。 |
| [SpbTestTool](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/spbtesttool) | 演示如何打开[spb 控制器](https://docs.microsoft.com/windows-hardware/drivers/spb/spb-controller-drivers)的句柄，使用 KMDF 驱动程序中的 SPB 接口，并使用 GPIO[被动级中断](https://docs.microsoft.com/windows-hardware/drivers/wdf/supporting-passive-level-interrupts)。 |
