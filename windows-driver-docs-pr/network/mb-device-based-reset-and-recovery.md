---
title: MB 基于设备的重置和恢复
description: MB 基于设备的重置和恢复
ms.assetid: CA75B63B-53EE-41BF-B2B6-E008F5598399
keywords:
- MB 基于设备的重置和恢复、基于移动宽带设备的重置和恢复、移动宽带微型端口驱动程序基于设备的重置和恢复
ms.date: 08/09/2018
ms.localizationpriority: medium
ms.openlocfilehash: 31ef7e6948b947ae105ff895aaa3ab8c21601f7a
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89207525"
---
# <a name="mb-device-based-reset-and-recovery"></a>MB 基于设备的重置和恢复

移动宽带 (MB 或 MBB) 基于设备的重置和恢复，是 Windows 10 版本1809及更高版本中的一项技术，为 MBB 设备和驱动程序引入了强大的重置恢复机制。 这种机制可让 MBB 设备避免发生故障、连接断开或操作命令的故障，最终使用户体验无缝发生（如果发生错误）并降低不得不重新启动系统的机会。 

基于设备的重置和恢复可以通过或不带固件依赖项实现。 IHV 或 OEM 合作伙伴可以使用支持的设备或固件级重置机制来扩展所有 Windows 电脑上可用的基于软件的重置机制，以提高恢复成功的速度。

## <a name="mb-device-based-reset-and-recovery-architecture-overview"></a>MB 基于设备的重置和恢复体系结构概述

