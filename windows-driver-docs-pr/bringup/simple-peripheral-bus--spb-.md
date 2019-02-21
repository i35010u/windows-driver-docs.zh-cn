---
title: 简单的外围总线 （存储）
description: SoC 集成电路充分利用简单，低-pin-计数，和低功耗序列互连设备连接到外围设备平台。
ms.assetid: E85BDD36-7ECE-47DB-A770-E28DA8383BA2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dcdbec4748deb281f462f2416f865f1dfb89d30a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525079"
---
# <a name="simple-peripheral-bus-spb"></a>简单的外围总线 （存储）


简单的芯片 (SoC) 集成电路进行广泛使用的系统，用于连接到平台外围设备互连低 pin 计数和低功耗的序列。 I²C、 SPI 和 UARTs 是示例。 对于基于 SoC 的平台，Windows 提供了常规的简单外围总线 （存储） 硬件抽象和这种抽象形式需要高级配置和电源接口 (ACPI) 命名空间的新支持。

## <a name="spb-controller-devices"></a>存储控制器设备


存储控制器设备标识以及分配供应商的硬件 ID 的命名空间中 (\_HID) 和一组使用的资源 (\_CRS)。

### <a name="spb-namespace-objects"></a>存储命名空间对象

存储控制器和外围设备连接到它们，通过 ACPI 枚举。 使用串行总线连接资源描述符描述它们之间的连接。 详细信息，请参阅部分 6.4.3.8，"连接描述符"的[ACPI 5.0 规范](https://www.uefi.org/specifications)。

### <a name="spb-resource-descriptors"></a>存储资源描述符

与 GPIO 连接情况一样，存储连接均由正在使用的设备，通过新的资源描述符操作系统描述。 通用串行总线资源描述符用于声明 I²C 连接、 SPI 连接和 UART 连接，并且可以扩展以在将来支持其他串行总线类型。

用于这些描述符的资源模板宏 19.5.55，部分所述"I2CSerialBus （I2C 串行总线连接资源描述符宏）"的[ACPI 5.0 规范](https://www.uefi.org/specifications)。

### <a name="genericserialbus-opregions"></a>GenericSerialBus OpRegions

此外与 GPIO 类似，ACPI 5.0 定义 OpRegion 用于存储控制器，GenericSerialBus （部分 5.5.2.4.5 ACPI 5.0 规范）。 由于 SPBs 通信总线，GenericSerialBus OpRegions 支持各种协议用于访问存储的目标设备。 有关详细信息，请参阅 》 的部分 5.5.2.4.5.3，"使用 GenericSerialBus 协议"， [ACPI 5.0 规范](https://www.uefi.org/specifications)。

通常使用 SPBs，是 ASL 控制方法，以与设备操作系统的驱动程序共享到的存储目标设备的访问权限的必要条件。 若要确保这些访问的同步，ACPI 5.0 定义设备锁定互斥体 (\_DLM) 对象。 有关详细信息，请参阅部分 5.7.5 [ACPI 5.0 规范](https://www.uefi.org/specifications)。

 

 




