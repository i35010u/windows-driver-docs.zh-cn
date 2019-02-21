---
title: 驱动程序初始化
description: 驱动程序初始化
ms.assetid: 9886BBBC-7EE5-45AF-AEDD-75C0885C622B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ecc49488e52a51cc37dd658c71740a486534a5b7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545267"
---
# <a name="driver-initialization"></a>驱动程序初始化


驱动程序初始化是功能的更复杂的阶段的用户模式驱动程序之一。 它涉及到大多数，如果不是全部中的示例驱动程序的组件。

### <a name="acpi-configuration-and-initialization"></a>ACPI 配置和初始化

| 模块               | 类/接口 |
|----------------------|-----------------|
| SpbAccelerometer.asl | 不适用             |

 

以便传感器永久连接到 I2C 总线设计的示例驱动程序。 而不是支持插，它支持的高级配置和电源接口 (ACPI)。

ACPI 允许 Windows 用于控制设备的配置和电源管理。 ACPI 规范具有表的定义，该 Windows 设备和外围设备连接到系统板的链接。 区分系统说明表 (DSDT) 介绍了外围设备连接到系统 — 包括传感器。 它存储在已知为 ACPI 机器语言 (AML) 的二进制格式。 有关 DSDT 表的详细信息，请参阅 ACPI 系统说明表主题。 （请注意，某些系统还使用辅助系统说明表 (SSDT) 来描述外围设备）。

若要在 Windows SoC 设备上安装传感器设备和驱动程序，你将需要更新 DSDT 表中的相应节点。 此节点包含有关示例设备的控制器和连接器的信息。 下面是如何 Windows 和您的驱动程序使用数据的节点中：

1.  1. 插即用 (PnP) 管理器从 ACPI 驱动程序中获取设备连接信息。
2.  然后，PnP 管理器创建的连接 ID 来表示总线连接。
3.  PnP 管理器将传递给的示例驱动程序的连接 ID，作为硬件资源。
4.  示例驱动程序使用的连接 ID 来打开到传感器设备的逻辑连接，并获取连接的句柄。
5.  驱动程序指定的目标 I/O 请求将发送到设备的此句柄。

### <a name="updating-the-dsdt-table"></a>更新 DSDT 表

有关说明如何更新 DSDT 表的说明，请参阅[Shark Cove 上安装的示例设备和驱动程序](installing-the-sample-device-and-driver-on-your-sharks-cove-board.md)主题。

### <a name="modifying-the-sample-asl-file"></a>修改示例 ASL 文件

如果修改示例驱动程序，以支持另一台设备，你将对示例 ASL 文件进行相应更新。 大部分更新将发送到\_CRS 部分中的文件在其中指定 I2C 和你的设备需要的 GPIO 资源。 您还需要提供一个唯一\_与更新后的 INF 文件中的相应条目匹配的 HID 条目。

### <a name="decoding-i2c-or-gpio-resources"></a>解码 I2C 或 GPIO 资源

如果不指定 /resdecode 选项， \_CRS 部分将包含二进制 blob。 若要将此段转换为人工读取的文本，将应用 /resdecode，如下所示：Asl.exe /tab:dsdt /resdecode

### <a name="updating-the-windows-setup-information-file"></a>更新 Windows 安装程序信息文件

| 模块               | 类/接口 |
|----------------------|-----------------|
| SpbAccelerometer.inf | 不适用             |

 

除了更新 DSDT 表，您将需要更新 Windows 安装程序信息文件 (INF) 来指定你的设备支持 ACPI。 ACPI 始终枚举传感器，因为 INF 文件中的硬件标识符必须包含"ACPI"字符串。

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
| DllMain.cpp | 不适用             |
| Device.cpp  | CMyDevice       |
| Driver.cpp  | CMyDriver       |
| Queue.cpp   | CMyQueue        |

 

下面的方法是在早期的初始化阶段调用通过 Windows 或驱动程序。 初步设备初始化方法适用于支持您的驱动程序的任何设备。 它们在模块 Device.cpp 中显示。

