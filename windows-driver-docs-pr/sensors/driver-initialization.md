---
title: 驱动程序初始化
description: 驱动程序初始化
ms.assetid: 9886BBBC-7EE5-45AF-AEDD-75C0885C622B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cdde029776cb127adc8336d4d884b3ee454311dd
ms.sourcegitcommit: 9102e34c3322d8697dbb6f9a1d78879147a73373
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/28/2020
ms.locfileid: "87264448"
---
# <a name="driver-initialization"></a>驱动程序初始化


驱动程序初始化是用户模式驱动程序功能的更复杂的一个阶段。 它涉及示例驱动程序中的大多数组件（如果不是全部）。

### <a name="acpi-configuration-and-initialization"></a>ACPI 配置和初始化

| 模块               | 类/接口 |
|----------------------|-----------------|
| SpbAccelerometer. asl | 空值             |

 

示例驱动程序的设计使传感器永久连接到 I2C 总线。 它不支持即插即用，而是支持高级配置和电源接口（ACPI）。

ACPI 允许 Windows 控制设备的配置和电源管理。 ACPI 规范包含链接您的 Windows 设备和连接到系统板的外围设备的表的定义。 差分系统描述表（DSDT）描述连接到系统（包括传感器）的外围设备。 它以二进制格式存储，称为 ACPI 机器语言（AML）。 有关 DSDT 表的详细信息，请参阅 ACPI 系统说明表主题。 （请注意，某些系统还使用辅助系统描述表（SSDT）来描述外围设备。）

若要在 Windows SoC 设备上安装传感器设备和驱动程序，需要使用相应的节点更新 DSDT 表。 此节点包含有关示例设备的控制器和连接器的信息。 下面是 Windows 和驱动程序使用节点中数据的方式：

1.  即插即用（PnP）管理器从 ACPI 驱动程序获取设备连接信息。
2.  然后，PnP 管理器创建一个连接 ID 以表示总线连接。
3.  PnP 管理器会将连接 ID 作为硬件资源传递给示例驱动程序。
4.  示例驱动程序使用连接 ID 打开到传感器设备的逻辑连接，并获取连接的句柄。
5.  驱动程序将此句柄指定为发送到设备的 i/o 请求的目标。

### <a name="updating-the-dsdt-table"></a>更新 DSDT 表

有关说明如何更新 DSDT 表的说明，请参阅在[带 Cove 上安装示例设备和驱动程序](installing-the-sample-device-and-driver-on-your-sharks-cove-board.md)。

### <a name="modifying-the-sample-asl-file"></a>修改示例 ASL 文件

如果修改示例驱动程序以支持其他设备，则将对示例 ASL 文件进行相应的更新。 大多数更新都将成为 \_ 文件的 CRS 部分，你可以在其中指定设备需要的 I2C 和 GPIO 资源。 你还需要提供 \_ 与更新的 INF 文件中的相应条目匹配的唯一 HID 条目。

### <a name="decoding-i2c-or-gpio-resources"></a>对 I2C 或 GPIO 资源进行解码

如果未指定/resdecode 选项，则 \_ CRS 部分将包含二进制 blob。 若要将此部分转换为可读文本，请按如下所示应用/resdecode： Asl.exe/tab： dsdt/resdecode

### <a name="updating-the-windows-setup-information-file"></a>更新 Windows 安装程序信息文件

| 模块               | 类/接口 |
|----------------------|-----------------|
| SpbAccelerometer .inf | 空值             |

 

除了更新 DSDT 表，你还需要更新 Windows 安装程序信息文件（INF）以指定你的设备支持 ACPI。 由于始终使用 ACPI 枚举传感器，因此 INF 文件中的硬件标识符必须包含 "ACPI" 字符串。

```cpp
; =================== Manufacturer/Models sections =======================

[Manufacturer]
%MSFT%                      = Microsoft,NTx86

[Microsoft.NTx86]
%SpbAccelerometer.DeviceDesc% = SpbAccelerometer_Install,ACPI\SpbAccelerometer
```

