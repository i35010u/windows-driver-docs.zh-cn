---
title: 系统范围内唯一设备 Id
description: 系统范围内唯一设备 Id
ms.assetid: 628577b6-05fe-4b63-929f-6d63e93c9266
keywords:
- 音频适配器 WDK，唯一设备 Id
- 适配器驱动程序 WDK 音频的唯一设备 Id
- 端口类音频适配器 WDK，唯一的设备 Id
- MF 总线驱动程序 WDK 音频
- 系统提供的多功能设备 WDK 音频
- 多功能音频设备 WDK，音频适配器
- 唯一的设备 Id WDK 音频
- 设备 Id WDK 音频
- 标识设备 Id
- 子设备 WDK 音频
- 专有总线驱动程序 WDK 音频
- 设备 ID 字符串 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 457fefef9c81a3b7a1bc7fa79f8b0b193f5f73ad
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555419"
---
# <a name="system-wide-unique-device-ids"></a>系统范围内唯一设备 Id


## <span id="system_wide_unique_device_ids"></span><span id="SYSTEM_WIDE_UNIQUE_DEVICE_IDS"></span>


典型的音频适配器的驱动程序轻松应该能够在系统中支持多个实例相同的音频的适配器卡。 存储设备扩展缓冲区中，几乎所有的驱动程序维护的数据结构 (请参阅的说明[**设备\_对象**](https://msdn.microsoft.com/library/windows/hardware/ff543147)结构的**DeviceExtension**字段)。 如果驱动程序的多个实例共享的任何全局数据，但是，这些实例应同步其访问此数据。

一个额外的要求是应具有的适配器的特定实例上每个子[设备 ID 字符串](https://msdn.microsoft.com/library/windows/hardware/ff541224)用于唯一标识子相同的适配器卡的所有实例在系统中。

最简单的方法来实现此目的是将每个适配器卡上的子公开为插管理器的逻辑独立设备。 中显示为选项 (1) 这[多功能音频设备](multifunction-audio-devices.md)。

第二种方法是使用系统提供多功能总线驱动程序来管理上的适配器卡子设备。 MF 总线驱动程序将保证是唯一在系统中，即使系统包含多个实例相同的适配器卡的设备 ID 分配给每个子。 MF 总线驱动程序还包含在其中子设备共享一组通用的配置注册表，但每个子有其自己的 PCI 基址寄存器集的设计。 子设备应相互没有任何隐藏依赖关系，并且应该能够同时运行而不会影响系统中或与其他设备。 这是中的选项 (2)[多功能音频设备](multifunction-audio-devices.md)。

第三种方法是使用专有总线驱动程序来管理上的适配器卡子设备。 如果子设备必须集中管理的相互依赖项通常需要这样做。 此类依赖项可能出现在两种方法：

-   子设备可能会共享某些卡上的资源。 例如，如果子设备共享数字信号处理器 (DSP)，总线驱动程序可能需要下载专有操作系统之前启动第一个子 DSP 上运行。

-   存在设计缺陷可能会导致在子设备之间的依赖项。 例如，存在设计缺陷可能会要求子设备以按特定顺序电源向上或向下。

任一类型的依赖关系存在时，专有总线驱动程序几乎始终是更好的解决方案比子设备直接向插管理器和尝试隐藏依赖项。

如果提供的适配器卡总线驱动程序，应确保总线驱动程序分配的设备 Id 在系统中是唯一。

总线驱动程序提供了它的一个子级响应设备 ID [ **IRP\_MN\_查询\_ID** ](https://msdn.microsoft.com/library/windows/hardware/ff551679)插管理器中的查询。 可以在其发送给响应中指示总线驱动程序的两种方式之一中指定的 ID [ **IRP\_MN\_查询\_功能**](https://msdn.microsoft.com/library/windows/hardware/ff551664)通过设置查询[**设备\_功能**](https://msdn.microsoft.com/library/windows/hardware/ff543095)结构的**UniqueID**字段**TRUE**或**FALSE**:

-   **UniqueID** = **TRUE**

    这意味着，保证的子级的名称是唯一的在整个系统。 设备 ID 字符串包含设备 ID 以及实例 ID，这是唯一标识硬件实例的序列号。

-   **UniqueID** = **FALSE**

    这意味着唯一仅方面父级的子级的名称。 大多数设备都使用这种标识。 在这种情况下，插 manager 扩展了它接收以使整个系统唯一设备 ID 字符串。 扩展的字符串是一个函数的父设备的唯一 id。

所有音频总线驱动程序应设置**UniqueID** = **FALSE**孩子。 这会导致要通过添加信息以使该 ID 在计算机上唯一的设备的父扩展孩子的设备 ID 字符串的插管理器。

 

 