|     | 方法                        | 通过调用                                                         | 用途                                                                                                       |
|-----|-------------------------------|--------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------|
| 1   | **DllGetClassObject**         | WUDFHost.exe                                                       | 获取驱动程序的类对象。 （所需的任何 COM DLL）。                                                   |
| 2   | **CMyDevice::OnQueryRemove**  | WUDFx.dll （Windows 用户模式驱动程序框架的组件）。 |                                                                                                               |
| 3   | **CMyDriver::OnDeviceAdd**    | WUDFx.dll （Windows 用户模式驱动程序框架的组件）。 | 通知已添加设备驱动程序。                                                             |
| 4   | **CMyDevice::Configure**      | **CMyDriver::OnDeviceAdd**                                         | 配置设备的队列和相应的回调对象。                                        |
| 5   | **CMyQueue:CreateInstance**   | **CMyDevice::Configure**                                           | 创建设备的队列回调的实例                                                            |
| 6   | **CMyDevice::CreateInstance** | **CMyDevice::OnDeviceAdd**                                         | 创建对应于给定设备 （在此情况下加速感应器） 的设备对象的实例。 |
| 7   | **CMyDevice::Initialize**     | **CMyDevice::CreateInstance**                                      | 初始化设备回调对象。                                                                       |

 

### <a name="establishing-a-data-connection"></a>建立数据连接

| 模块                  | 类/接口      |
|-------------------------|----------------------|
| Device.cpp              | CMyDevice            |
| SensorDdi.cpp           | CSensorDdi           |
| AccelerometerDevice.cpp | CAccelerometerDevice |

 

在初始化准备设备对象，获取 ACPI 的配置数据，并创建数据连接中断期间，驱动程序时会调用这些方法下面。 对于示例驱动程序，这些方法文件 AccelerometerDevice.cpp 中找到。

如果您要迁移的示例驱动程序以支持其他设备，如指南针，你将创建一个并行模块 CompassDevice.cpp。 CAccelerometerDevice 类替换为 CCompassDevice 类和修改以支持你的设备对象、 数据和中断的示例的模块中的方法。

|     | 方法                                                 | 通过调用                                                         | 用途                                                                                                                |
|-----|--------------------------------------------------------|--------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------|
| 1   | **CMyDevice::OnPrepareHardware**                       | WUDFx.dll （Windows 用户模式驱动程序框架的组件）。 | 启动所需的操作以便可以访问给定的设备驱动程序。                                       |
| 2   | **CSensorDdi::Initialize**                             | **CMyDevice::OnPrepareHardware**                                   | 创建并初始化传感器设备对象。                                                                        |
| 3   | **CSensorDevice::Initialize**                          | **CSensorDdi::Initialize**                                         | 初始化传感器驱动程序接口、 客户端管理器和报表管理器。                                   |
| 4   | **CAccelerometerDevice::InitializeDevice**             | **CSensorDevice::Initialize**                                      | 初始化加速感应器设备对象。                                                                           |
| 5   | **CAccelerometerDevice::GetConfigurationData**         | **CAccelerometerDevice::InitializeDevice**                         | 启动配置数据从 ACPI 的检索。                                                               |
| 6   | **CAccelerometerDevice::PrepareInputParametersForDsm** | **CAccelerometerDevice::GetConfigurationData**                     | 准备 ACPI 输入的缓冲区 (ACPI\_EVAL\_输入\_缓冲区) 之前调用设备特定方法 (DSM) 函数。 |
| 7   | **CAccelerometerDevice::ParseAcpiOutputBuffer**        | **CAccelerometerDevice::GetConfigurationData**                     | 分析在 ACPI 输出缓冲区中返回的配置数据 (ACPI\_EVAL\_输出\_缓冲区)。                |
| 8   | **CAccelerometerDevice::ParseResources**               | **CAccelerometerDevice::InitializeDevice**                         | 分析设备资源，以确保它们支持串行 I2C 连接。                                        |
| 9   | **CAccelerometerDevice::ConnectInterrupt**             | **CAccelerometerDevice::ParseResources**                           | 创建数据连接中断。                                                                                 |

 

### <a name="initializing-the-spb-request-object"></a>初始化存储请求对象

| 模块                  | 类/接口      |
|-------------------------|----------------------|
| Device.cpp              | CMyDevice            |
| SensorDdi.cpp           | CSensorDdi           |
| AccelerometerDevice.cpp | CAccelerometerDevice |
| SpbRequest.cpp          | CSpbRequest          |

 

若要打开的文件句柄的基础存储控制器的初始化期间，驱动程序时会调用这些方法下面。 （请注意，此序列的前四个方法中的数据连接序列的前四个方法相同。）