### <a name="initializing-the-driver-and-device"></a>初始化驱动程序和设备

| 模块      | 类/接口 |
|-------------|-----------------|
| DllMain .cpp | 空值             |
| 设备 .cpp  | CMyDevice       |
| 驱动程序 .cpp  | CMyDriver       |
| Queue   | CMyQueue        |

 

下面的方法由 Windows 或驱动程序在早期初始化阶段调用。 初级设备初始化方法适用于你的驱动程序支持的任何设备。 它们显示在模块设备 .cpp 中。

|  步骤   | 方法                        | 调用者                                                         | 目的                                                                                                       |
|-----|-------------------------------|--------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------|
| 1   | **DllGetClassObject**         | WUDFHost.exe                                                       | 获取驱动程序的类对象。 （对于任何 COM DLL 都是必需的。）                                                   |
| 2   | **CMyDevice::OnQueryRemove**  | WUDFx.dll （Windows 用户模式驱动程序框架的组件）。 |                                                                                                               |
| 3   | **CMyDriver::OnDeviceAdd**    | WUDFx.dll （Windows 用户模式驱动程序框架的组件）。 | 通知驱动程序已添加设备。                                                             |
| 4   | **CMyDevice：： Configure**      | **CMyDriver::OnDeviceAdd**                                         | 配置设备的队列和相应的回调对象。                                        |
| 5   | **CMyQueue： CreateInstance**   | **CMyDevice：： Configure**                                           | 创建设备队列回调的实例                                                            |
| 6   | **CMyDevice：： CreateInstance** | **CMyDevice::OnDeviceAdd**                                         | 创建设备对象的一个实例，该实例对应于给定的设备（在本例中为加速计）。 |
| 7   | **CMyDevice：： Initialize**     | **CMyDevice：： CreateInstance**                                      | 初始化设备回调对象。                                                                       |

 

### <a name="establishing-a-data-connection"></a>建立数据连接

| 模块                  | 类/接口      |
|-------------------------|----------------------|
| 设备 .cpp              | CMyDevice            |
| SensorDdi .cpp           | CSensorDdi           |
| AccelerometerDevice .cpp | CAccelerometerDevice |

 

以下方法由驱动程序在初始化期间调用，用于准备设备对象、获取 ACPI 配置数据和创建数据连接中断。 对于示例驱动程序，这些方法位于 AccelerometerDevice 文件中。

如果要移植示例驱动程序以支持另一台设备，如罗盘，你将创建一个并行模块 CompassDevice。 将 CAccelerometerDevice 类替换为 CCompassDevice 类，并修改该示例的模块中的方法，以支持设备的对象、数据和中断。

| 步骤    | 方法                                                 | 调用者                                                         | 目的                                                                                                                |
|-----|--------------------------------------------------------|--------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------|
| 1   | **CMyDevice::OnPrepareHardware**                       | WUDFx.dll （Windows 用户模式驱动程序框架的组件）。 | 开始使给定设备可由驱动程序访问所需的操作。                                       |
| 2   | **CSensorDdi：： Initialize**                             | **CMyDevice::OnPrepareHardware**                                   | 创建并初始化传感器设备对象。                                                                        |
| 3   | **CSensorDevice：： Initialize**                          | **CSensorDdi：： Initialize**                                         | 初始化传感器驱动程序接口、客户端管理器和报表管理器。                                   |
| 4   | **CAccelerometerDevice::InitializeDevice**             | **CSensorDevice：： Initialize**                                      | 初始化加速感应设备对象。                                                                           |
| 5   | **CAccelerometerDevice::GetConfigurationData**         | **CAccelerometerDevice::InitializeDevice**                         | 启动从 ACPI 进行配置数据的检索。                                                               |
| 6   | **CAccelerometerDevice：:P repareInputParametersForDsm** | **CAccelerometerDevice::GetConfigurationData**                     | \_ \_ \_ 在调用设备特定方法（DSM）函数之前准备 acpi 输入缓冲区（acpi EVAL 输入缓冲区）。 |
| 7   | **CAccelerometerDevice：:P arseAcpiOutputBuffer**        | **CAccelerometerDevice::GetConfigurationData**                     | 分析在 ACPI 输出缓冲区（ACPI \_ EVAL \_ 输出缓冲区）中返回的配置数据 \_ 。                |
| 8   | **CAccelerometerDevice：:P arseResources**               | **CAccelerometerDevice::InitializeDevice**                         | 分析设备资源，以确保它们支持串行 I2C 连接。                                        |
| 9   | **CAccelerometerDevice::ConnectInterrupt**             | **CAccelerometerDevice：:P arseResources**                           | 创建数据连接中断。                                                                                 |

 

