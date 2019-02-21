---
title: 示例驱动程序 I/O 模型
description: 存储驱动程序通过简单的外围总线、 系统 GPIO 插针和资源中心进行通信。 这里可以看到在用户模式和内核模式下，实际的硬件组件的组织方式。
ms.assetid: 86DA1BDE-DD97-45CA-884D-12BD279BD12E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a44f21c66e456c0066fcb3bcd7c8b0ba43271928
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526549"
---
# <a name="sample-driver-io-model"></a>示例驱动程序 I/O 模型


存储驱动程序通过简单的外围总线、 系统 GPIO 插针和资源中心进行通信。 在这里可以看到组件中的组织方式： 用户模式和内核模式下，实际的硬件。

![驱动程序 i/o 模型](images/io.png)

## <a name="simple-peripheral-bus-spb"></a>简单的外围总线 （存储）


Windows 8.1 支持存储组件作为类扩展插件 （在内核模式下运行），使开发和实现存储控制器驱动程序更容易。 存储组件：

-   资源中心包括注册和设置检索处理所有通信。
-   实现分层的队列结构来管理同步目标和总线锁定请求
-   将转换到内核模式从用户模式缓冲区

有关详细信息请参阅[简单的外围总线](https://docs.microsoft.com/windows-hardware/design/component-guidelines/simple-peripheral-bus--spb-)。

### <a name="spb-component-and-the-sample-driver"></a>存储组件和示例驱动程序

| 模块         | 类/接口 |
|----------------|-----------------|
| SpbRequest.cpp | CSpbRequest     |

 

示例代码与存储组件交互的 SpbAccelerometer SpbRequest.cpp 中找到。 按如下所述，与此组件进行交互 CSpbRequest 类中的三个方法。

| 方法                                          | 用途                                       |
|-------------------------------------------------|-----------------------------------------------|
| **CSpbRequest::CreateAndSendIoctl**             | 创建并发出一个 IOCTL 请求。          |
| **CSpbRequest::CreateAndSendWrite**             | 创建并发出存储写入               |
| **CSpbRequest::CreateAndSendWriteReadSequence** | 创建并发出存储读/写序列。 |

 

## <a name="general-purpose-inputoutput-gpio"></a>常规用途输入/输出 (GPIO)

Windows 8.1 支持驻留在同一级别作为内核模式存储组件的 GPIO 类扩展。 同时提供驱动程序的客户端的标准接口，该扩展允许在基础硬件连接和 GPIO 位置的灵活性。

在 SoC 平台 GPIO 插针是分散到芯片，以及其他组件，如 SPI 连接调制解调器上公开。

### <a name="the-gpio-component-and-the-sample-driver"></a>GPIO 组件和示例驱动程序

| 模块               | 类/接口 |
|----------------------|-----------------|
| SpbAccelerometer.asl | 不适用             |

 

SpbAccelerometer 示例依赖于中断的 GPIO 组件。 SpbAccelerometer.asl 文件中的 GpioInt() 元素定义已连接到作为中断资源 ADXL345 的 GPIO 插针。

```cpp
//
// Sample I2C and GPIO resources. Modify to match your
// platform's underlying controllers and connections.
// \_SB.I2C and \_SB.GPIO are paths to predefined I2C
// and GPIO controller instances.
//
// Note: as written SpbAccelerometer requires a GPIO resource.
//
I2CSerialBus(0x1D, ControllerInitiated, 400000, AddressingMode7Bit, "\\_SB.I2C", , )
GpioInt(Level, ActiveHigh, Exclusive, PullDown, 0, "\\_SB.GPIO") {1} })
```

下面是 I2C 资源的关键元素：

| 元素    | 描述                                             |
|------------|---------------------------------------------------------|
| 0x1D       | 指定从设备的 I2C 地址。         |
| 400000     | 指定从设备的运行频率。 |
| \\\\SB.I2C | 指定从设备的 ACPI 节点。           |

 

### <a name="processing-acceleration-data"></a>处理加速数据

| 模块                  | 类/接口      |
|-------------------------|----------------------|
| AccelerometerDevice.cpp | CAccelerometerDevice |

 

如果由 ADXL345，示例驱动程序的被动 ISR 例程断言 GPIO 行 (**CAccelerometerDevice::OnInterruptIsr**) 调用。 帮助器函数**CAccelerometerDevice::OnInterruptWorkItem**，处理中断数据的::**OnInterruptIsr**存储。

如果中断处理::**OnInterruptIsr**对应于注册 0x30 (ADXL\_345\_INT\_文件 Adxl345.h 中的源)，该驱动程序调用一个函数注册表，读取操作以获取通过 0x37 0x32 寄存器的内容。 这些寄存器包含 X、 Y 和 z 轴的最新的加速数据。 读取的操作调用中**CAcclerometerDevice::RequestData**方法 (通过调用**CAccelerometerDevice::OnInterruptWorkItem**)。

当::**RequestData**方法处理读取操作的结果，它首先将两个字节的对应于每个轴的数据相结合。 接下来，它将应用的比例因子来获取实际 acceleration 值。 (缩放比例是范围的 G-强制 (32) 除以解决方法的结果 (2 ^13)。 结果是.00390625.).

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

缩放比例由中设置注册 0x31 (数据\_格式)。

## <a name="resource-hub"></a>资源中心

Windows 8.1 支持的资源中心，管理所有设备和总线控制器连接。 它可确保必要的开始和停止排序进行维护。

中心是专门针对 SoC 平台和其平面设备树的组件。 在这些系统上的总线不同于电脑：

-   连接是通常无法发现的;它们在 ACPI 以静态方式定义
-   硬件组件通常具有跨越多个总线，而不是严格的父-子关系的多个依赖项

### <a name="resource-hub-and-the-sample-driver"></a>资源中心和示例驱动程序

| 模块               | 类/接口 |
|----------------------|-----------------|
| SpbAccelerometer.asl | 不适用             |

 

**ResourceTemplate** SpbAccelerometer.asl 节指定资源的连接方式。

```cpp
Name(RBUF, ResourceTemplate()
{
   //
    // Sample I2C and GPIO resources. Modify to match your
    // platform&#39;s underlying controllers and connections.
    // \_SB.I2C and \_SB.GPIO are paths to predefined I2C
    // and GPIO controller instances.
    //
    // Note: as written SpbAccelerometer requires a GPIO resource.
    //
    I2CSerialBus(0x1D, ControllerInitiated, 400000, AddressingMode7Bit, "\\_SB.I2C", , )
    GpioInt(Level, ActiveHigh, Exclusive, PullDown, 0, "\\_SB.GPIO") {1}
        })
Return(RBUF)
```

 

 




