---
title: 加速感应器对象
description: 示例驱动程序将加速感应器视为由 CAccelerometerDevice 类表示的对象。
ms.assetid: D8E227E1-FFB5-4F4B-A981-6BD05C8FFAF2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 256cca34dfa02bad762ebd45b930ceb8e0653a7b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532967"
---
# <a name="accelerometer-object"></a>加速感应器对象


| 模块                  | 类/接口      |
|-------------------------|----------------------|
| AccelerometerDevice.cpp | CAccelerometerDevice |
| SensorDdi.cpp           | CSensorDdi           |

 

示例驱动程序将加速感应器视为由 CAccelerometerDevice 类表示的对象。 在标头文件 AccelerometerDevice.h; 中声明此对象和 AccelerometerDevice.cpp 中定义。 如果您打算扩展以支持其他传感器，除了 ADXL345，此驱动程序将到新设备 （例如，CompassDevice.h 和 CompassDevice.cpp） 创建类似名称的标头和源代码文件对应的。 如果您的驱动程序支持单个传感器，替换现有标头和源文件。

加速感应器对象支持的方法的：

-   初始化加速计
    -   配置硬件
    -   将数据通知中断连接
    -   将数据写入到设备的注册接口
    -   从设备的注册接口读取数据
    -   支持用户模式下中断
    -   检索支持的数据字段
    -   检索支持的事件
    -   检索支持的属性
    -   设置报表时间间隔内
    -   设置设备状态
    -   设置默认属性值

## <a name="initialization-methods"></a>初始化方法

| 模块                  | 类/接口      |
|-------------------------|----------------------|
| AccelerometerDevice.cpp | CAccelerometerDevice |

 

对象支持以下方法：

| 方法                                      | 描述                                                                                                                                                                                                                                                                           |
|---------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **CAccelerometerDevice::InitializeDevice**  | 从 ACPI，检索设备配置设置，然后，检索资源中心连接 Id。 通过调用此方法**CSensorDdi::Initialize**后传感器驱动程序接口、 客户端管理器和报表管理器已初始化后一种方法。 |
| **CAccelerometerDevice::ConfigureHardware** | 分配读取和写入缓冲区，并设置读取和编写器寄存器。                                                                                                                                                                                                          |
| **CAccelerometerDevice::ConnectInterrupt**  | Sreates WUDF 设备中断。 这是通过配置 WUDF\_中断\_配置数据结构，然后调用**IWDFDevice3::CreateInterrupt**方法。                                                                                                                  |

 

有关完整的初始化方法序列，请参阅[驱动程序初始化](driver-initialization.md)本指南中的部分。

## <a name="device-register-read--and-write-operations"></a>设备注册读取和写入操作

| 模块                  | 类/接口      |
|-------------------------|----------------------|
| AccelerometerDevice.cpp | CAccelerometerDevice |

 

加速感应器对象支持读取-和写入操作。 这些操作让驱动程序获取的给定的注册，或者，若要将新值写入到寄存器中的当前值。 **CAccelerometerDevice::ReadRegister**对应于读取操作和**CAccelerometerDevice::WriteRegister**对应于写入操作。 调用这些操作：

-   在驱动程序初始化时间**CAccelereometerDevice::ConfigureHardware**会调用方法来配置设备，并将其放在备用服务器模式。
-   当连接的客户端的计数变为零并且**CAccelerometerDevice::SetDeviceStateStandby**调用方法。
-   GPIO 行由 ADXL345 的断言时， **CAccelerometerDevice::OnInterruptIsr**调用方法。

## <a name="supporting-user-mode-interrupts"></a>支持用户模式下中断

本部分介绍的示例驱动程序如何获取 ADXL345 的数据。