### <a name="initializing-the-spb-request-object"></a>初始化 SPB 请求对象

| 模块                  | 类/接口      |
|-------------------------|----------------------|
| 设备 .cpp              | CMyDevice            |
| SensorDdi .cpp           | CSensorDdi           |
| AccelerometerDevice .cpp | CAccelerometerDevice |
| SpbRequest .cpp          | CSpbRequest          |

 

下面的方法由驱动程序在初始化期间调用，以打开基础 SPB 控制器的文件句柄。 （请注意，此序列的前四个方法与数据连接序列中的前四个方法相同。）

| 步骤   | 方法                                      | 调用者                                                         | 目的                                                                                                                                          |
|-----|---------------------------------------------|--------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------|
| 1   | **CMyDevice::OnPrepareHardware**            | WUDFx.dll （Windows 用户模式驱动程序框架的组件）。 | 开始使给定设备可由驱动程序访问所需的操作。                                                                |
| 2   | **CSensorDdi：： Initialize**                  | **CMyDevice::OnPrepareHardware**                                   | 创建并初始化传感器设备对象。                                                                                                |
| 3   | **CSensorDevice：： Initialize**               | **CSensorDdi：： Initialize**                                         | 初始化传感器驱动程序接口、客户端管理器和报表管理器。                                                             |
| 4   | **CAccelerometerDevice::InitializeDevice**  | **CSensorDevice：： Initialize**                                      | 初始化加速感应设备对象。                                                                                                     |
| 5   | **CAccelerometerDevice::InitializeRequest** | **CAccelerometerDevice::InitializeDevice**                         | 为 SPB 请求对象启动初始化过程（使用先前检索到的驱动程序的资源中心路径和连接 ID）。 |
| 6   | **CSpbRequest：： Initialize**                 | **CAccelerometerDevice::InitializeRequest**                        | 打开基础 SPB 的文件句柄                                                                                                        |

 

### <a name="initializing-the-supported-sensor-properties-and-data-fields"></a>初始化支持的传感器属性和数据字段

| 模块                  | 类/接口      |
|-------------------------|----------------------|
| 设备 .cpp              | CMyDevice            |
| SensorDdi .cpp           | CSensorDdi           |
| AccelerometerDevice .cpp | CAccelerometerDevice |
| SpbRequest .cpp          | CSpbRequest          |

 

下面的方法由驱动程序在初始化期间调用，以获取该传感器支持的属性和数据字段。 对于 Windows 传感器平台，加速感应器属性对应于读取或读/写数据，如传感器的报告间隔或支持的最小报告时间间隔。 数据字段对应于实际加速感应读数沿 X 轴、Y 轴和 Z 轴。 （请注意，此序列的前三种方法与以前的数据连接中的前三个方法和 SPB 请求对象的序列相同。）

