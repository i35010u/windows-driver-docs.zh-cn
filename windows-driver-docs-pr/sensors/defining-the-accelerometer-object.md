---
title: 定义加速感应器对象
description: 示例驱动程序将加速感应器视为一个对象。
ms.assetid: EA30C9E6-3DA1-44C8-89DA-6FA21BE3B226
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d909c42980a302e4165685af9b155ffdd68151ac
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63377823"
---
# <a name="defining-the-accelerometer-object"></a>定义加速感应器对象


示例驱动程序将加速感应器视为一个对象。

## <a name="defining-the-accelerometer-object"></a>定义加速感应器对象


在标头文件 AccelerometerDevice.h; 中声明此对象并且，源文件 AccelerometerDevice.cpp 中进行定义。 如果您打算扩展此驱动程序以支持新增的传感器，可以创建类似的标头和对应于这些其他设备的源文件。 （如果您的驱动程序支持单个传感器，您将此标头和源将替换为对应于你的设备功能和要求的文件。）

加速感应器对象支持的方法的：

-   初始化传感器对象
-   配置硬件
-   将数据通知中断连接
-   设置报表时间间隔内
-   设置设备状态
-   将数据写入到设备的注册接口

### <a name="initializing-the-sensor-object"></a>初始化传感器对象

对象支持**初始化**从 ACPI，检索设备配置设置，然后，检索资源中心连接 Id 的方法。

### <a name="configuring-the-hardware"></a>配置硬件

对象支持**ConfigureHardware**分配读取和写入缓冲区，并设置读取和编写器寄存器方法。

### <a name="configuring-the-data-notification-interrupt"></a>配置数据通知中断

对象支持**ConnectInterrupt**创建 WUDF 设备中断的方法。 此配置，它会**WUDF\_中断\_CONFIG**数据结构，然后调用**IWDFDevice3::CreateInterrupt**方法。

### <a name="supporting-the-report-interval"></a>支持报表时间间隔内

传感器平台支持报表时间间隔内的概念，并且允许应用程序将此间隔设置为定义的范围内的值。 Windows 应用程序可以设置的间隔加速感应器通过调用**Accelerometer.ReportInterval**属性。 当应用程序调用此属性，该驱动程序的**SetReportInterval**调用方法将传递给设备的固件的请求的时间间隔。

负责报表时间间隔内的主要组件是客户端管理器。 模块 ClientManager.cpp 中找到支持代码。 客户端管理器维护连接的客户端、 订阅状态所需的报告间隔和所需的更改的区分大小的列表。 只要任何这些更改，客户端管理器计算数据更新模式和最低报表时间间隔内，并更改敏感度值。 有关报表时间间隔和更改敏感度的详细信息，请参阅[筛选数据](filtering-data.md)主题。

文件 Adxl345.h 中定义用于 ADXL345 的最小值和默认报表时间间隔。 示例驱动程序限制为 10 毫秒的最小报表间隔以及为 100 毫秒的默认间隔。

### <a name="supporting-the-device-state"></a>支持的设备状态

示例设备支持三种模式：

-   与事件处理度量模式
-   不带事件的度量模式
-   备用服务器模式

度量模式是会导致数据收集; 的模式备用服务器模式 （如名称所示） 将导致设备返回任何数据。 当设置度量模式与事件一起使用时，驱动程序允许应用程序注册以接收每个时间数据从设备收到的通知。 当设置度量模式下没有事件时，应用必须轮询最新数据的设备。

有三种模式之一的每个对应的源文件中的三种方法：**SetDeviceStateEventing**， **SetDeviceStatePolling**，和**SetDeviceStateStandby**。 在调用这些方法**SetDataUpdateMode**。

### <a name="writing-data-to-the-devices-register-interface"></a>将数据写入到设备的注册接口

ADXL345 控制通过其寄存器中写入值。 例如，驱动程序中设置相应的位启用中断**INT\_启用**注册。 和驱动程序时将写入到的值选择特定的中断 pin **INT\_映射**注册。

驱动程序支持**WriteRegister**传感器寄存器中写入数据时在内部调用的方法。 此方法的第一个参数指定正在写入到哪一寄存器，第二个自变量指向数据缓冲区和第三个参数指定的缓冲区的大小。

表 16 个设备的数据工作表中找到了加速感应器的完整注册映射。 示例驱动程序支持注册在映射中发现的值的子集。 Adxl345.h 标头文件中找到这些支持的值：

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

## <a name="related-topics"></a>相关主题
[SpbAccelerometer 驱动程序示例](spbaccelerometer-driver-sample.md)



