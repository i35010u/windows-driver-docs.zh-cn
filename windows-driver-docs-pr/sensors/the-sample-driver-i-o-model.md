---
title: 示例驱动程序 i/o 模型
description: SPB 驱动程序通过简单的外围总线、系统 GPIO pin 和资源中心进行通信。 可在此处了解如何在用户模式、内核模式和实际硬件中组织组件。
ms.assetid: 86DA1BDE-DD97-45CA-884D-12BD279BD12E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e2d956460a09d22d722b124a365ebf6ef1ab8486
ms.sourcegitcommit: 937974aa9bbe0262a7ffe9631593fab48c4e7492
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2020
ms.locfileid: "90009865"
---
# <a name="sample-driver-io-model"></a>示例驱动程序 i/o 模型


SPB 驱动程序通过简单的外围总线、系统 GPIO pin 和资源中心进行通信。 可在此处查看组件的组织方式：用户模式、内核模式和实际硬件。

![驱动程序 i/o 模型](images/io.png)

## <a name="simple-peripheral-bus-spb"></a>简单外设总线 (SPB)


Windows 8.1 支持将 SPB 组件作为类扩展 (在内核模式下运行，) 使开发和实现 SPB 控制器驱动程序更容易。 SPB 组件：

-   处理与资源中心的所有通信，包括注册和设置检索。
-   实现分层队列结构以管理同时目标和总线锁定请求
-   将缓冲区从用户模式转换为内核模式

有关详细信息，请参阅 [简单外围总线](/windows-hardware/design/component-guidelines/simple-peripheral-bus--spb-)。

### <a name="spb-component-and-the-sample-driver"></a>SPB 组件和示例驱动程序

| 模块         | 类/接口 |
|----------------|-----------------|
| SpbRequest .cpp | CSpbRequest     |

 

SpbAccelerometer 示例代码与 SPB 组件进行交互，可在 SpbRequest 中找到。 CSpbRequest 类中的三种方法与此组件进行交互，如下所述。

| 方法                                          | 目的                                       |
|-------------------------------------------------|-----------------------------------------------|
| **CSpbRequest::CreateAndSendIoctl**             | 创建并发出 IOCTL 请求。          |
| **CSpbRequest::CreateAndSendWrite**             | 创建并颁发 SPB 写入               |
| **CSpbRequest::CreateAndSendWriteReadSequence** | 创建并颁发一个 SPB 写入/读取序列。 |

 

## <a name="general-purpose-inputoutput-gpio"></a>通用输入/输出 (GPIO) 

Windows 8.1 支持与内核模式 SPB 组件位于同一级别的 GPIO 类扩展。 扩展可在基础硬件连接和 GPIO 位置上灵活，同时提供客户端驱动程序的标准接口。

在 SoC 平台上，GPIO 引脚分布在芯片上，并在其他组件（如 SPI 连接的调制解调器）上公开。

### <a name="the-gpio-component-and-the-sample-driver"></a>GPIO 组件和示例驱动程序

| 模块               | 类/接口 |
|----------------------|-----------------|
| SpbAccelerometer. asl | 不可用             |

 

SpbAccelerometer 示例依赖于用于中断的 GPIO 组件。 Asl 文件中的 GpioInt ( # A1 元素将连接到 ADXL345 的 GPIO pin 定义为中断资源。

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
| 0x1D       | 指定从属设备的 I2C 地址。         |
| 400000     | 指定从属设备的运行频率。 |
| \\\\SB.I2C | 为从属设备指定 ACPI 节点。           |

 

### <a name="processing-acceleration-data"></a>处理加速数据

| 模块                  | 类/接口      |
|-------------------------|----------------------|
| AccelerometerDevice .cpp | CAccelerometerDevice |

 

如果 GPIO 行由 ADXL345 断言，则会调用示例驱动程序的被动 ISR 例程 (**CAccelerometerDevice：： OnInterruptIsr**) 。 Helper 函数 **CAccelerometerDevice：： OnInterruptWorkItem**可处理：：**OnInterruptIsr** 存储的中断数据。

如果由：：**OnInterruptIsr** 处理的中断对应于 \_ \_ 在文件 Adxl345) 中注册 0x30 (ADXL 345 INT \_ 源，则驱动程序将调用 register 读取操作，以获取寄存器0x32 到0x37 的内容。 这些寄存器包含 X 轴、Y 轴和 Z 轴的最新加速数据。 读取操作在 **CAcclerometerDevice：： RequestData** 方法中调用， (通过 **CAccelerometerDevice：： OnInterruptWorkItem**) 调用。

当：：**RequestData** 方法处理读取操作的结果时，它首先合并对应于每个轴的两个字节的数据。 接下来，它应用缩放比例以获取实际加速值。  (比例因子是指将 G-力 (32) 的范围除以 (2 ^ 13) 的分辨率。 结果为. 00390625. ) 

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

比例因子由 register 0x31 (数据格式) 中的设置确定 \_ 。

## <a name="resource-hub"></a>资源中心

Windows 8.1 支持一个资源中心，该中心管理所有设备和总线控制器的连接。 它可确保维护必要的开始和结束排序。

中心是专门针对 SoC 平台及其平面设备树的组件。 这些系统上的总线与电脑不同：

-   连接通常是不可发现的;它们是在 ACPI 中静态定义的
-   硬件组件通常具有多个跨越多个总线的依赖关系，而不是严格的父子关系

### <a name="resource-hub-and-the-sample-driver"></a>资源中心和示例驱动程序

| 模块               | 类/接口 |
|----------------------|-----------------|
| SpbAccelerometer. asl | 不可用             |

 

Asl 的 **ResourceTemplate** 节指定了资源的连接方式。

```cpp
Name(RBUF, ResourceTemplate()
{
   //
    // Sample I2C and GPIO resources. Modify to match your
    // platform's underlying controllers and connections.
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

 