加速感应器对象支持使用用户模式下的中断**CAccelerometerDevice::OnInterruptWorkItem**方法。 当用户模式框架调用此方法时，反过来，调用**CAccelerometerDevice::RequestData**。 此方法，反过来，调用**CAccelerometerDevice::ReadRegister**读取寄存器的内容通过 0x32 注册 0x37 ADXL345 上的。 这些六个寄存器包含当前的读数，G 破解，沿 X、 Y 和 z 轴中。

| 注册 | 目录                              |
|----------|---------------------------------------|
| 0x32     | X 轴读取的低序位字节  |
| 0x33     | 高序位字节的 x 轴读取 |
| 0x34     | Y 轴读取的低序位字节  |
| 0x35     | 高序位字节的 y 轴读取 |
| 0x36     | Z 轴读取的低序位字节  |
| 0x37     | 高序位字节的 z 轴读取 |

 

中的代码**CAccelerometerDevice::RequestData**方法打包到一个短 （xRaw、 yRaw 和 zRaw） 类型的变量的每个轴是寄存器内容，然后应用.00390625 的比例因子。 (缩放比例在的结果除以加速的范围值，32 这种情况下 （因为 + /-16 G 受支持），通过数可以表示以 13 位为单位 (2 ^13)-这是所选的解决方法。

```cpp
// Get the data values as doubles
SHORT xRaw, yRaw, zRaw;
DOUBLE xAccel, yAccel, zAccel;
const DOUBLE scaleFactor = 1/256.0F;

xRaw = (SHORT)((m_pDataBuffer[1] << 8) | m_pDataBuffer[0]);
yRaw = (SHORT)((m_pDataBuffer[3] << 8) | m_pDataBuffer[2]);
zRaw = (SHORT)((m_pDataBuffer[5] << 8) | m_pDataBuffer[4]);

xAccel = (DOUBLE)xRaw * scaleFactor;
yAccel = (DOUBLE)yRaw * scaleFactor;
zAccel = (DOUBLE)zRaw * scaleFactor;
```

该驱动程序，计算的值后，它将打包到每个**PROPVARIANT**结构，并调用**CAccelerometerDevice::AddDataField**方法来更新每个轴的值。

请注意，支持的加速范围 （+ /-16 G) 和解决方法使用寄存器 0x31 ADXL345 中的设置的也是。 此错误出现在*g\_ConfigurationSettings* AccelerometerDevice.cpp 开始部分找到的数组：

```cpp
// +-16g, 13-bit resolution
{ ADXL345_DATA_FORMAT,
   ADXL345_DATA_FORMAT_FULL_RES |
   ADXL345_DATA_FORMAT_JUSTIFY_RIGHT |
   ADXL345_DATA_FORMAT_RANGE_16G },
```

## <a name="supporting-the-report-interval"></a>支持报表时间间隔内

| 模块                  | 类/接口      |
|-------------------------|----------------------|
| AccelerometerDevice.cpp | CAccelerometerDevice |

 

传感器平台支持报表时间间隔，并能让应用程序将其设置为定义的范围内的值。 文件 Adxl345.h 中定义的示例驱动程序的最小值和默认报表间隔。

```cpp
const ULONG ACCELEROMETER_MIN_REPORT_INTERVAL              = 10;
const ULONG DEFAULT_ACCELEROMETER_CURRENT_REPORT_INTERVAL  = 100;
```

示例驱动程序限制为 10 毫秒的最小报表间隔以及为 100 毫秒的默认间隔。

传感器驱动程序使用的报表时间间隔来确定何时引发事件通知。 如果尚未超过变化敏感度，驱动程序等待当前的时间间隔，然后引发为连接的应用程序提供当前的数据读取的数据事件。 （如果尚未超出变化敏感度，则此设置将替代报表时间间隔内和驱动程序将立即引发数据事件。）

Windows 应用程序可以通过调用设置加速感应器的时间间隔**Accelerometer.ReportInterval**属性。 当应用程序调用此属性，该驱动程序的**CAccelerometerDevice::SetReportInterval**调用方法将传递给设备的固件的请求的时间间隔。