|     | 方法                                      | 通过调用                                                         | 用途                                                                                                                                          |
|-----|---------------------------------------------|--------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------|
| 1   | **CMyDevice::OnPrepareHardware**            | WUDFx.dll （Windows 用户模式驱动程序框架的组件）。 | 启动所需的操作以便可以访问给定的设备驱动程序。                                                                |
| 2   | **CSensorDdi::Initialize**                  | **CMyDevice::OnPrepareHardware**                                   | 创建并初始化传感器设备对象。                                                                                                |
| 3   | **CSensorDevice::Initialize**               | **CSensorDdi::Initialize**                                         | 初始化传感器驱动程序接口、 客户端管理器和报表管理器。                                                             |
| 4   | **CAccelerometerDevice::InitializeDevice**  | **CSensorDevice::Initialize**                                      | 初始化加速感应器设备对象。                                                                                                     |
| 5   | **CAccelerometerDevice::InitializeRequest** | **CAccelerometerDevice::InitializeDevice**                         | 启动 （使用该驱动程序之前检索到的资源中心路径和连接 ID） 的存储请求对象的初始化过程。 |
| 6   | **CSpbRequest::Initialize**                 | **CAccelerometerDevice::InitializeRequest**                        | 此时将打开到基础存储的文件句柄                                                                                                        |

 

### <a name="initializing-the-supported-sensor-properties-and-data-fields"></a>正在初始化的受支持的传感器属性和数据字段

| 模块                  | 类/接口      |
|-------------------------|----------------------|
| Device.cpp              | CMyDevice            |
| SensorDdi.cpp           | CSensorDdi           |
| AccelerometerDevice.cpp | CAccelerometerDevice |
| SpbRequest.cpp          | CSpbRequest          |

 

若要获取的属性和支持的传感器的数据字段的初始化期间，驱动程序时会调用这些方法下面。 对于 Windows 传感器平台，加速感应器属性相对应读取或读写数据，如传感器的报表时间间隔内或其受支持的最小报表时间间隔。 数据字段对应于实际加速感应器读数沿其 X 轴、 y 和 z 轴。 （请注意，此序列的前三个方法是与以前的数据连接和存储请求的对象，序列中的前三个方法相同。）

|     | 方法                                             | 通过调用                                                         | 用途                                                                                                               |
|-----|----------------------------------------------------|--------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------|
| 1   | **CMyDevice::OnPrepareHardware**                   | WUDFx.dll （Windows 用户模式驱动程序框架的组件）。 | 启动所需的操作以便可以访问给定的设备驱动程序。                                     |
| 2   | **CSensorDdi::Initialize**                         | **CMyDevice::OnPrepareHardware**                                   | 创建并初始化传感器设备对象。                                                                      |
| 3   | **CSensorDevice::Initialize**                      | **CSensorDdi::Initialize**                                         | 初始化传感器驱动程序接口、 客户端管理器和报表管理器。                                  |
| 4   | **CSensorDevice::InitializeSensorDriverInterface** | **CSensorDevice::Initialize**                                      | 开始初始化**IPortableDeviceValues**存储的属性键和数据字段值的对象。 |
| 5   | **CSensorDevice::AddPropertyKeys**                 | **CSensorDevice::InitializeSensorDriverInterface**                 | 循环访问支持的属性并添加**PROPERTYKEY**为每个。                                        |
| 6   | **CAccelerometerDevice::GetSupportedProperties**   | **CSensorDevice::AddPropertyKeys**                                 | 获取**PROPERTYKEY**给定的设备的属性的结构。                                                |
| 7   | **CSensorDevice::AddDataFieldKeys**                | **CSensorDevice::InitializeSensorDriverInterface**                 | 循环访问的受支持的数据字段并添加**PROPERTYKEY**为每个。                                       |
| 8   | **CSensorDevice::GetSupportedDataFields**          | **CSensorDevice::AddDataFieldKeys**                                | 获取**PROPERTYKEY**的给定的设备的数据字段。                                                         |

 

### <a name="initializing-the-persistent-unique-id-property"></a>初始化永久唯一 ID 属性

| 模块                  | 类/接口      |
|-------------------------|----------------------|
| Device.cpp              | CMyDevice            |
| SensorDdi.cpp           | CSensorDdi           |
| AccelerometerDevice.cpp | CAccelerometerDevice |
| SensorDevice.cpp        | CSensorDevice        |

 

在初始化来初始化传感器的永久唯一标识符 (PUID) 期间，驱动程序时会调用这些方法下面。 使用 Windows **PUID**在设备会话之间持久保存数据。 （请注意，此序列的前四个方法与以前的属性和数据字段序列中的前四个方法相同。）

