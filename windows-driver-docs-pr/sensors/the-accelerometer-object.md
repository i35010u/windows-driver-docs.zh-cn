---
title: 加速感应对象
description: 示例驱动程序将加速感应程序视为由 CAccelerometerDevice 类表示的对象。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b2827998b16f78174bb5ae273bd7433cc35b345a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812123"
---
# <a name="accelerometer-object"></a>加速感应对象


| 模块                  | 类/接口      |
|-------------------------|----------------------|
| AccelerometerDevice .cpp | CAccelerometerDevice |
| SensorDdi .cpp           | CSensorDdi           |

 

示例驱动程序将加速感应程序视为由 CAccelerometerDevice 类表示的对象。 此对象在标头文件 AccelerometerDevice 中声明。和在 AccelerometerDevice 中定义。 如果你要扩展此驱动程序以支持另一个传感器，则除了 ADXL345，你还将创建一个名为的标头和源文件，对应到你的新设备 (例如，CompassDevice 和 CompassDevice) 。 如果驱动程序支持单个传感器，请替换现有的头文件和源文件。

加速感应对象支持以下方法：

-   初始化加速感应
    -   配置硬件
    -   连接数据通知中断
    -   将数据写入设备的注册接口
    -   从设备的注册界面读取数据
    -   支持用户模式中断
    -   检索受支持的数据字段
    -   检索受支持的事件
    -   检索支持的属性
    -   设置报表间隔
    -   设置设备状态
    -   设置默认属性值

## <a name="initialization-methods"></a>初始化方法

| 模块                  | 类/接口      |
|-------------------------|----------------------|
| AccelerometerDevice .cpp | CAccelerometerDevice |

 

对象支持以下方法：

| 方法                                      | 描述                                                                                                                                                                                                                                                                           |
|---------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **CAccelerometerDevice::InitializeDevice**  | 从 ACPI 检索设备配置设置，然后检索资源中心连接 Id。 此方法由 **CSensorDdi：： Initialize** 方法在后者初始化传感器驱动程序接口、客户端管理器和报表管理器后调用。 |
| **CAccelerometerDevice::ConfigureHardware** | 分配读取和写入缓冲区，并设置读取和写入器寄存器。                                                                                                                                                                                                          |
| **CAccelerometerDevice::ConnectInterrupt**  | Sreates WUDF 设备中断。 它通过配置 WUDF \_ 中断 \_ 配置数据结构，然后调用 **IWDFDevice3：： CreateInterrupt** 方法来实现此操作。                                                                                                                  |

 

有关完整的初始化方法序列，请参阅本指南中的 [驱动程序初始化](driver-initialization.md) 部分。

## <a name="device-register-read--and-write-operations"></a>设备-注册读和写操作

| 模块                  | 类/接口      |
|-------------------------|----------------------|
| AccelerometerDevice .cpp | CAccelerometerDevice |

 

加速感应对象同时支持读写操作。 这些操作允许驱动程序获取给定寄存器的当前值，或将新值写入寄存器。 **CAccelerometerDevice：： ReadRegister** 对应于读取操作，而 **CAccelerometerDevice：： WriteRegister** 对应于写入操作。 调用以下操作：

-   在调用 **CAccelereometerDevice：： ConfigureHardware** 方法以配置设备并将其置于备用模式时，在驱动程序初始化时。
-   当已连接的客户端的计数为零时，将调用 **CAccelerometerDevice：： SetDeviceStateStandby** 方法。
-   当 ADXL345 断言 GPIO 行并调用 **CAccelerometerDevice：： OnInterruptIsr** 方法时。

## <a name="supporting-user-mode-interrupts"></a>支持用户模式中断

本部分介绍了示例驱动程序如何获取 ADXL345 的数据。

加速感应对象通过 **CAccelerometerDevice：： OnInterruptWorkItem** 方法支持用户模式中断。 当用户模式框架调用此方法时，它将调用 **CAccelerometerDevice：： RequestData**。 此方法反过来会调用 **CAccelerometerDevice：： ReadRegister** ，以便在 ADXL345 上通过 register 0x37 读取 register 0x32 的内容。 这六个寄存器包含当前读数，其中 G-force 沿 X 轴、Y 轴和 Z 轴。

| 注册 | 目录                              |
|----------|---------------------------------------|
| 0x32     | X 轴读取的低序位字节  |
| 0x33     | X 轴读取的高序位字节 |
| 0x34     | Y 轴读取的低序位字节  |
| 0x35     | Y 轴读取的高序位字节 |
| 0x36     | Z 轴读取的低序位字节  |
| 0x37     | Z 轴读取的高序位字节 |

 