Windows MBB 服务使用标准 [移动宽带接口模型](https://www.usb.org/developers/docs/devclass_docs/MBIM10Errata1_073013.zip "MBIM 规范") （ (MBIM) 接口，此接口是在 USB 传输扩展 NCM 规范的基础上构建的，它可初始化和控制移动设备。 发送到 IHV 设备的每个命令都通过收件箱 Windows MBB 类驱动程序发送为 MBIM 命令。 使用 MBIM 协议交换初始化蜂窝调制解调器后，可以在主机、调制解调器和网络之间启动数据路径。 发送到移动电话设备的任何其他控件将通过 MBIM 协议进行并行传输。 

在 MBIM 控制路径和数据路径上都可能会发生许多故障。 在 Windows 10 版本1809之前的 Windows 版本中，内置了简单的错误处理机制。 每当发送 MBIM 命令并且设备变得无响应时，该机制会尝试通过发送 MBIM reset 命令重置设备。 但是，因为故障通常是由于第一次 MBIM 接口无响应而导致的，所以此重置并不总是有效。 此外，该机制不会解决可能出现的其他故障，例如数据路径故障导致连接断开。 

MB 基于设备的重置和恢复引入了一个集中式框架，用于检测更大的一组故障并使用一组渐进有影响力重置来协调恢复。 如果设备支持设备级重置，MB 基于设备的重置和恢复将在所有基于软件的重置都用尽后合并设备级重置。 重置和恢复框架将重新定义，并根据 MBIM 命令响应能力替换现有的重置机制。  

MB 基于设备的重置和恢复检测和尝试解决以下类型的故障：

| 故障区域        | 失败描述                                         |
|------------------------|-------------------------------------------------------------|
| 控制路径           | <ul><li>在 MBIM 协议路径上检测到挂起状态。 有关挂起检测的详细信息，请参阅 [MB 挂起检测](mb-hang-detection.md)。</li><li>由于 MBB reponding 的状态和/或信息错误而失败。</li></ul> |
| 数据路径              | <ul><li>设备端故障导致数据路径故障。 例如，终结点不 reponding 数据流量，损坏的数据来自 PHY，等等。</li><li>调制解调器/网络故障。 例如，网络无法 repsonding 到 IP 流量、DNS 失败、数据包丢失，等等。</li></ul> |

某些故障无法从恢复角度进行操作，包括但不限于：

- 预配或与激活相关的问题，例如缺少 COSA 设置或 MO 启动的服务拒绝
- 由于驱动程序初始化失败导致的控制路径问题 (与电源或硬件相关的) 或软件 bug

但是，一旦检测到可操作的故障，基于 MB 设备的重置和恢复将尝试以下重置机制。 "重置" 选项按 Windows 执行的顺序列出，最少为有影响力。 

下表中的基于软件的重置选项在所有 Windows 10 版本 1809 MBB 设备上可用，并可通过 OEM patners 禁用或配置。

| 重置序列 | 重置类型    | 重置机制 |
| ---------------|-------------- | --------------- |
| 1              | 仅软件 | 停用和激活 PDP 上下文 |
| 2              | 仅软件 | 切换飞行模式 (APM) 开/关 |
| 3              | 仅软件  | 在即插即用 (PnP) 级别启用/禁用设备 |

使用 MBB 设备/固件功能的 Oem 启用了以下基于设备的重置选项。 

| 重置序列 | 重置类型   | 重置机制 |
| -------------- |------------- | --------------- |
| 4              | 基于设备 | 功能级别设备重置 (FLDR)  |
| 5              | 基于设备 | 平台级别设备重置 (PLDR)  |

恢复顺序已更改，在某些情况下，对于某些类型的故障，某些情况下会绕过某些类型的重置机制。 例如，如果在切换飞行模式时出现命令超时，则操作系统不会切换飞行模式来修复它。如果 MBB 设备不响应任何 MBIM 命令，则操作系统会直接与基于设备的重置机制联系。

对于启用 MBIM 函数的 UDE 客户端驱动程序，Windows 10 1809 版包含一个新的 API，可用于在 UDECx 客户端驱动程序检测到错误时请求重置。 以下部分介绍了这些新的基于设备的重置 mechanims，包括 PCI 的 FLDR、PLDR 和 UDECx reset。

## <a name="device-based-resets"></a>基于设备的重置

### <a name="function-level-device-reset-fldr"></a>功能级设备重置 (FLDR) 

在系统影响方面，函数级设备重置是基于设备的最浅重置。 它发生在设备内部，并对其他设备不可见，在整个重置过程中，该设备保持连接到总线，并返回到有效状态 (换言之，在该过程之后) 初始状态。 这可以由总线驱动程序或固件提供。 如果总线规范定义满足要求的带内重置机制，则总线驱动程序实现 FLDR 处理程序。 固件编写器可能会使用其自己的 FLDR 实现（如重置线路或电源切换）替代总线定义的 FLDR，但仍遵循 FLDR 的要求。 

### <a name="platform-level-device-reset-pldr"></a>平台级别设备重置 (PLDR)   

对于不能使用 FLDR 或作为 FLDR 的最后滑雪场补充的情况，平台级设备重置。 这种重置机制导致在电源周期中将设备报告为缺少总线 (，例如) 或影响多台设备 (如共享电源导轨或设备) 中的重置线路。 在 ACPI 表中指定了 reset 方法，该方法可能会实现为切换专用重置线路或对 D3 电源资源进行重启。 执行 PLDR 时，OS 会泪水并重建所有受影响设备的堆栈，以确保一切都从处于纯洁状态启动。

### <a name="reset-recovery-for-ude-devices"></a>重置 UDE 设备的恢复 

对于启用 MBIM 函数的 UDE 客户端驱动程序，Windows 10 1809 版包含一个 API，可用于在 UDECx 客户端驱动程序检测到错误时请求重置。 客户端驱动程序通过调用新方法 [**UdecxWdfDeviceNeedsReset**](/windows-hardware/drivers/ddi/udecxwdfdevice/nf-udecxwdfdevice-udecxwdfdeviceneedsreset)指定重置类型（如果支持) ，则指定它希望 UDECx 尝试设备 (）。 这些重置类型包括 **PlatformLevelDeviceReset** 和 **FunctionLevelDeviceReset** ，它们是 [**UDECX_WDF_DEVICE_RESET_TYPE**](/windows-hardware/drivers/ddi/udecxwdfdevice/ne-udecxwdfdevice-_udecx_wdf_device_reset_type) 枚举的值。 启动重置后，UDECx 将调用驱动程序的 [*EVT_UDECX_WDF_DEVICE_RESET*](/windows-hardware/drivers/ddi/udecxwdfdevice/nc-udecxwdfdevice-evt_udecx_wdf_device_reset) 回调函数，并确保在此过程中不会调用任何其他回调。 客户端驱动程序应执行任何重置相关操作（如释放任何资源），然后通过调用 [**UdecxWdfDeviceResetComplete**](/windows-hardware/drivers/ddi/udecxwdfdevice/nf-udecxwdfdevice-udecxwdfdeviceresetcomplete)来完成信号重置。

以下流程图说明了 UDE 设备重置过程。

![UDECx 客户端驱动程序的重置恢复流的流](images/mb-self-healing-udecx-reset.png "UDECx 客户端驱动程序的重置恢复的调用流。")


## <a name="requirements-for-mb-device-based-reset-and-recovery"></a>基于设备的重置和恢复的要求

### <a name="requirements-for-fldr"></a>FLDR 的要求

若要支持设备上的 FLDR，设备 ( # A1 范围内必须 `_RST` 定义一个方法。 执行时，该方法必须仅重置该设备，而不应触摸另一台设备。 设备还必须在总线上保持连接状态。 

```cpp
Device(PCI0)  
{  
Device(USB0)  
{  
    Name(_ADR, 0x1d0000)  
    Name(_S4D, 0x2)  
    Name(_S3D, 0x2)  
    …  
    Method(_RST, 0x0, NotSerialized)  
    {  
            //  
            // Perform reset of the USB0 device  
            //  
    } 
} 
} 
```

### <a name="requirements-for-pldr"></a>PLDR 的要求

在 PLDR 中，受其他设备重置影响的设备表示为 "共享" `PowerResource` 以进行重置。 设备声明它们对的依赖项 `PowerResource` 以重置，并 `PowerResource` 实现 `_RST` 方法。 

```cpp
Device(PCI0)  
{  
PowerResource(URST, 0x5, 0x0)  
{  
    //  
    // Dummy _ON and _OFF methods. All power resources must have these  
    // two defined.  
    // Method(_ON, 0x0, NotSerialized)  
    {  
    }  
    Method(_OFF, 0x0, NotSerialized)  
    {  
    }  
    Method(_RST, 0x0, NotSerialized)  
    {  
            //  
            // Perform reset of the USB0 and USB1 devices  
            //  
    } 
}  
Device(USB0)  
{  
    Name(_ADR, 0x1d0000)  
    Name(_S4D, 0x2)  
    Name(_S3D, 0x2)  
    …  
    Name(_PRR, Package(0x1) { ^URST })  
}  
Device(USB1)  
{  
    Name(_ADR, 0x1d0001)  
    Name(_S4D, 0x2)  
    Name(_S3D, 0x2)  
    …  
    Name(_PRR, Package(0x1) { ^URST })  
} 
} 
```

或者，可以通过将设备置于 D3Cold 电源状态并返回到 D0 来实现 PLDR，实质上是重新启动设备。 在这种情况下， `_PR3` 在设备范围内声明足以支持 PLDR。 `_PR3`如果设备范围内未引用任何设备，ACPI 将使用来确定设备之间的重置依赖项 `_PRR` 。 有关详细信息，请参阅 [重置和恢复设备](../kernel/resetting-and-recovering-a-device.md)。 

## <a name="related-links"></a>相关链接

[MB 挂起检测](mb-hang-detection.md)

[**UDECX_WDF_DEVICE_RESET_TYPE**](/windows-hardware/drivers/ddi/udecxwdfdevice/ne-udecxwdfdevice-_udecx_wdf_device_reset_type)

[**UdecxWdfDeviceNeedsReset**](/windows-hardware/drivers/ddi/udecxwdfdevice/nf-udecxwdfdevice-udecxwdfdeviceneedsreset)

[*EVT_UDECX_WDF_DEVICE_RESET*](/windows-hardware/drivers/ddi/udecxwdfdevice/nc-udecxwdfdevice-evt_udecx_wdf_device_reset)

[**UdecxWdfDeviceResetComplete**](/windows-hardware/drivers/ddi/udecxwdfdevice/nf-udecxwdfdevice-udecxwdfdeviceresetcomplete)