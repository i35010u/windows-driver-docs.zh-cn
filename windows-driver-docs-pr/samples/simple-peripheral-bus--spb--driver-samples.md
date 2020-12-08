---
title: 简单外设总线 (SPB) 驱动程序示例
description: 此目录中的驱动程序示例提供了为设备编写自定义 SPB 驱动程序的起点。
ms.date: 11/21/2019
ms.localizationpriority: medium
ms.openlocfilehash: c7b3f016838d3b1b2fb32afedabd457b73afa60a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96831169"
---
# <a name="simple-peripheral-bus-spb-driver-samples"></a>简单外设总线 (SPB) 驱动程序示例

此目录中的驱动程序示例提供了为设备编写自定义 SPB 驱动程序的起点。

| 示例 | 说明 |
| --- | --- |
| [主干 I2C 示例驱动程序](/samples/microsoft/windows-driver-samples/skeleton-i2c-sample-driver) | 演示如何为 Windows 设计 KMDF 控制器驱动程序，该驱动程序符合) 设备驱动程序接口 (DDI) 中的简单外围总线 (SPB。 SPB 是低速串行总线的抽象 (例如，I2C 和 SPI) ，它允许为跨平台使用开发外围设备驱动程序，而无需了解底层总线硬件或设备连接。 |
| [SpbTestTool](/samples/microsoft/windows-driver-samples/spbtesttool) | 演示如何打开 [spb 控制器](../spb/spb-controller-drivers.md)的句柄，使用 KMDF 驱动程序中的 SPB 接口，并使用 GPIO [被动级中断](../wdf/supporting-passive-level-interrupts.md)。 |
