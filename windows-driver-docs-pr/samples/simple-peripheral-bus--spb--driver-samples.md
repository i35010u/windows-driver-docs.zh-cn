---
title: 简单外设总线 (SPB) 驱动程序示例
description: 此目录中的驱动程序示例编写你的设备的自定义存储驱动程序提供一个起始点。
ms.assetid: E9A667EA-3AE5-4A0E-BC3F-CD442141886B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 691244e8d41c104439b91219e148116edb0d0707
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366291"
---
# <a name="simple-peripheral-bus-spb-driver-samples"></a>简单外设总线 (SPB) 驱动程序示例


此目录中的驱动程序示例编写你的设备的自定义存储驱动程序提供一个起始点。

## <a name="simple-peripheral-bus-spb"></a>简单外设总线 (SPB)


| 示例名称                | 解决方案                                                       | 描述                                                                                                                                                                                                                                                                                                                                                                   |
|----------------------------|----------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 主干 I2C 示例驱动程序 | [SkeletonI2C](https://go.microsoft.com/fwlink/p/?LinkId=617969) | 演示如何设计的简单外围总线 （存储） 设备驱动程序接口 (DDI) 符合 Windows KMDF 控制器驱动程序。 存储是低速度串行总线 （例如，I2C 和 SPI），而无需了解基础总线硬件或设备连接的跨平台使用允许外围设备驱动程序开发的抽象。 |
| SpbTestTool                | [SpbTestTool](https://go.microsoft.com/fwlink/p/?LinkId=617970) | 演示如何打开的句柄[存储控制器](https://docs.microsoft.com/windows-hardware/drivers/spb/spb-controller-drivers)、 使用 KMDF 驱动程序，从存储接口和使用 GPIO[被动等级中断](https://docs.microsoft.com/windows-hardware/drivers/wdf/supporting-passive-level-interrupts)。                                                 |










