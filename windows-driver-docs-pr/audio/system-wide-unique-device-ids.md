---
title: 系统范围内唯一的设备 ID
description: 系统范围内唯一的设备 ID
keywords:
- 音频适配器 WDK，唯一设备 Id
- 适配器驱动程序 WDK 音频，唯一的设备 Id
- 端口类音频适配器 WDK，唯一的设备 Id
- MF 总线驱动程序 WDK 音频
- 系统提供的多功能设备 WDK 音频
- 多功能音频设备 WDK、音频适配器
- 唯一设备 Id WDK 音频
- 设备 Id WDK 音频
- 标识设备 Id
- subdevices WDK 音频
- 专用总线驱动程序 WDK 音频
- 设备 ID 字符串 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4f08245db44d0a933a96ca5380ca176d09e3d595
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96800531"
---
# <a name="system-wide-unique-device-ids"></a>系统范围内唯一的设备 ID


## <span id="system_wide_unique_device_ids"></span><span id="SYSTEM_WIDE_UNIQUE_DEVICE_IDS"></span>


典型音频适配器的驱动程序应该能够轻松地支持系统中同一音频适配器卡的几个实例。 驱动程序维护的几乎所有数据结构都存储在设备扩展缓冲区中 (查看 [**设备 \_ 对象**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_object) 结构的 **DeviceExtension** 字段的说明) 。 但是，如果驱动程序的多个实例共享任何全局数据，则这些实例应该同步其对此数据的访问。

另外一项要求是，适配器卡的特定实例上的每个 subdevice 都应有一个 [设备 ID 字符串](../install/device-identification-strings.md) ，该字符串唯一标识系统中同一适配器卡的所有实例的 subdevice。

完成此项工作的最直接的方法是将适配器卡上的每个 subdevice 作为逻辑上不同的设备公开到即插即用管理器。 在 [多功能音频设备](multifunction-audio-devices.md)中，此选项显示为选项 (1) 。

另一种方法是使用系统提供的多功能总线驱动程序来管理适配器卡上的 subdevices。 MF 总线驱动程序分配给每个 subdevice 一个设备 ID，该 ID 保证在系统中是唯一的，即使系统包含同一适配器卡的多个实例也是如此。 MF 总线驱动程序适用于 subdevices 共享一组公共配置寄存器的设计，但每个 subdevice 都有其自己的 PCI 基址寄存器集。 Subdevices 应该彼此之间没有隐藏的依赖项，并且应该能够并发操作而不会干扰系统中的其他设备或其他设备。 这是 [多功能音频设备](multifunction-audio-devices.md)中 (2) 的选项。

第三种方法是使用专用总线驱动程序来管理适配器卡上的 subdevices。 如果 subdevices 具有必须集中管理的相互依赖项，则通常需要这样做。 此类依赖项可以通过几种方式发生：

-   Subdevices 可能共享某些卡上资源。 例如，如果 subdevices)  (DSP 共享数字信号处理器，则总线驱动程序可能需要下载在启动第一个 subdevice 之前在 DSP 上运行的专有操作系统。

-   设计缺陷可能会导致 subdevices 之间的依赖关系。 例如，设计缺陷可能要求 subdevices 按特定顺序开启或关闭。

当存在任何类型的依赖项时，专用总线驱动程序几乎总是更好的解决方案，而不是直接向即插即用管理器呈现 subdevices 并尝试隐藏依赖项。

如果为适配器提供自己的总线驱动程序，应确保总线驱动程序分配的设备 Id 在整个系统中是唯一的。

总线驱动程序为其某个子项提供设备 ID，以响应即插即用 manager 中的 [**IRP \_ MN \_ 查询 \_ ID**](../kernel/irp-mn-query-id.md) 查询。 可以通过以下两种方式之一来指定 ID：总线驱动程序通过将 [**设备 \_ 功能**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_capabilities)结构的 **UniqueID** 字段设置为 **TRUE** 或 **FALSE** 来指示其对 [**IRP \_ MN \_ 查询 \_ 功能**](../kernel/irp-mn-query-capabilities.md)查询的响应：

-   **UniqueID**  = **TRUE**

    这意味着保证子名称在整个系统中是唯一的。 设备 ID 字符串包含设备 ID 和实例 ID，这是唯一标识硬件实例的序列号。

-   **UniqueID**  = **FALSE**

    这意味着，子名称只对父对象唯一。 大多数设备使用这种标识。 在这种情况下，即插即用 manager 将扩展接收的设备 ID 字符串，使其在系统中是唯一的。 扩展字符串是父设备的唯一 ID 的函数。

所有音频总线驱动程序都应为其子级设置 **UniqueID**  =  **FALSE** 。 这会导致即插即用 manager 通过添加有关设备的父级的信息来扩展子的设备 ID 字符串，使 ID 在计算机上是唯一的。

 

