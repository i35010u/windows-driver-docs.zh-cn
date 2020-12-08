---
title: 修改示例以支持另一个传感器
description: 修改示例以支持另一个传感器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 89ebf7856d0ec6b109ff77d0e70fec51fa4b722e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812295"
---
# <a name="modify-the-sample-to-support-another-sensor"></a>修改示例以支持另一个传感器


SpbAccelerometer 示例演示如何为 ADXL345 加速感应程序编写驱动程序。 如果你的驱动程序支持单个传感器 (这不是加速感应器) ，你将修改或替换以下文件和功能：

| 文件                    | 修订                                                                                                                                                                                                                                                                                                                                                                             |
|-------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| SpbAccelerometer.inx    | 重命名文件。 更新设备名称字符串以反映设备的名称。  (搜索和替换 "SPB 加速感应" 和 "SpbAccelerometer" 的实例。 ) 确保 INF 文件中的硬件标识符包含 "ACPI" 字符串。                                                                                                                                      |
| SpbAccelerometer. asl    | 重命名文件。 更新 \_ CRS 部分，使其指定设备所需的 I2C 和 GPIO 资源。                                                                                                                                                                                                                                                                    |
| Adxl345               | 重命名文件。 如果设备类似于 ADXL345，并且支持一组注册和相应的读取和写入操作，请修改此文件，使其映射到设备支持的寄存器和操作。 如果设备不支持寄存器或读/写操作，请删除此文件。                                                             |
| AccelerometerDevice   | 重命名文件。 将对应于特定 ADXL345 功能的私有方法替换为与设备上的功能相对应的方法。 例如，如果你的设备未使用寄存器和中断，请替换 ReadRegister、WriterRegister 和 ConnectInterrupt 方法。 替换不再反映设备功能的私有成员。 |
| AccelerometerDevice .cpp | 重命名文件。 从头文件中删除要提取的方法，并为与设备功能对应的新方法插入定义。                                                                                                                                                                                                                  |

 

 

 




