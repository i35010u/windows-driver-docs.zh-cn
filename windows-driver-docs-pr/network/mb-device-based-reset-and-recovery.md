---
title: MB 基于设备的重置和恢复
description: MB 基于设备的重置和恢复
ms.assetid: CA75B63B-53EE-41BF-B2B6-E008F5598399
keywords:
- MB 基于设备的重置和恢复、 基于移动宽带设备的重置和恢复、 移动宽带的微型端口驱动程序基于设备的重置和恢复
ms.date: 08/09/2018
ms.localizationpriority: medium
ms.openlocfilehash: 72fa51716e5a80dbdfe838888b721179a662e405
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577467"
---
# <a name="mb-device-based-reset-and-recovery"></a>MB 基于设备的重置和恢复

基于设备的移动宽带 （MB 或 MBB） 重置和恢复是一种技术在 Windows 10 中，引入了用于 MBB 设备和驱动程序的可靠重置恢复机制的 1809年和更高版本。 此机制，MBB 设备，以避免会导致不正常工作，断开连接或无响应操作的命令，最终使用户体验无缝，如果发生错误并减少了无需重新启动的可能性丢失的失败系统。 

使用或不带固件依赖项，可以实现基于设备的重置和恢复。 IHV 或 OEM 合作伙伴可以使用受支持的设备扩展在所有 Windows Pc 上提供的基于软件的重置机制或固件级别重置机制，以提高成功恢复的速率。

## <a name="mb-device-based-reset-and-recovery-architecture-overview"></a>MB 基于设备的重置和恢复体系结构概述