**CAccelerometerDevice：： RequestData** 方法中的代码将每个轴的寄存器内容打包为一个类型为 SHORT (XRaw、YRaw 和 zRaw 的变量) ，然后应用比例系数00390625。  (缩放系数是指在这种情况下分割加速度值的范围，32在这种情况下 (，因为支持 +/-16G，) 按13位表示的数字 (2 ^ 13) ，这是所选的分辨率。

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

驱动程序计算值后，会将每个值打包到 **PROPVARIANT** 结构中，并调用 **CAccelerometerDevice：： AddDataField** 方法来更新每个轴的值。

请注意，支持的加速范围 (+/-16G) ，并且使用 ADXL345 中的 register 0x31 设置分辨率。 这出现在 AccelerometerDevice 开头的 *g \_ ConfigurationSettings* 数组中：

```cpp
// +-16g, 13-bit resolution
{ ADXL345_DATA_FORMAT,
   ADXL345_DATA_FORMAT_FULL_RES |
   ADXL345_DATA_FORMAT_JUSTIFY_RIGHT |
   ADXL345_DATA_FORMAT_RANGE_16G },
```

## <a name="supporting-the-report-interval"></a>支持报表间隔

| 模块                  | 类/接口      |
|-------------------------|----------------------|
| AccelerometerDevice .cpp | CAccelerometerDevice |

 

传感器平台支持报表间隔，并允许应用程序将其设置为定义范围内的值。 示例驱动程序的最小和默认报表间隔在文件 Adxl345 中定义。

```cpp
const ULONG ACCELEROMETER_MIN_REPORT_INTERVAL              = 10;
const ULONG DEFAULT_ACCELEROMETER_CURRENT_REPORT_INTERVAL  = 100;
```

示例驱动程序将最小报表间隔限制为10毫秒，默认间隔限制为100毫秒。

传感器驱动程序使用报表间隔来确定何时引发事件通知。 如果尚未超出更改敏感度，驱动程序将等待当前间隔，然后引发一个数据事件，使连接的应用程序当前读取数据。  (如果已超出更改敏感度，这将覆盖报表间隔，驱动程序将立即引发数据事件。 ) 

Windows 应用可以通过调用 **ReportInterval** 属性设置加速感应的间隔。 当应用调用此属性时，将调用驱动程序的 **CAccelerometerDevice：： SetReportInterval** 方法将请求的间隔传递到设备的固件。

将报表间隔设置为三个 ADXL 寄存器的连续写入操作。 在修改设备上的数据速率时，第一次写入操作将禁用中断：

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

## <a name="supporting-the-device-mode"></a>支持设备模式

| 模块                  | 类/接口      |
|-------------------------|----------------------|
| AccelerometerDevice .cpp | CAccelerometerDevice |

 

示例设备支持三种设备模式：

-   事件的度量模式
-   不带事件的度量模式
-   备用模式

度量模式导致数据收集;备用模式导致设备没有返回任何数据。 如果设置了带事件的度量模式，则驱动程序允许应用注册，以便在数据到达设备时接收通知。 如果设置了没有事件的度量模式，应用程序必须轮询设备以获取最新数据。

源文件中的三个方法对应于三种模式中的每一种： **SetDeviceStateEventing、SetDeviceStatePolling** 和 **SetDeviceStateStandby**。 它们是从 **SetDataUpdateMode** 内调用的。

## <a name="measurement-mode-without-eventing"></a>不带事件的度量模式

如果设置了没有事件的度量模式，Windows 应用会通过调用 **GetCurrentReading** 来获取最新的传感器读数。

驱动程序在初始化期间和从备用模式返回时设置此模式。 它使用两个写入操作。 第一个操作将禁用中断：

```cpp
pBuffer[0] = 0;
hr = WriteRegister(ADXL345_INT_ENABLE, pBuffer, 1);
```

第二个操作将设备置于度量模式：

```cpp
pBuffer[0] = ADXL345_POWER_CTL_MEASURE;
hr = WriteRegister(ADXL345_POWER_CTL, pBuffer, 1);
```

## <a name="measurement-mode-with-eventing"></a>事件的度量模式

设置带有事件的度量模式后，Windows 应用可以通过注册 **ReadingChanged** 事件的事件处理程序从驱动程序接收数据更新。

驱动程序在初始化期间设置此模式 (和从备用模式返回时，) 。 驱动程序将此模式设置为两个写入操作。 第一个操作确保将设备置于度量模式：

```cpp
pBuffer[0] = ADXL345_POWER_CTL_MEASURE;
hr = WriteRegister(ADXL345_POWER_CTL, pBuffer, 1);
```

第二个操作启用活动检测中断：

```cpp
 pBuffer[0] = ADXL345_INT_ACTIVITY;
 hr = WriteRegister(ADXL345_INT_ENABLE, pBuffer, 1);
```

## <a name="supporting-standby-mode"></a>支持备用模式

当客户端订阅计数为0时，驱动程序将设置此模式。 它使用两个写入操作和一个读取操作。 第一次写入操作可确保中断被禁用：

```cpp
pBuffer[0] = 0;
hr = WriteRegister(ADXL345_INT_ENABLE, pBuffer, 1);
```

接下来，将清除所有未完成中断的读取操作：

```cpp
hr = ReadRegister(ADXL345_INT_SOURCE, pBuffer, 1, 0);
```

然后，第二个写入操作将设备置于备用模式：

```cpp
pBuffer[0] = ADXL345_POWER_CTL_STANDBY;
hr = WriteRegister(ADXL345_POWER_CTL, pBuffer, 1);
```

 

 