| 步骤  | 方法                                             | 调用者                                                         | 目的                                                                                                               |
|-----|----------------------------------------------------|--------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------|
| 1   | **CMyDevice::OnPrepareHardware**                   | WUDFx.dll （Windows 用户模式驱动程序框架的组件）。 | 开始使给定设备可由驱动程序访问所需的操作。                                     |
| 2   | **CSensorDdi：： Initialize**                         | **CMyDevice::OnPrepareHardware**                                   | 创建并初始化传感器设备对象。                                                                      |
| 3   | **CSensorDevice：： Initialize**                      | **CSensorDdi：： Initialize**                                         | 初始化传感器驱动程序接口、客户端管理器和报表管理器。                                  |
| 4   | **CSensorDevice::InitializeSensorDriverInterface** | **CSensorDevice：： Initialize**                                      | 启动存储属性键和 datafield 值的**IPortableDeviceValues**对象的初始化。 |
| 5   | **CSensorDevice::AddPropertyKeys**                 | **CSensorDevice::InitializeSensorDriverInterface**                 | 循环访问受支持的属性，并为每个属性添加**PROPERTYKEY** 。                                        |
| 6   | **CAccelerometerDevice::GetSupportedProperties**   | **CSensorDevice::AddPropertyKeys**                                 | 获取给定设备的属性的**PROPERTYKEY**结构。                                                |
| 7   | **CSensorDevice::AddDataFieldKeys**                | **CSensorDevice::InitializeSensorDriverInterface**                 | 循环访问受支持的数据字段，并为每个字段添加**PROPERTYKEY** 。                                       |
| 8   | **CSensorDevice::GetSupportedDataFields**          | **CSensorDevice::AddDataFieldKeys**                                | 获取给定设备的数据字段的**PROPERTYKEY**。                                                         |

 

### <a name="initializing-the-persistent-unique-id-property"></a>初始化永久性唯一 ID 属性

| 模块                  | 类/接口      |
|-------------------------|----------------------|
| 设备 .cpp              | CMyDevice            |
| SensorDdi .cpp           | CSensorDdi           |
| AccelerometerDevice .cpp | CAccelerometerDevice |
| SensorDevice .cpp        | CSensorDevice        |

 

下面的方法由驱动程序在初始化期间调用，用于初始化传感器的持久唯一标识符（PUID）。 Windows 使用**PUID**跨设备会话保存数据。 （请注意，此序列的前四个方法与前一个属性和数据字段序列中的前四个方法相同。）

| 步骤  | 方法                                             | 调用者                                                         | 目的                                                                                                   |
|-----|----------------------------------------------------|--------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------|
| 1   | **CMyDevice::OnPrepareHardware**                   | WUDFx.dll （Windows 用户模式驱动程序框架的组件）。 | 开始使给定设备可由驱动程序访问所需的操作。                         |
| 2   | **CSensorDdi：： Initialize**                         | **CMyDevice::OnPrepareHardware**                                   | 创建并初始化传感器设备对象。                                                          |
| 3   | **CSensorDevice：： Initialize**                      | **CSensorDdi：： Initialize**                                         | 初始化传感器驱动程序接口、客户端管理器和报表管理器。                      |
| 4   | **CSensorDevice::InitializeSensorDriverInterface** | **CSensorDevice：： Initialize**                                      | 开始初始化存储属性键和 datafield 值的对象。               |
| 5   | **CSensorDevice::SetUniqueID**                     | **CSensorDevice::InitializeSensorDriverInterface**                 | 调用一个方法，该方法获取驱动程序可跨会话使用的永久唯一标识符（PUID）。 |
| 6   | **CAcclerometerDevice::GetSensorObjectID**         | **CSensorDevice::SetUniqueID**                                     | 获取加速度的永久性标识符（"ADXL345"）。                                               |

 

### <a name="setting-the-default-property-values"></a>设置默认属性值

| 模块                  | 类/接口      |
|-------------------------|----------------------|
| 设备 .cpp              | CMyDevice            |
| SensorDdi .cpp           | CSensorDdi           |
| AccelerometerDevice .cpp | CAccelerometerDevice |
| SensorDevice .cpp        | CSensorDevice        |

 

