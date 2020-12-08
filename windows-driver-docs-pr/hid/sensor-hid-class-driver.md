---
title: 传感器 HID 类驱动程序
description: 'Windows 操作系统包含内置的传感器 HID 类驱动程序 ( # A0) 。'
keywords:
- HID 类驱动程序，传感器
- 传感器 HID 类驱动程序
- HID
- HID 协议
- 传感器驱动程序示例
- 传感器驱动程序，示例
- Windows 8 传感器驱动程序
- 传感器驱动程序，Windows 8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 66034e7143c1c449a1c15abed6886eb70b10ca15
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96820343"
---
# <a name="sensor-hid-class-driver"></a>传感器 HID 类驱动程序


从 Windows 8 开始，Windows 操作系统包含一个内置的传感器 HID 类驱动程序 ( # A0) ，该驱动程序支持使用 HID 传输进行通信的第11种传感器类型。

下面列出了受支持的传感器：

-   三维加速度
-   环境光线
-   环境温度
-   大气力度
-   罗盘三维
-   设备方向
-   陀螺仪3D
-   湿度
-   倾斜仪3D
-   状态
-   邻近帮助

下图描绘了从两个传感器应用程序向下和向下传递到硬件本身的两个传感器应用程序之间的数据流。

![客户端传感器体系结构](images/client-sensor-architecture.png)

## <a name="support-for-custom-sensors"></a>支持自定义传感器


除了前面的列表中介绍的十一个传感器，类驱动程序还支持自定义类。 此类允许传感器制造商集成前面列表中未找到的设备：例如，碳 monoxide 传感器。 自定义传感器将自身作为具有唯一属性的自定义设备提供给传感器 API。

## <a name="architecture-and-overview"></a>体系结构和概述


如果要为兼容的传感器创建固件，则需要对类驱动程序所支持的 i/o 模型有一个基本的了解。

-   传感器将功能报告或输入报告发送到 HID 类驱动程序。 为响应来自驱动程序的请求而发送功能报表。 此报表包含属性数据，包括传感器的更改敏感度设置、其报表间隔和报告状态。 输入报表根据请求发送或以异步方式发送以响应事件。 此报告包含实际的传感器数据。 例如，对于加速感应程序，报表包含 G 强制，沿 x、y 和 z 轴) 。
-   HID 类驱动程序将功能报告发送到传感器。 例如，当应用程序请求新的更改敏感度或报表间隔时，驱动程序会将这些值打包到功能报表，并使用此报表将请求发送到传感器的固件。

下图说明了 i/o 模型：

![i/o 模型](images/hid-sensor-stack.png)

## <a name="sample-report-descriptor"></a>示例报表描述符


如果你的传感器支持类驱动程序的本机七个类别之一，则其固件需要支持特定功能和输入报告。 功能报表包括传感器的当前报告状态、其状态、更改敏感度和报告间隔 (除了) 的其他可能属性。 输入报表包含传感器读数：对于开关，为 True 或 False，为环境光线传感器的加速感应器或 LUX 的值。

### <a name="sample-accelerometer-feature-report"></a>采样加速功能报表

下面的代码示例演示加速感应程序的 HID 功能报表。 请注意此报表的自描述性特性。 它包括最小值和最大值以及各个字段的计数和大小。

``` syntax
//feature reports (xmit/receive)
    HID_USAGE_PAGE_SENSOR,
    HID_USAGE_SENSOR_PROPERTY_REPORTING_STATE,
    HID_LOGICAL_MIN_8(0x00),                   //LOGICAL_MINIMUM (0) 
    HID_LOGICAL_MAX_8(0xFF),             //LOGICAL_MAXIMUM (255) 
    HID_REPORT_SIZE(8),
    HID_REPORT_COUNT(1),
    HID_FEATURE(Data_Var_Abs),

    HID_USAGE_SENSOR_PROPERTY_SENSOR_STATUS,
    HID_LOGICAL_MIN_8(0x00),                   //LOGICAL_MINIMUM (0) 
    HID_LOGICAL_MAX_8(0xFF),             //LOGICAL_MAXIMUM (255) 
    HID_REPORT_SIZE(8),
    HID_REPORT_COUNT(1),
    HID_FEATURE(Data_Var_Abs),

    HID_USAGE_SENSOR_PROPERTY_CHANGE_SENSITIVITY_ABS,
    HID_LOGICAL_MIN_8(0x00),                   //LOGICAL_MINIMUM (0) 
    HID_LOGICAL_MAX_16(0xFF,0xFF), //LOGICAL_MAXIMUM (65535) 
    HID_REPORT_SIZE(16),
    HID_REPORT_COUNT(1),
    HID_USAGE_SENSOR_UNITS_G,
    HID_UNIT_EXPONENT(0xE), 
    HID_FEATURE(Data_Var_Abs),

    HID_USAGE_SENSOR_PROPERTY_REPORT_INTERVAL,
    HID_LOGICAL_MIN_8(0x00),                   //LOGICAL_MINIMUM (0) 
    HID_LOGICAL_MAX_32(0xFF,0xFF,0xFF,0xFF), //LOGICAL_MAXIMUM (4294967295) 
    HID_REPORT_SIZE(32),
    HID_REPORT_COUNT(1),
    HID_USAGE_SENSOR_UNITS_MILLISECOND,
    HID_UNIT_EXPONENT(0), 
    HID_FEATURE(Data_Var_Abs),
```