|     | 方法                                             | 通过调用                                                         | 用途                                                                                                   |
|-----|----------------------------------------------------|--------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------|
| 1   | **CMyDevice::OnPrepareHardware**                   | WUDFx.dll （Windows 用户模式驱动程序框架的组件）。 | 启动所需的操作以便可以访问给定的设备驱动程序。                         |
| 2   | **CSensorDdi::Initialize**                         | **CMyDevice::OnPrepareHardware**                                   | 创建并初始化传感器设备对象。                                                          |
| 3   | **CSensorDevice::Initialize**                      | **CSensorDdi::Initialize**                                         | 初始化传感器驱动程序接口、 客户端管理器和报表管理器。                      |
| 4   | **CSensorDevice::InitializeSensorDriverInterface** | **CSensorDevice::Initialize**                                      | 启动存储的属性键和数据字段值的对象的初始化。               |
| 5   | **CSensorDevice::SetUniqueID**                     | **CSensorDevice::InitializeSensorDriverInterface**                 | 调用方法，可在会话之间获取驱动程序可以使用的持久性唯一标识符 (PUID)。 |
| 6   | **CAcclerometerDevice::GetSensorObjectID**         | **CSensorDevice::SetUniqueID**                                     | 获取加速感应器的永久标识符 ("ADXL345")。                                               |

 

### <a name="setting-the-default-property-values"></a>设置默认属性值

| 模块                  | 类/接口      |
|-------------------------|----------------------|
| Device.cpp              | CMyDevice            |
| SensorDdi.cpp           | CSensorDdi           |
| AccelerometerDevice.cpp | CAccelerometerDevice |
| SensorDevice.cpp        | CSensorDevice        |

 

Windows 传感器平台支持的传感器类型的默认属性值，制造商的名称、 传感器型号和序列号。 SpbAccelerometer 示例中的代码将这些属性设置为驱动程序和设备初始化阶段的一部分。 下面的方法被调用该驱动程序，初始化过程中，若要设置加速感应器的默认值。 （请注意，此序列的前四个方法中的上一个属性设置序列的前四个方法相同。）

|     | 方法                                             | 通过调用                                                         | 用途                                                                                           |
|-----|----------------------------------------------------|--------------------------------------------------------------------|---------------------------------------------------------------------------------------------------|
| 1   | **CMyDevice::OnPrepareHardware**                   | WUDFx.dll （Windows 用户模式驱动程序框架的组件）。 | 启动所需的操作以便可以访问给定的设备驱动程序。                 |
| 2   | **CSensorDdi::Initialize**                         | **CMyDevice::OnPrepareHardware**                                   | 创建并初始化传感器设备对象。                                                   |
| 3   | **CSensorDevice::Initialize**                      | **CSensorDdi::Initialize**                                         | 初始化传感器驱动程序接口、 客户端管理器和报表管理器。              |
| 4   | **CSensorDevice::InitializeSensorDriverInterface** | **CSensorDevice::Initialize**                                      | 启动存储的属性键和数据字段值的对象的初始化。       |
| 5   | **CAccelerometerDevice::SetDefaultPropertyValues** | **CSensorDevice::InitializeSensorDriverInterface**                 | 设置的默认属性值的加速感应器 （制造商、 型号、 序列号、 等等。） |

 

### <a name="retrieving-the-default-writeable-properties"></a>检索默认可写属性

| 模块                  | 类/接口      |
|-------------------------|----------------------|
| Device.cpp              | CMyDevice            |
| SensorDdi.cpp           | CSensorDdi           |
| AccelerometerDevice.cpp | CAccelerometerDevice |
| SensorDevice.cpp        | CSensorDevice        |

 

Windows 传感器平台支持只读和读写属性的传感器，这是正确的默认属性。 SpbAccelerometer 示例中的代码获取驱动程序和设备初始化阶段的一部分的可写 （或可设置） 的默认属性列表。 下面的方法被调用该驱动程序，初始化过程中，若要获取这些属性的加速感应器。 （请注意，此序列的前四个方法中的上一个属性设置序列的前四个方法相同。）