Windows 传感器平台支持传感器类型、制造商名称、传感器型号和序列号的默认属性值。 SpbAccelerometer 示例中的代码将这些属性设置为驱动程序和设备初始化阶段的一部分。 下面的方法由驱动程序在初始化期间调用，以设置加速感应的默认值。 （请注意，此序列的前四个方法与之前的属性设置序列中的前四个方法相同。）

| 步骤   | 方法                                             | 调用者                                                         | 目的                                                                                           |
|-----|----------------------------------------------------|--------------------------------------------------------------------|---------------------------------------------------------------------------------------------------|
| 1   | **CMyDevice::OnPrepareHardware**                   | WUDFx.dll （Windows 用户模式驱动程序框架的组件）。 | 开始使给定设备可由驱动程序访问所需的操作。                 |
| 2   | **CSensorDdi：： Initialize**                         | **CMyDevice::OnPrepareHardware**                                   | 创建并初始化传感器设备对象。                                                   |
| 3   | **CSensorDevice：： Initialize**                      | **CSensorDdi：： Initialize**                                         | 初始化传感器驱动程序接口、客户端管理器和报表管理器。              |
| 4   | **CSensorDevice::InitializeSensorDriverInterface** | **CSensorDevice：： Initialize**                                      | 开始初始化存储属性键和 datafield 值的对象。       |
| 5   | **CAccelerometerDevice::SetDefaultPropertyValues** | **CSensorDevice::InitializeSensorDriverInterface**                 | 设置加速感应的默认属性值（制造商、型号、序列号等） |

 

### <a name="retrieving-the-default-writeable-properties"></a>检索默认的可写属性

| 模块                  | 类/接口      |
|-------------------------|----------------------|
| 设备 .cpp              | CMyDevice            |
| SensorDdi .cpp           | CSensorDdi           |
| AccelerometerDevice .cpp | CAccelerometerDevice |
| SensorDevice .cpp        | CSensorDevice        |

 

Windows 传感器平台支持传感器的只读和读写属性，这也适用于默认属性。 SpbAccelerometer 示例中的代码获取作为驱动程序和设备初始化阶段的一部分的可写入（或可设置）默认属性的列表。 下面的方法由驱动程序在初始化期间调用，以获取加速感应的这些属性。 （请注意，此序列的前四个方法与之前的属性设置序列中的前四个方法相同。）

| 步骤   | 方法                                             | 调用者                                                         | 目的                                                                                           |
|-----|----------------------------------------------------|--------------------------------------------------------------------|---------------------------------------------------------------------------------------------------|
| 1   | **CMyDevice::OnPrepareHardware**                   | WUDFx.dll （Windows 用户模式驱动程序框架的组件）。 | 开始使给定设备可由驱动程序访问所需的操作。                  |
| 2   | **CSensorDdi：： Initialize**                         | **CMyDevice::OnPrepareHardware**                                   | 创建并初始化传感器设备对象。                                                  |
| 3   | **CSensorDevice：： Initialize**                      | **CSensorDdi：： Initialize**                                         | 初始化传感器驱动程序接口、客户端管理器和报表管理器。              |
| 4   | **CSensorDevice::InitializeSensorDriverInterface** | **CSensorDevice：： Initialize**                                      | 开始初始化存储属性键和 datafield 值的对象。       |
| 5   | **CAccelerometerDevice::SetDefaultPropertyValues** | **CSensorDevice::InitializeSensorDriverInterface**                 | 设置加速感应的默认属性值（制造商、型号、序列号等） |

 

### <a name="activating-support-for-events"></a>激活对事件的支持

| 模块                  | 类/接口      |
|-------------------------|----------------------|
| 设备 .cpp              | CMyDevice            |
| SensorDdi .cpp           | CSensorDdi           |
| AccelerometerDevice .cpp | CAccelerometerDevice |
| SensorDevice .cpp        | CSensorDevice        |

 

