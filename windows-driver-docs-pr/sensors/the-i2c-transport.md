---
title: I2C 传输
description: I2C 传输
ms.assetid: A483FAA6-9FA6-4C91-B8D4-021DDBB9B869
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8fab1188baaeeb4f558618ccd3914d4f31489c79
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63345068"
---
# <a name="i2c-transport"></a>I2C 传输


| 模块                  | 类/接口      |
|-------------------------|----------------------|
| AccelerometerDevice.cpp | CAccelerometerDevice |
| Adxl345.h               | 不可用                  |

 

I²C (间 IC) 传输协议是由其使用者产品 Phillips Corporation 引入了两条串行传输。 传感器是设备的支持此传输的一个类别。 示例包括：

-   ADXL345 加速感应器
-   HMC5883L 指南针
-   MS5611 01BA03 大气压力传感器
-   TMP100 温度传感器

I2C 总线上的两条电线对应于时钟行 (SCL) 和串行数据行 (SDA)。 I2C 传输有关的详细信息，请参阅 I2C 总线规范。

传感器通常支持 I2C 传输的支持寄存器的组。 在主机使用这些寄存器来配置和控制将从设备。 对于 ADXL345，寄存器对应于特定设备属性、 功能或功能。 一些寄存器是只读的;其他用户均可读/写。 例如，注册 0x2D (POWER\_CTL) 允许在主机上传感器设置自动睡眠模式下，此模式下处于非活动状态一段时间后将设备设置为低功耗状态。 （有关详细了解 ADXL345s 注册和命令，请参阅制造商的数据表）。

示例驱动程序具有一个方法，将值写入到给定的注册 (**CAcclelerometerDevice::WriteRegister**)，另一个寄存器中读取值 (**CAccelerometerDevicce::ReadRegister**)。 这些值，数据缓冲区将标识正在写入到的寄存器 （或从读取） 的参数、 指向要写入的数据或读取和缓冲区长度。

例如，以下一系列**WriteRegister**并**ReadRegister**调用发生在驱动程序和设备的初始化过程中。 该驱动程序调用**WriteRegister**配置传感器。 如果操作成功， **ReadRegister**反映之前编写的值的内容返回。

方法注册数据用途**CAccelerometerDevice::WriteRegister** 0x2d\\0 (0x00) 重置传感器的电源控制寄存器中，并将设备放在备用服务器模式。
**CAccelerometerDevice::ReadRegister** 0x2d\\0 (0x00) 设备已放入备用服务器模式。
**CAccelerometerDevice::WriteRegister** 0x31\\v (0x0b) 在每个轴的 + /-16 G 范围的高分辨率模式下设置设备。
**CAccelerometerDevice::ReadRegister** 0x31\\v (0x0b) 高分辨率设置 （+ /-16 G) 的最大范围。
. . .
. . .
. . .
 

加速感应器的完整注册映射是设备的数据工作表的表 16 中。 示例驱动程序支持这些寄存器的子集。 Adxl345.h 标头文件中找到这些支持的值：

```cpp
//
// Register interface
//

#define ADXL345_DEVID                       0x00
#define ADXL345_THRESH_TAP                  0x1D
#define ADXL345_OFFSET_X                    0x1E
#define ADXL345_OFFSET_Y                    0x1F
#define ADXL345_OFFSET_Z                    0x20
#define ADXL345_DURATION_TAP                0x21
#define ADXL345_LATENT_TAP                  0x22
#define ADXL345_WINDOW_TAP                  0x23
#define ADXL345_THRESH_ACT                  0x24
#define ADXL345_THRESH_INACT                0x25
#define ADXL345_TIME_INACT                  0x26
#define ADXL345_ACT_INACT_CTL               0x27
#define ADXL345_THRESH_FF                   0x28
#define ADXL345_TIME_FF                     0x29
#define ADXL345_TAP_AXES                    0x2A
#define ADXL345_ACT_TAP_STATUS              0x2B
#define ADXL345_BW_RATE                     0x2C
#define ADXL345_POWER_CTL                   0x2D
#define ADXL345_INT_ENABLE                  0x2E
#define ADXL345_INT_MAP                     0x2F
#define ADXL345_INT_SOURCE                  0x30
#define ADXL345_DATA_FORMAT                 0x31
#define ADXL345_DATA_X0                     0x32
#define ADXL345_DATA_X1                     0x33
#define ADXL345_DATA_Y0                     0x34
#define ADXL345_DATA_Y1                     0x35
#define ADXL345_DATA_Z0                     0x36
#define ADXL345_DATA_Z1                     0x37
#define ADXL345_FIFO_CTL                    0x38
#define ADXL345_FIFO_STATUS                 0x39
```

 

 