|     | 方法                                             | 通过调用                                                         | 用途                                                                                           |
|-----|----------------------------------------------------|--------------------------------------------------------------------|---------------------------------------------------------------------------------------------------|
| 1   | **CMyDevice::OnPrepareHardware**                   | WUDFx.dll （Windows 用户模式驱动程序框架的组件）。 | 启动所需的操作以便可以访问给定的设备驱动程序。                  |
| 2   | **CSensorDdi::Initialize**                         | **CMyDevice::OnPrepareHardware**                                   | 创建并初始化传感器设备对象。                                                  |
| 3   | **CSensorDevice::Initialize**                      | **CSensorDdi::Initialize**                                         | 初始化传感器驱动程序接口、 客户端管理器和报表管理器。              |
| 4   | **CSensorDevice::InitializeSensorDriverInterface** | **CSensorDevice::Initialize**                                      | 启动存储的属性键和数据字段值的对象的初始化。       |
| 5   | **CAccelerometerDevice::SetDefaultPropertyValues** | **CSensorDevice::InitializeSensorDriverInterface**                 | 设置的默认属性值的加速感应器 （制造商、 型号、 序列号、 等等。） |

 

### <a name="activating-support-for-events"></a>激活事件的支持

| 模块                  | 类/接口      |
|-------------------------|----------------------|
| Device.cpp              | CMyDevice            |
| SensorDdi.cpp           | CSensorDdi           |
| AccelerometerDevice.cpp | CAccelerometerDevice |
| SensorDevice.cpp        | CSensorDevice        |

 

Windows 传感器平台支持的事件。 应用程序注册事件处理程序从驱动程序获取通知。 有关加速感应器、 超出 （以 G 强制为单位） 的某些变化敏感度或当前报表时间间隔到期时触发这些通知。

若要支持传感器平台中的事件模型，该驱动程序必须激活一个线程来处理事件通知。 若要执行此激活的初始化期间，驱动程序时会调用这些方法下面。 （请注意，此序列的前三个方法中的上一个序列号的前三个方法相同。）

|     | 方法                                         | 通过调用                                                         | 用途                                                                              |
|-----|------------------------------------------------|--------------------------------------------------------------------|--------------------------------------------------------------------------------------|
| 1   | **CMyDevice::OnPrepareHardware**               | WUDFx.dll （Windows 用户模式驱动程序框架的组件）。 | 启动所需的操作以便可以访问给定的设备驱动程序。    |
| 2   | **CSensorDdi::Initialize**                     | **CMyDevice::OnPrepareHardware**                                   | 创建并初始化传感器设备对象。                                    |
| 3   | **CSensorDevice::Initialize**                  | **CSensorDdi::Initialize**                                         | 初始化传感器驱动程序接口、 客户端管理器和报表管理器。 |
| 4   | **CReportManager::Initialize**                 | **CSensorDevice::Initialize**                                      | 创建用于处理事件的线程。                                            |
| 5   | **CReportManager::ActivateDataEventingThread** | **CReportManager::Initialize**                                     | 激活以前方法创建的线程。                                 |

 

### <a name="initializing-the-class-extension"></a>初始化类扩展

| 模块     | 类/接口 |
|------------|-----------------|
| Device.cpp | CMyDevice       |

 

Windows 传感器平台的扩展名为类提供用于获取传感器数据和引发事件通知的标准机制的传感器 api。 示例驱动程序调用**ISensorClassExtension::Initialize**方法来初始化类扩展，它接收到的调用之后**CMyDevice::OnPrepareHardware**。

### <a name="configuring-the-device-and-placing-it-in-standby-mode"></a>配置设备并将其放在备用服务器模式

| 模块                  | 类/接口      |
|-------------------------|----------------------|
| Device.cpp              | CMyDevice            |
| SensorDdi.cpp           | CSensorDdi           |
| AccelerometerDevice.cpp | CAccelerometerDevice |
| SensorDevice.cpp        | CSensorDevice        |

 

最后一个序列中的设备和驱动程序的初始化方法的配置 ADXL345，并将其放在备用服务器模式。 （这一序列的写入和读取的操作会多次一直重复该设备配置。）