Windows 传感器平台支持事件。 应用程序注册事件处理程序以从驱动程序获取通知。 对于加速感应程序，当超过特定的更改敏感度（以 G force 度量）或当前报表间隔过期时，将触发这些通知。

若要支持传感器平台中的事件模型，驱动程序必须激活线程才能处理事件通知。 下面的方法由驱动程序在初始化期间调用以执行此激活。 （请注意，此序列的前三种方法与前面的多个序列中的前三个方法相同。）

| 步骤   | 方法                                         | 调用者                                                         | 目的                                                                              |
|-----|------------------------------------------------|--------------------------------------------------------------------|--------------------------------------------------------------------------------------|
| 1   | **CMyDevice::OnPrepareHardware**               | WUDFx.dll （Windows 用户模式驱动程序框架的组件）。 | 开始使给定设备可由驱动程序访问所需的操作。    |
| 2   | **CSensorDdi：： Initialize**                     | **CMyDevice::OnPrepareHardware**                                   | 创建并初始化传感器设备对象。                                    |
| 3   | **CSensorDevice：： Initialize**                  | **CSensorDdi：： Initialize**                                         | 初始化传感器驱动程序接口、客户端管理器和报表管理器。 |
| 4   | **CReportManager：： Initialize**                 | **CSensorDevice：： Initialize**                                      | 创建用于处理事件的线程。                                            |
| 5   | **CReportManager::ActivateDataEventingThread** | **CReportManager：： Initialize**                                     | 激活由上一个方法创建的线程。                                 |

 

### <a name="initializing-the-class-extension"></a>初始化类扩展

| 模块     | 类/接口 |
|------------|-----------------|
| 设备 .cpp | CMyDevice       |

 

Windows 传感器平台具有传感器 API 的类扩展，它提供了一种用于获取传感器数据和引发事件通知的标准机制。 示例驱动程序调用**ISensorClassExtension：： initialize**方法，以便在它收到对**CMyDevice：： OnPrepareHardware**的调用后初始化该类扩展。

### <a name="configuring-the-device-and-placing-it-in-standby-mode"></a>配置设备并将其置于备用模式

| 模块                  | 类/接口      |
|-------------------------|----------------------|
| 设备 .cpp              | CMyDevice            |
| SensorDdi .cpp           | CSensorDdi           |
| AccelerometerDevice .cpp | CAccelerometerDevice |
| SensorDevice .cpp        | CSensorDevice        |

 

设备和驱动程序初始化中的最后一个方法序列配置 ADXL345，并将其置于备用模式。 （此写入和读取操作的顺序重复多次，直到配置了设备。）

| 步骤  | 方法                                          | 调用者                                                         | 目的                                                                               |
|-----|-------------------------------------------------|--------------------------------------------------------------------|---------------------------------------------------------------------------------------|
| 1   | **CMyDevice::OnD0Entry**                        | WUDFx.dll （Windows 用户模式驱动程序框架的组件）。 | 当系统上出现新设备时进行调用。                                      |
| 2   | **CSensorDdi：： Start**                           | **CMyDevice::OnD0Entry**                                           | 调用 CSensorDevice：： Start 的传递方法。                                |
| 3   | **CSensorDevice：： Start**                        | **CSensorDdi：： Start**                                              | 启动设备配置过程。                                           |
| 4   | **CAccelerometerDevice::ConfigureHardware**     | **CSensorDevice：： Start**                                           | 启动向 ADXL345 的指定寄存器写入值的操作。 |
| 5   | **CAcclerometerDevice::WriteRegister**          | **CAccelerometerDevice::ConfigureHardware**                        | 启动向 ADXL345 的指定寄存器写入值的操作。 |
| 6   | **CSpbRequest::CreateAndSendWrite**             | **CAcclerometerDevice::WriteRegister**                             | 通过 I2C 总线传输写入请求                                          |
| 7   | **CAcclerometerDevice::ReadRegister**           | **CAccelerometerDevice::ConfigureHardware**                        | 启动从指定的 ADXL345 寄存器读取值的操作。       |
| 8   | **CSpbRequest::CreateAndSendWriteReadSequence** | **CAcclerometerDevice::ReadRegister**                              | 通过 I2C 总线接收读取结果。                                           |
| 9   | **CSpbRequest::CreateAndSendIoctl**             | **CSpbRequest::CreateAndSendWriteReadSequence**                    | 创建和发送 IOCTL 请求的帮助器方法。                                |

 