设置报表时间间隔内转换到 ADXL 寄存器的三个连续的写入操作。 第一个写操作禁用中断时，我们修改设备上的数据速率：

```cpp
// Disable interrupts while data rate is modified
pWriteBuffer[0] = 0;
hr = WriteRegister(ADXL345_INT_ENABLE, pWriteBuffer, 1);
The second write operation updates the new data rate:

// Update the data rate.
pWriteBuffer[0] = newDataRate.RateCode;
hr = WriteRegister(ADXL345_BW_RATE, pWriteBuffer, 1);

The third write operation re-enables interrupts:

// Reenable interrupts
pWriteBuffer[0] = ADXL345_INT_ACTIVITY;
hr = WriteRegister(ADXL345_INT_ENABLE, pWriteBuffer, 1);
```

## <a name="supporting-the-device-mode"></a>支持的设备模式

| 模块                  | 类/接口      |
|-------------------------|----------------------|
| AccelerometerDevice.cpp | CAccelerometerDevice |

 

示例设备支持三种设备模式：

-   与事件处理度量模式
-   不带事件的度量模式
-   备用服务器模式

度量模式会导致数据收集;备用服务器模式会不导致设备返回任何数据。 当设置度量模式与事件一起使用时，该驱动程序可以让应用注册以接收通知，当数据到达时从设备。 当设置度量模式下没有事件时，应用必须轮询最新数据的设备。

源文件中的三个方法对应于每个三种模式：**SetDeviceStateEventing、 SetDeviceStatePolling**，并**SetDeviceStateStandby**。 在调用它们**SetDataUpdateMode**。

## <a name="measurement-mode-without-eventing"></a>不带事件的度量模式

Windows 应用程序而无需 eventing 度量模式设置时，获取最新的传感器读数通过调用**Accelerometer.GetCurrentReading**。

驱动程序设置此模式下在初始化过程中，从待机模式返回时。 它使用两个写操作。 第一个操作禁用中断：

```cpp
pBuffer[0] = 0;
hr = WriteRegister(ADXL345_INT_ENABLE, pBuffer, 1);
```

第二个操作将设备置于度量模式：

```cpp
pBuffer[0] = ADXL345_POWER_CTL_MEASURE;
hr = WriteRegister(ADXL345_POWER_CTL, pBuffer, 1);
```

## <a name="measurement-mode-with-eventing"></a>与事件处理度量模式

Windows 应用时设置了度量模式使用事件处理，可以通过注册的事件处理程序从驱动程序接收数据更新**Accelerometer.ReadingChanged**事件。

驱动程序设置此模式下，在初始化期间 （和，它返回从待机模式时）。 该驱动程序设置此模式使用两个写操作。 第一个操作可确保设备处于度量模式：

```cpp
pBuffer[0] = ADXL345_POWER_CTL_MEASURE;
hr = WriteRegister(ADXL345_POWER_CTL, pBuffer, 1);
```

而且，第二个操作使活动检测中断：

```cpp
 pBuffer[0] = ADXL345_INT_ACTIVITY;
 hr = WriteRegister(ADXL345_INT_ENABLE, pBuffer, 1);
```

## <a name="supporting-standby-mode"></a>支持备用服务器模式

在客户端订阅计数变为 0，则驱动程序设置此模式。 它使用两个写操作和读取的操作。 第一个写入操作可确保中断处于禁用状态：

```cpp
pBuffer[0] = 0;
hr = WriteRegister(ADXL345_INT_ENABLE, pBuffer, 1);
```

下一步，以清除未完成的任何中断的读取操作：

```cpp
hr = ReadRegister(ADXL345_INT_SOURCE, pBuffer, 1, 0);
```

然后，第二个写操作位置设备处于备用模式：

```cpp
pBuffer[0] = ADXL345_POWER_CTL_STANDBY;
hr = WriteRegister(ADXL345_POWER_CTL, pBuffer, 1);
```

 

 




