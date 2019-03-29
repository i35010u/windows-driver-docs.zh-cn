---
title: 传感器 HID 类驱动程序
description: Windows 操作系统包含内置传感器 HID 类驱动程序 (SensorsHIDClassDriver.dll)。
ms.assetid: F43958F0-5AFD-40E9-A583-FAA25F8C1B7D
keywords:
- 传感器的 HID 的类驱动程序
- 传感器 HID 类驱动程序
- HID
- HID 的协议
- 传感器驱动程序示例
- 传感器驱动程序示例
- Windows 8 传感器驱动程序
- 传感器驱动程序，Windows 8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b5edeb20dbe097552c3c96b03f3f925c271d7238
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568570"
---
# <a name="sensor-hid-class-driver"></a>传感器 HID 类驱动程序


Windows 操作系统从 Windows 8 开始，包括支持十一种类型的传感器，使用 HID 传输进行通信的内置传感器 HID 类驱动程序 (SensorsHIDClassDriver.dll)。

下面是一个受支持的传感器列表：

-   Accelerometer 3D
-   环境光线
-   环境温度
-   大气压力
-   Compass 3D
-   设备方向
-   陀螺仪 3D
-   湿度
-   倾斜仪 3D
-   状态
-   邻近感应

下图描绘了来回从两个传感器应用程序的数据流下通过驱动程序堆栈和，最后，对硬件本身。

![客户端传感器体系结构](images/client-sensor-architecture.png)

## <a name="support-for-custom-sensors"></a>对自定义传感器的支持


除了前面列表中所述的 11 个传感器类驱动程序还支持自定义类。 此类允许传感器制造商联系，以将前面的列表中找不到设备的集成：例如，一氧化碳传感器。 自定义传感器将自己呈现到传感器 API 为自定义设备具有唯一属性。

## <a name="architecture-and-overview"></a>体系结构和概述


如果要创建兼容传感器的固件，将需要支持的类驱动程序的 I/O 模型的一个基本的了解。

-   传感器 HID 类驱动程序中向功能报表或输入的报表。 从驱动程序的请求响应中发送功能报告。 此报表包含属性数据包括传感器的变化敏感度设置、 其报告间隔，以及其报告的状态。 输入的报表在请求后，或以响应事件以异步方式发送。 此报表包含实际的传感器数据。 例如，对于加速感应器、 报表包含沿 x、 y 和 z 轴的 G 强制）。
-   HID 类驱动程序将发送到传感器的功能报表。 例如，当应用程序请求的新变化敏感度或报表时间间隔内，该驱动程序打包到特征报告的这些值，并使用此报表将请求发送到传感器的固件。

下图说明了 I/O 模型：

![i/o 模型](images/hid-sensor-stack.png)

## <a name="sample-report-descriptor"></a>示例报告描述符


如果您的传感器支持类驱动程序的本机的七大类别之一，其固件都需要支持特定功能和输入的报表。 功能报表包括传感器的当前报告状态，其状态，变化敏感度和报告间隔 （除了其他可能的属性）。 输入的报表包含传感器读数：True 或 False 的交换机、 环境光线传感器的 LUX 或加速感应器的重力值。

### <a name="sample-accelerometer-feature-report"></a>示例加速感应器功能报表

下面的代码示例显示了加速感应器 HID 功能报表。 请注意此报表的自我描述的特性。 它包括最小和最大值的计数和大小的各个字段。

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

### <a name="sample-accelerometer-input-report"></a>示例加速感应器输入的报表

下面的代码示例显示了同一设备的 HID 输入的报表。 同样，请注意此报表中的字段的自我描述的特性。

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

 

 




