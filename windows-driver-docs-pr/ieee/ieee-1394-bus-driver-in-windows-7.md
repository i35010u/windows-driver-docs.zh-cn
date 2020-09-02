---
title: Windows 7 中的 IEEE 1394 总线驱动程序
description: Windows 7 包括 1394ohci.sys，这是一种新的 IEEE 1394 总线驱动程序，它支持以 IEEE-1394b 规范中定义的速度更快、更备用的媒体。
ms.assetid: 3744C1D5-E411-4E47-9154-40E15626250D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 158507c488b4319d317d7932fe8d8801109b7c1f
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89382231"
---
# <a name="ieee-1394-bus-driver-in-windows-7"></a>Windows 7 中的 IEEE 1394 总线驱动程序

Windows 7 包括 1394ohci.sys，这是一种新的 IEEE 1394 总线驱动程序，它支持以 IEEE-1394b 规范中定义的速度更快、更备用的媒体。 1394ohci.sys 总线驱动程序是单个 (单一) 设备驱动程序，通过使用内核模式驱动程序框架 (KMDF) 实现。 旧版1394总线驱动程序 (适用于 Windows 的早期版本) 包含多个设备驱动程序，这些驱动程序是使用 Windows 驱动模型 (WDM) 在端口/微型端口配置中实现的。 1394ohci.sys 总线驱动程序会替换旧的端口驱动程序、1394bus.sys 和主要微型端口驱动程序，ochi1394.sys。

新的 1394ohci.sys 总线驱动程序完全向后兼容旧的总线驱动程序。 本主题介绍新的和旧的1394总线驱动程序之间的一些已知行为差异。

> [!NOTE]
> 1394ohci.sys 驱动程序是 Windows 中包含的系统驱动程序。 当你安装1394控制器时，它会自动加载。 这不是可再发行的驱动程序，可单独下载。

* [I/o 请求完成](#io-request-completion)
* [配置 ROM 检索](#configuration-rom-retrieval)
* [IEEE-1394-1995 PHY 支持](#ieee-1394-1995-phy-support)
* [节点 \_ 设备 \_ 扩展结构使用情况](#node_device_extension-structure-usage)
* [差距计数优化](#gap-count-optimization)
* [设备驱动程序接口 (DDI) 更改](#device-driver-interface-ddi-changes)
* [相关主题](#related-topics)

## <a name="io-request-completion"></a>I/o 请求完成

发送到新1394总线驱动程序的所有 i/o 请求都将返回状态 \_ "挂起"，因为 1394ohci.sys 总线驱动程序是通过使用 KMDF 而不是使用 WDM 实现的。 此行为不同于旧1394总线驱动程序的行为，在这种情况下，某些 i/o 请求会立即完成。

客户端驱动程序必须等待，直到发送到新1394总线驱动程序的 i/o 请求已完成。 你可以提供一个在请求完成后调用的 i/o 完成例程。 已完成的 i/o 请求的状态位于 IRP 中。

## <a name="configuration-rom-retrieval"></a>配置 ROM 检索

新的1394总线驱动程序尝试使用更快的总线速度来检索节点配置 ROM 的内容。 旧1394总线驱动程序使用异步 quadlet 读取速度为 S100 速度，即每秒100兆位 (Mbps) 。 1394ohci.sys 总线驱动程序还使用节点配置 ROM 标头的 " **生成** " 和 " **最大 \_ rom** " 条目中指定的值来改善配置 rom 的其余内容的检索。 有关新1394总线驱动程序如何检索节点配置 ROM 内容的详细信息，请参阅 [检索 IEEE 1394 节点的配置 rom 的内容](./retrieving-the-contents-of-a-ieee-1394-node-s-configuration-rom.md)。

## <a name="ieee-1394-1995-phy-support"></a>IEEE-1394-1995 PHY 支持

1394ohci.sys 总线驱动程序需要支持 IEEE-1394a 或 IEEE-1394b 的物理层 (PHY) 。 它不支持支持 IEEE-1394-1995 的 PHY。 此要求的原因是 1394ohci.sys 总线驱动程序独占使用较短的 (仲裁) 总线重置。

## <a name="node_device_extension-structure-usage"></a>节点 \_ 设备 \_ 扩展结构使用情况

客户端驱动程序可以引用与客户端驱动程序所控制设备 (PDO) 相关联的1394总线驱动程序中的设备扩展。 此设备扩展由 **节点 \_ 设备 \_ 扩展** 结构描述。 在 1394ohci.sys 中，此结构保持在与旧版1394总线驱动程序相同的位置，但结构的非静态成员可能无效。 当客户端驱动程序使用新的1394总线驱动程序时，必须确保 **节点 \_ 设备 \_ 扩展** 中的访问数据有效。 包含有效数据的 **节点 \_ 设备 \_ 扩展** 的静态成员为 **Tag**、 **DeviceObject**和 **PortDeviceObject**。 所有其他成员 **节点 \_ 设备 \_ 扩展** 都是非静态的，客户端驱动程序不得引用此扩展。

## <a name="gap-count-optimization"></a>差距计数优化

1394ohci.sys 总线驱动程序的默认行为是在1394总线上仅找到 IEEE 1394a 设备（不包括本地节点）时优化间隙计数。 例如，如果运行 1394ohci.sys 的系统的主机控制器符合 IEEE 1394b，但总线上的所有设备都符合 IEEE 1394a，则新的1394总线驱动程序会尝试优化间隙计数。

仅当 1394ohci.sys 总线驱动程序确定本地节点为总线管理器时，才会进行间隙计数优化。

1394ohci.sys 总线驱动程序使用节点的自 id 数据包中的速度设置来确定设备是否符合 IEEE-1394a。 如果某个节点在自 id 数据包的速度 (sp) 字段中设置了这两个位，则 1394ohci.sys 会将节点视为符合1394b。 如果 "速度" 字段包含任何其他值，则 1394ohci.sys 会将节点视为符合 IEEE-1394a。 使用的 "间隙计数" 值基于 IEEE-1394a 规范中的表 E-1，它提供了一个跃点的功能。 1394ohci.sys 总线驱动程序不计算差距计数。 您可以通过使用注册表值来更改默认的间隙计数行为。 有关详细信息，请参阅 [修改 IEEE 1394 总线驱动程序的默认行为](./modifying-the-default-behavior-of-the-ieee-1394-bus-driver.md)。

## <a name="device-driver-interface-ddi-changes"></a>设备驱动程序接口 (DDI) 更改

在 Windows 7 中，1394 DDIs 已更改为支持1394b 规范定义的更快的速度，并经过改进，简化了1394客户端驱动程序的开发。 有关新的1394总线驱动程序支持的常规 DDI 更改的详细信息，请参阅 [Windows 7 中的设备驱动程序界面 (DDI) 更改](./device-driver-interface--ddi--changes-in-windows-7.md)。

## <a name="related-topics"></a>相关主题

[IEEE 1394 驱动程序堆栈](./the-ieee-1394-driver-stack.md)  
[检索 IEEE 1394 节点的配置 ROM 的内容](./retrieving-the-contents-of-a-ieee-1394-node-s-configuration-rom.md)