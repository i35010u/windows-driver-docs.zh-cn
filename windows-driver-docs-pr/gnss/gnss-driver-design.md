---
title: 全局导航卫星系统（GNSS）驱动程序设计
description: 讨论开发适用于 Windows 10 的全局导航卫星系统（GNSS）驱动程序时要考虑的设计原则，其中包括数据结构、错误报告和驱动程序版本控制。
ms.assetid: E10B1149-CC8B-438D-B537-258F7FCFA0E7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ff6b1c2757f8920313c260a3be070b0fac316899
ms.sourcegitcommit: 96f94bffe426b7f92913fa0ffff1918c76e0e52c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/04/2020
ms.locfileid: "76980678"
---
# <a name="global-navigation-satellite-system-gnss-driver-design"></a>全局导航卫星系统（GNSS）驱动程序设计

讨论开发适用于 Windows 10 的全局导航卫星系统（GNSS）驱动程序时要考虑的设计原则，其中包括数据结构、错误报告和驱动程序版本控制。

## <a name="data-structures"></a>数据结构

为了实现向后兼容性和将来的扩展性，所有数据结构都以版本号和大小开始，以适应将来的扩展和向后兼容性问题。 作为附加的安全措施，每个结构还具有一个填充缓冲区，以便即使在添加新字段时，静态结构大小仍保持不变。 这是为了使用结构的静态编译时大小（使用**sizeof**）而不是结构的动态大小，来防止任何较旧的 GNSS 驱动程序出现错误。

除非另外指定，否则所有参数都将遵循国际系统（SI）：

| 参数 | 计算 |
| --- | --- |
| 距离、阈值或级别 | 进度表 |
| 超时或间隔 | 数 |
| 速度 | 计量/秒 |

## <a name="error-reporting"></a>错误报告

全局导航卫星系统（GNSS） DDI 需要将**NTSTATUS**作为驱动程序的返回值。 高级操作系统（HLOS）基于这些错误消息仅对成功和失败情况进行操作，并且不会查看特定错误消息。 但最好是驱动程序返回的错误与相应的**NTSTATUS**错误消息紧密映射。 GNSS 驱动程序可以发送其自己的自定义**NTSTATUS**错误消息，这些错误消息对于诊断目的可能很有用。

## <a name="driver-versioning"></a>驱动程序版本控制

为全局导航卫星系统（GNSS） DDI 指定的每个结构都包含 "驱动程序版本" 字段，许多结构包含一个填充字段。 这两个组件都用于使用以下策略来缓解新版本的 GNSS DDI：

- 框架和驱动程序使用功能交换过程来传达各自的版本。 这些 IOCTLs 被认为是特别的，因为它们使用版本字段来传达其版本。 因此，涉及设备和平台功能检查的实现应显式检查第一次返回的版本，并将其存储起来供以后使用。 [**GNSS\_设备\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/gnssdriver/ns-gnssdriver-gnss_device_capability)结构的版本成员会传达驱动程序的版本号。 [**GNSS\_平台\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/gnssdriver/ns-gnssdriver-gnss_platform_capability)结构的版本成员与 GNSS 适配器的版本号通信。

- 当添加新字段时，如果该结构包含填充字段，则应使用空白填充空间，而不是将其添加到结构中，这将保持二进制兼容性

- 每当添加新字段时，GNSS DDI 的版本将被视为递增。 这会在 GNSS DDI 标头本身的注释中反映出来，但不会公开为常量。 GNSS 适配器和 GNSS 驱动程序都将使用私有常数值来指示其当前版本。 这允许 GNSS 适配器和驱动程序都针对特定版本进行编码。

- GNSS 适配器必须与 GNSS 驱动程序的较旧版本向后兼容。 如果新版本的 DDI 中引入了协议更改，则符合新的 GNSS DDI 的 GNSS 适配器必须仅为新版驱动程序实现新协议，并为旧版本的驱动程序使用旧协议。

- GNSS 驱动程序必须与较新版本的 GNSS 适配器向前兼容，并应以其编码的当前版本相同的方式来处理 GNSS 适配器的新版本。

- 使用较新版本的 GNSS 驱动程序时，GNSS 适配器的较旧版本不应正常工作。 为了促进 GNSS 适配器和 GNSS 驱动程序与新版本 DDI 的共同开发，GNSS 适配器中将不会有任何严格版本检查来阻止新的 GNSS 驱动程序。 但是，针对 DDI 的较新版本而实现的 GNSS 驱动程序将不会发送到零售设备，其中包含针对旧版本 GNSS DDI 实现的 GNSS 适配器。

- GNSS 适配器将不支持任何 Windows 8.1 或较早的 GNSS 传感器驱动程序。 这些驱动程序将通过旧堆栈继续在 Windows 10 中运行。 如果存在另一个 Windows 10 GNSS 驱动程序，则不确定旧的 GNSS 传感器驱动程序的使用情况。