Windows MBB 服务初始化和控制使用标准的移动电话网络设备[移动宽带接口模型](http://www.usb.org/developers/docs/devclass_docs/MBIM10Errata1_073013.zip "MBIM 规范")(MBIM) 接口，这基于 USB 传输扩展NCM 规范中。 发送到 IHV 设备每个命令将发送为 MBIM 命令通过收件箱 Windows MBB 类驱动程序。 使用 MBIM 协议交换初始化蜂窝调制解调器时，数据路径可以启动主机、 调制解调器，请与网络之间。 通过并行 MBIM 协议 exchange 继续发送到移动电话的设备的其他任何控件。 

有多种 MBIM 控制路径和数据路径上发生的故障。 在版本的 Windows 10，版本 1809 之前, 的 Windows 生成简单的错误处理机制。 每当发送 MBIM 命令和设备变得无响应，该机制会尝试将设备重置通过发送 MBIM 重置命令。 但是，因为故障通常是由于无响应的 MBIM 接口第一个位置中，此重置并非始终有效。 此外，该机制不会解决可能发生数据路径故障导致连接丢失的其他故障。 

MB 基于设备的重置和恢复引入了一个集中式的框架，用于检测具有一系列以渐进方式有影响力的重置更广的故障并协调恢复。 如果设备支持设备级重置，基于 MB 设备的重置和恢复将包含已耗尽后所有基于软件的重置设备级别重置。 重置和恢复 framework 重新定义，并替换现有重置基于 MBIM 命令响应能力的机制。  

MB 基于设备的重置和恢复检测，从而纠正以下类型的故障：

| 故障的区域        | 失败描述                                         |
|------------------------|-------------------------------------------------------------|
| 控制路径           | <ul><li>MBIM 协议路径上检测到挂起的情况。 有关挂起检测的详细信息，请参阅[MB 挂起检测](mb-hang-detection.md)。</li><li>由于使用不正确的状态和/或信息 MBB reponding 导致的失败。</li></ul> |
| 数据路径              | <ul><li>设备端故障导致数据路径失败。 例如，终结点不 reponding 数据流量，损坏的数据从物理，等等。</li><li>调制解调器/网络端失败。 例如，网络不 repsonding IP 通信、 DNS 失败、 数据包丢失等。</li></ul> |

某些故障不是可操作从恢复角度看，包括但不是限于：

- 预配或激活相关的问题，例如缺少 COSA 设置或 MO 发起服务拒绝
- 由于驱动程序初始化失败 （电源或硬件相关） 或软件错误的控制路径问题

但是，一旦检测到可操作失败，则基于 MB 设备的重置和恢复将尝试以下重置机制。 Windows 将执行，从最小的顺序列出了重置的选项为大多数有影响。 

基于软件的重置选项下, 表中所有 Windows 10，版本 1809 MBB 设备上可用，可禁用或由 OEM 合作伙伴配置。

| 重置序列 | 重置类型    | 重置机制 |
| ---------------|-------------- | --------------- |
| 1              | 仅软件 | 停用和激活 PDP 上下文 |
| 2              | 仅软件 | 切换飞行模式 (APM) 开/关 |
| 3              | 仅软件  | 启用/禁用级别插 (PnP) 设备 |

由 Oem MBB 设备/固件功能使用情况下，以下基于设备的重置选项处于启用状态。 

| 重置序列 | 重置类型   | 重置机制 |
| -------------- |------------- | --------------- |
| 4              | 基于设备的 | 功能级别的设备重置 （文件夹数） |
| 5              | 基于设备的 | 平台级别的设备重置 (PLDR) |

更改恢复顺序，并且在某些情况下重置某些机制绕过，对于某些类型的故障。 例如，如果命令超时发生时切换飞行模式，OS 不会切换飞行模式来修复此错误。 如果 MBB 设备不响应任何 MBIM 命令，然后操作系统将交流的基于设备的重置机制直接。

启用 MBIM 函数中，Windows 10 的 UDE 客户端驱动程序版本 1809年包含一个新 API，可用于请求重置，只要 UDECx 客户端驱动程序检测到错误。 以下部分介绍这些新的基于设备的重置机制，包括文件夹数、 PLDR 和 UDECx 为 PCI 重置。

## <a name="device-based-resets"></a>基于设备的重置

### <a name="function-level-device-reset-fldr"></a>函数级设备重置 （文件夹数）

函数级设备重置为最亮基于设备的重置方面对系统的影响。 它在设备内，会发生情况并对其他设备，都不可见，设备就会保持连接到在重置整个总线而过程完成后返回到有效状态 （即，初始状态）。 这可以通过任一总线驱动程序或固件提供。 如果总线规范定义了一种带内重置机制，能够满足要求，总线驱动程序实现的文件夹数处理程序。 固件编写器可能会替代总线定义具有其自己的实现使用带外信号，如重置行或切换电源，仍遵循 FLDR 的要求的文件夹数的文件夹数。 

### <a name="platform-level-device-reset-pldr"></a>平台级别的设备重置 (PLDR)  

平台级别设备重置为的情况下无法使用的文件夹数，或作为文件夹数的最后使用的补充。 此机制的原因将设备重置被报告为缺少的总线 （在一个电源周期内，例如） 或影响多个设备 (如共享 power 铁路或重置在设备之间的行)。 重置方法可能会作为切换专用重设行或关闭再打开 D3 power 资源实现的 ACPI 表中指定。 PLDR 执行时，操作系统将关闭并重新生成所有受影响的设备以确保所有内容从原始状态开始的堆栈。

### <a name="reset-recovery-for-ude-devices"></a>重置 UDE 设备的恢复 

对于启用 MBIM 函数中，Windows 10 的 UDE 客户端驱动程序版本 1809年包括可用于请求重置，只要 UDECx 客户端驱动程序检测到错误的 API。 客户端驱动程序通过调用新方法，请求重置[ **UdecxWdfDeviceNeedsReset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxwdfdevice/nf-udecxwdfdevice-udecxwdfdeviceneedsreset)，指定重置类型，其目的是 UDECx 要尝试的设备 （如果支持）。 重置这些密钥类型是**PlatformLevelDeviceReset**并**FunctionLevelDeviceReset**的值，并且[ **UDECX_WDF_DEVICE_RESET_TYPE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxwdfdevice/ne-udecxwdfdevice-_udecx_wdf_device_reset_type)枚举。 UDECx 后启动时重置，将调用的驱动程序[ *EVT_UDECX_WDF_DEVICE_RESET* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxwdfdevice/nc-udecxwdfdevice-evt_udecx_wdf_device_reset)回调函数，并确保在此过程中调用任何其他回调时。 客户端驱动程序需要执行任何重置相关的操作，如释放任何资源，则信号重置完成，通过调用[ **UdecxWdfDeviceResetComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxwdfdevice/nf-udecxwdfdevice-udecxwdfdeviceresetcomplete)。

以下流程图说明了 UDE 设备重置过程。

![重置恢复流 UDECx 客户端驱动程序的流](images/mb-self-healing-udecx-reset.png "UDECx 客户端的重置恢复驱动程序调用流。")


## <a name="requirements-for-mb-device-based-reset-and-recovery"></a>MB 基于设备的重置和恢复要求

### <a name="requirements-for-fldr"></a>要求的文件夹数

若要支持的设备上，必须有 Device() 范围内的文件夹数`_RST`定义的方法。 执行时，该方法必须重置仅该设备，并且不应接触另一台设备。 设备还必须保持连接到总线上。 

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

在 PLDR，其他设备重置受影响的设备都表示为共享`PowerResource`重置。 设备声明对其依赖关系`PowerResource`重置，并且`PowerResource`实现`_RST`方法。 

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

此外，PLDR 可以通过将设备放入 D3Cold 电源状态并返回到 D0 (实质上是电源周期设备）。 在这种情况下，具有`_PR3`声明作用域的设备中是否足以支持 PLDR。 将使用 ACPI`_PR3`来确定重置设备之间的依赖项，如果没有`_PRR`引用设备作用域中。 有关详细信息，请参阅[重置和恢复设备](../kernel/resetting-and-recovering-a-device.md)。 

## <a name="related-links"></a>相关链接

[MB 挂起检测](mb-hang-detection.md)

[**UDECX_WDF_DEVICE_RESET_TYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxwdfdevice/ne-udecxwdfdevice-_udecx_wdf_device_reset_type)

[**UdecxWdfDeviceNeedsReset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxwdfdevice/nf-udecxwdfdevice-udecxwdfdeviceneedsreset)

[*EVT_UDECX_WDF_DEVICE_RESET*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxwdfdevice/nc-udecxwdfdevice-evt_udecx_wdf_device_reset)

[**UdecxWdfDeviceResetComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxwdfdevice/nf-udecxwdfdevice-udecxwdfdeviceresetcomplete)