大多数设备配置工作都是通过一系列的**CAccelerometerDevice：： WriteRegister**和**CAccelerometerDevice：： ReadRegister**方法调用来进行的。 驱动程序使用：：**WriteRegister**方法将值写入其中一个 ADXL345 寄存器;然后，它会检查相应的：：**ReadRegister**方法中返回的值以验证写入操作是否成功。 下面是完整的写入和读取操作序列。

| 步骤 | 方法                                  | 注册 | 数据                | 目的                                                                                                            |
|-----|-----------------------------------------|----------|---------------------|--------------------------------------------------------------------------------------------------------------------|
| 1   | **CAccelerometerDevice::WriteRegister** | **0x2d** | **" \\ 0" （0x00）**    | 重置传感器的电源控制寄存器，并将设备置于备用模式。                                   |
| 2   | **CAccelerometerDevice::ReadRegister**  | **0x2d** | **" \\ 0" （0x00）**    | 返回的寄存器值指示写操作成功。                                          |
| 3   | **CAccelerometerDevice::WriteRegister** | **0x31** | **" \\ v" （0x0b）**    | 将设备设置为完全分辨率模式，每个轴上的 +/-16G 范围。                                   |
| 4   | **CAccelerometerDevice::ReadRegister**  | **0x31** | **" \\ v" （0x0b**     | 返回的寄存器值指示写操作成功。                                          |
| 5   | **CAccelerometerDevice::WriteRegister** | **0x38** | **" \\ 0" （0x00）**    | 将传感器的 FIFO 控制寄存器重置为绕过模式。                                                      |
| 6   | **CAccelerometerDevice::ReadRegister**  | **0x38** | **" \\ 0" （0x00）**    | 返回的寄存器值指示写操作成功。                                          |
| 7   | **CAccelerometerDevice::WriteRegister** | **0x2C** | **" \\ a" （0x07）**    | 设置 BW \_ 速率寄存器以启动低功耗模式。                                                             |
| 8   | **CAccelerometerDevice::ReadRegister**  | **0x2C** | **" \\ a" （0x07）**    | 返回的寄存器值指示写操作成功。                                          |
| 9   | **CAccelerometerDevice::WriteRegister** | **0x24** | **" \\ x1" （0x01）**   | 将 TRESH \_ ACT （活动阈值）寄存器设置为1。                                                            |
| 10  | **CAccelerometerDevice::ReadRegister**  | **0x24** | **" \\ x1" （0x01）**   |                                                                                                                    |
| 11  | **CAccelerometerDevice::WriteRegister** | **0x27** | **0xf0**          | 将 ACT \_ INACT \_ CTL （活动/非活动）寄存器设置为0xf0。                                                       |
| 12  | **CAccelerometerDevice::ReadRegister**  | **0x27** | **0xf0**          | 返回的 register 值指示写操作成功。                                              |
| 13  | **CAccelerometerDevice::WriteRegister** | **0x2f** | **" \\ 0x10" （0x10）** | 设置 INT \_ 映射（中断映射）注册。 0x10 的值请求将水印映射到 INT2 pin。 |
| 14  | **CAccelerometerDevice::ReadRegister**  | **0x2f** | **" \\ 0x10" （0x10）** | 返回的 register 值指示写操作成功。                                          |


在配置了驱动程序和设备之后，初始化序列完成，应用程序可以开始接收传感器数据。

 

 




