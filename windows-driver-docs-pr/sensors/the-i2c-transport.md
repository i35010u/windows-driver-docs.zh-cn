---
title: I2C 传输
description: I2C 传输
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5cdbcf0604f8131d927cb9480609b4773b6893b4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96805053"
---
# <a name="i2c-transport"></a>I2C 传输


| 模块                  | 类/接口      |
|-------------------------|----------------------|
| AccelerometerDevice .cpp | CAccelerometerDevice |
| Adxl345               | 空值                  |

 

I-C (IC) 传输是一种由梅花公司为其使用者产品引入的双线路串行传输。 传感器是一类支持此传输的设备。 示例包括：

-   ADXL345 加速感应
-   HMC5883L 罗盘
-   MS5611-01BA03 大气压力传感器
-   TMP100 温度传感器

I2C 总线上的两条线路对应于一个时钟行 (SCL) ，以及一个串行数据行 (SDA) 。 有关 I2C 传输的详细信息，请参阅 I2C 总线规范。

支持 I2C 传输的传感器通常支持一组寄存器。 主节点使用这些寄存器来配置和控制从属设备。 对于 ADXL345，寄存器对应于特定设备属性、功能或功能。 某些寄存器是只读的;其他是可读/写的。 例如，将0x2D 注册 (POWER \_ CTL) 使主节点设置传感器上的自动休眠模式—此模式将设备设置为在特定时间内处于不活动状态的低功率状态。  (有关 ADXL345s 注册和命令的详细信息，请参阅制造商的数据表。 ) 

示例驱动程序提供了一种方法，该方法将值写入给定寄存器 (**CAcclelerometerDevice：： WriteRegister**) ，另一种方法将寄存器中的值 (**CAccelerometerDevicce：： ReadRegister**) 。 它们采用用于标识要写入的寄存器的参数 (或从) 读取、指向要写入或读取的数据的指针以及数据缓冲区的缓冲区长度。

例如，以下 **WriteRegister** 和 **ReadRegister** 调用序列发生在驱动程序和设备初始化过程中。 驱动程序调用 **WriteRegister** 来配置传感器。 如果操作成功，则 **ReadRegister** 将返回反映以前写入的值的内容。

方法寄存器 Data 目的 **CAccelerometerDevice：： WriteRegister** 0x2d " \\ 0" (0X00) 重置传感器的电源控制寄存器，并将设备置于待机模式。
**CAccelerometerDevice：： ReadRegister** 0x2d " \\ 0" (0x00) 设备已置于备用模式。
**CAccelerometerDevice：： WriteRegister** 0x31 " \\ v" (0x0b) 将设备设置为完全分辨率模式，每个轴上的 +/-16G。
**CAccelerometerDevice：： ReadRegister** 0x31 " \\ v" () 0x0b 已设置最大范围 (+/-16G) 。
. . .
. . .
. . .
 

加速感应的完整注册图位于设备数据表的表16中。 示例驱动程序支持部分寄存器。 可在 Adxl345 头文件中找到这些支持的值：

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

 

 