### <a name="sample-accelerometer-input-report"></a>采样加速输入报告

下面的代码示例显示了同一设备的 HID 输入报告。 同样，请注意此报表中字段的自描述性特性。

``` syntax
//input reports (transmit)
    HID_USAGE_PAGE_SENSOR,
    HID_USAGE_SENSOR_STATE,
    HID_LOGICAL_MIN_8(0x00),                   //LOGICAL_MINIMUM (0) 
    HID_LOGICAL_MAX_8(0xFF),             //LOGICAL_MAXIMUM (255) 
    HID_REPORT_SIZE(8),
    HID_REPORT_COUNT(1),
    HID_INPUT(Data_Var_Abs),

    HID_USAGE_SENSOR_EVENT,
    HID_LOGICAL_MIN_8(0x00),                   //LOGICAL_MINIMUM (0) 
    HID_LOGICAL_MAX_8(0xFF),             //LOGICAL_MAXIMUM (255) 
    HID_REPORT_SIZE(8),
    HID_REPORT_COUNT(1),
    HID_INPUT(Data_Var_Abs),

    HID_USAGE_SENSOR_DATA_MOTION_ACCELERATION_X_AXIS,
    HID_LOGICAL_MIN_16(0x01,0x80),             //    LOGICAL_MINIMUM (-32767) 
    HID_LOGICAL_MAX_16(0xFF,0x7F),             //    LOGICAL_MAXIMUM (32767)
    HID_REPORT_SIZE(16), 
    HID_REPORT_COUNT(1), 
    HID_USAGE_SENSOR_UNITS_G,
    HID_UNIT_EXPONENT(0xE), 
    HID_INPUT(Data_Var_Abs),

    HID_USAGE_SENSOR_DATA_MOTION_ACCELERATION_Y_AXIS,
    HID_LOGICAL_MIN_16(0x01,0x80),             //    LOGICAL_MINIMUM (-32767) 
    HID_LOGICAL_MAX_16(0xFF,0x7F),             //    LOGICAL_MAXIMUM (32767)
    HID_REPORT_SIZE(16), 
    HID_REPORT_COUNT(1), 
    HID_USAGE_SENSOR_UNITS_G,
    HID_UNIT_EXPONENT(0xE), 
    HID_INPUT(Data_Var_Abs),

    HID_USAGE_SENSOR_DATA_MOTION_ACCELERATION_Z_AXIS,
    HID_LOGICAL_MIN_16(0x01,0x80),             //    LOGICAL_MINIMUM (-32767) 
    HID_LOGICAL_MAX_16(0xFF,0x7F),             //    LOGICAL_MAXIMUM (32767)
    HID_REPORT_SIZE(16), 
    HID_REPORT_COUNT(3), 
    HID_USAGE_SENSOR_UNITS_G,
    HID_UNIT_EXPONENT(0xE), 
    HID_INPUT(Data_Var_Abs),

    HID_USAGE_SENSOR_DATA_MOTION_INTENSITY,
    HID_LOGICAL_MIN_8(0x00),                   //LOGICAL_MINIMUM (0) 
    HID_LOGICAL_MAX_8(0xFF),             //LOGICAL_MAXIMUM (255) 
    HID_REPORT_SIZE(8),
    HID_REPORT_COUNT(1),
    HID_INPUT(Data_Var_Abs),
```

 

 




