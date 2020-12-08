---
title: 简单外设总线 (SPB)
description: SoC 集成线路广泛使用简单、低 pin 计数和低功耗串行互连，以便连接到平台外围设备。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 989fb0c80bd1eccfde23647fbfb671625faaff25
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96783585"
---
# <a name="simple-peripheral-bus-spb"></a>简单外设总线 (SPB)


芯片上的系统 (SoC) 集成线路广泛使用简单、低 pin 计数和低功耗串行互连，以便连接到平台外围设备。 例如，UARTs。 对于基于 SoC 的平台，Windows 为简单的外围总线 (SPB) 硬件提供常规抽象，此抽象需要高级配置和电源接口 (ACPI) 命名空间中的新支持。

## <a name="spb-controller-devices"></a>SPB 控制器设备


在命名空间中标识一个 SPB 控制器设备，其中包含供应商分配的硬件 ID (\_ HID) 和 (CRS) 使用的一组资源 \_ 。

### <a name="spb-namespace-objects"></a>SPB 命名空间对象

通过 ACPI 枚举 SPB 控制器和连接到它们的外围设备。 使用串行总线连接资源描述符描述它们之间的连接。 有关详细信息，请参阅 [ACPI 5.0 规范](https://uefi.org/specifications)的 "连接描述符" 一节。

### <a name="spb-resource-descriptors"></a>SPB 资源描述符

与 GPIO 连接情况一样，通过使用新的资源描述符，使用设备将 SPB 连接介绍给操作系统。 通用串行总线资源描述符用于声明 I e 连接、SPI 连接和 UART 连接，并且可以进行扩展以支持将来的其他串行总线类型。

有关这些描述符的资源模板宏，请参阅 [ACPI 5.0 规范](https://uefi.org/specifications)的 "I2CSERIALBUS (I2C 串行总线连接资源描述符宏) " 一节。

### <a name="genericserialbus-opregions"></a>GenericSerialBus OpRegions

与 GPIO 类似，ACPI 5.0 定义了 OpRegion 以与 SPB 控制器一起使用，GenericSerialBus (5.5.2.4.5 的 ACPI 5.0 规范) 。 由于 SPBs 是通信总线，因此 GenericSerialBus OpRegions 支持用于访问 SPB 目标设备的各种协议。 有关详细信息，请参阅 [ACPI 5.0 规范](https://uefi.org/specifications)的 "使用 GenericSerialBus 协议" 部分。

通常使用 SPBs，ASL 控制方法需要使用该设备的操作系统驱动程序来共享对 SPB 目标设备的访问。 为了确保这些访问的同步，ACPI 5.0 (DLM) 对象定义设备锁互斥体 \_ 。 有关详细信息，请参阅 [ACPI 5.0 规范](https://uefi.org/specifications)的5.7.5 部分。

 

 