|     | 方法                                          | 通过调用                                                         | 用途                                                                               |
|-----|-------------------------------------------------|--------------------------------------------------------------------|---------------------------------------------------------------------------------------|
| 1   | **CMyDevice::OnD0Entry**                        | WUDFx.dll （Windows 用户模式驱动程序框架的组件）。 | 当新的设备将显示在系统上时调用。                                      |
| 2   | **CSensorDdi::Start**                           | **CMyDevice::OnD0Entry**                                           | 调用 CSensorDevice::Start 的传递方法。                                |
| 3   | **CSensorDevice::Start**                        | **CSensorDdi::Start**                                              | 启动设备配置过程。                                           |
| 4   | **CAccelerometerDevice::ConfigureHardware**     | **CSensorDevice::Start**                                           | 启动值写入指定的注册表，其中 ADXL345 的操作。 |
| 5   | **CAcclerometerDevice::WriteRegister**          | **CAccelerometerDevice::ConfigureHardware**                        | 启动值写入指定的注册表，其中 ADXL345 的操作。 |
| 6   | **CSpbRequest::CreateAndSendWrite**             | **CAcclerometerDevice::WriteRegister**                             | 通过 I2C 总线将传输写入请求                                          |
| 7   | **CAcclerometerDevice::ReadRegister**           | **CAccelerometerDevice::ConfigureHardware**                        | 启动操作，用于读取来自指定 ADXL345 寄存器的值。       |
| 8   | **CSpbRequest::CreateAndSendWriteReadSequence** | **CAcclerometerDevice::ReadRegister**                              | 通过 I2C 总线接收读取的结果。                                           |
| 9   | **CSpbRequest::CreateAndSendIoctl**             | **CSpbRequest::CreateAndSendWriteReadSequence**                    | 创建并发送 IOCTL 请求的帮助器方法。                                |

 

大多数设备配置工作都是通过一系列**CAccelerometerDevice::WriteRegister**并**CAccelerometerDevice::ReadRegister**方法调用。 驱动程序使用::**WriteRegister**方法以将值写入 ADXL345 之一注册; 然后会检查返回的相应的值::**ReadRegister**方法以验证是否在写入操作成功。 下面是一系列完整写入和读取的操作。

|     | 方法                                  | 注册 | 数据                | 用途                                                                                                            |
|-----|-----------------------------------------|----------|---------------------|--------------------------------------------------------------------------------------------------------------------|
| 1   | **CAccelerometerDevice::WriteRegister** | **0x2d** | **'\\0' (0x00)**    | 重置传感器的电源控制寄存器，同时让设备处于备用模式。                                   |
| 2   | **CAccelerometerDevice::ReadRegister**  | **0x2d** | **'\\0' (0x00)**    | 返回的注册值表示写入操作成功。                                          |
| 3   | **CAccelerometerDevice::WriteRegister** | **0x31** | **'\\v' (0x0b)**    | 设置范围为每个轴的 + /-16 G 的高分辨率模式中的设备。                                   |
| 4   | **CAccelerometerDevice::ReadRegister**  | **0x31** | **'\\v' (0x0b**     | 返回的注册值表示写入操作成功。                                          |
| 5   | **CAccelerometerDevice::WriteRegister** | **0x38** | **'\\0' (0x00)**    | 将传感器的先进先出控制寄存器重置为绕过模式。                                                      |
| 6   | **CAccelerometerDevice::ReadRegister**  | **0x38** | **'\\0' (0x00)**    | 返回的注册值表示写入操作成功。                                          |
| 7   | **CAccelerometerDevice::WriteRegister** | **0x2C** | **'\\a' (0x07)**    | 设置 BW\_速率注册，以启动低能耗模式。                                                             |
| 8   | **CAccelerometerDevice::ReadRegister**  | **0x2C** | **'\\a' (0x07)**    | 返回的注册值表示写入操作成功。                                          |
| 9   | **CAccelerometerDevice::WriteRegister** | **0x24** | **'\\x1' (0x01)**   | 设置 TRESH\_ACT （活动阈值） 注册为 1。                                                            |
| 10  | **CAccelerometerDevice::ReadRegister**  | **0x24** | **'\\x1' (0x01)**   |                                                                                                                    |
| 11  | **CAccelerometerDevice::WriteRegister** | **0x27** | **(0xf0)**          | 设置 ACT\_INACT\_CTL （活动/非活动） 注册到 0xf0。                                                       |
| 12  | **CAccelerometerDevice::ReadRegister**  | **0x27** | **(0xf0)**          | 返回的寄存器值指示写操作成功。                                              |
| 13  | **CAccelerometerDevice::WriteRegister** | **0x2f** | **'\\0x10' (0x10)** | 设置 INT\_映射 （中断映射） 注册。 值为 0x10 请求水印映射到 INT2 pin。 |
| 14  | **CAccelerometerDevice::ReadRegister**  | **0x2f** | **'\\0x10' (0x10)** | 返回的寄存器值指示写入操作成功。                                          |

 

在配置的驱动程序和设备后，初始化序列已完成，应用程序可以开始接收传感器数据。

 

 




