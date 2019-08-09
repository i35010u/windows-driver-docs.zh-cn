---
title: Windows 7 中的 IEEE 1394 总线驱动程序
description: Windows 7 包括 1394ohci.sys，新的 IEEE 1394 总线驱动程序支持更快的速度和备选媒体 IEEE 1394b 规范中定义。
ms.assetid: 3744C1D5-E411-4E47-9154-40E15626250D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e0be9334833e1f4b8644e5b67a15c135c30eed56
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385776"
---
# <a name="ieee-1394-bus-driver-in-windows-7"></a>Windows 7 中的 IEEE 1394 总线驱动程序

Windows 7 包括 1394ohci.sys，新的 IEEE 1394 总线驱动程序支持更快的速度和备选媒体 IEEE 1394b 规范中定义。 1394ohci.sys 总线驱动程序是一个单一 （整体式） 的设备驱动程序，通过使用内核模式驱动程序框架 (KMDF) 实现。 旧的 1394年总线驱动程序 （在早期版本的 Windows 中可用） 包括端口/微型端口配置中使用 Windows 驱动程序模型 (WDM) 实现的多个设备驱动程序。 1394ohci.sys 总线驱动程序将替换旧端口驱动程序、 1394bus.sys，主要的微型端口驱动程序、 ochi1394.sys。

新 1394ohci.sys 总线驱动程序是使用旧式总线驱动程序完全向后的兼容。 本主题介绍了一些新的和旧的 1394年总线驱动程序之间的已知行为差异。

> [!NOTE]
> 1394ohci.sys 驱动程序是在 Windows 中包含的系统驱动程序。 在安装 1394年控制器时，它会自动加载。 这不是一个可再发行组件的驱动程序，则可以单独下载。

* [I/O 请求完成](#io-request-completion)
* [配置 ROM 检索](#configuration-rom-retrieval)
* [IEEE 1394 1995 PHY 支持](#ieee-1394-1995-phy-support)
* [节点\_设备\_扩展结构用法](#node_device_extension-structure-usage)
* [间隙计数优化](#gap-count-optimization)
* [设备驱动程序接口 (DDI) 更改](#device-driver-interface-ddi-changes)
* [相关主题](#related-topics)

## <a name="io-request-completion"></a>I/O 请求完成

发送到新的 1394年总线驱动程序的所有 I/O 请求都返回状态\_PENDING 由于 1394ohci.sys 总线驱动程序实现而不是 WDM 使用 KMDF。 此行为不同于旧的 1394年总线驱动程序，在特定的 I/O 请求立即完成。

客户端驱动程序必须等待，直到 I/O 请求发送到新的 1394年总线驱动程序都已完成。 您可以在请求完成后调用的 I/O 完成例程。 已完成的 I/O 请求的状态处于 IRP。

## <a name="configuration-rom-retrieval"></a>配置 ROM 检索

新的 1394年总线驱动程序将尝试使用异步块事务总线速度更快地检索内容节点的配置 rom。 旧的 1394年总线驱动程序使用异步 quadlet 读取 S100 速度 — 或 100 兆位 / 秒 (Mbps)。 1394ohci.sys 总线驱动程序还在使用中指定值**代**和**max\_rom**的节点的配置 ROM 标头以提高检索的剩余条目配置 rom。 内容 有关新的 1394年总线驱动程序如何检索节点的配置 ROM 中的内容的详细信息，请参阅[检索的 IEEE 1394 节点的配置 ROM 内容](https://docs.microsoft.com/windows-hardware/drivers/ieee/retrieving-the-contents-of-a-ieee-1394-node-s-configuration-rom)。

## <a name="ieee-1394-1995-phy-support"></a>IEEE 1394 1995 PHY 支持

1394ohci.sys 总线驱动程序需要支持 IEEE 1394a 或 IEEE 1394b 物理层 （物理）。 它不支持支持 IEEE 1394 1995年 PHY。 这是由于短 （仲裁） 总线重置 1394ohci.sys 总线驱动程序的独占使用。

## <a name="node_device_extension-structure-usage"></a>节点\_设备\_扩展结构用法

客户端驱动程序可以引用客户端驱动程序控制的设备与物理设备对象 (PDO) 相关联的 1394年总线驱动程序中的设备扩展。 描述此设备扩展**节点\_设备\_扩展**结构。 在 1394ohci.sys，此结构保持在相同的位置，如下所示的旧的 1394年总线驱动程序，但非静态成员的结构可能不是有效。 当客户端驱动程序使用新的 1394年总线驱动程序时，它们必须确保在访问数据**节点\_设备\_扩展**有效。 静态成员**节点\_设备\_扩展**包含有效的数据是**标记**， **DeviceObject**，和**PortDeviceObject**。 所有其他成员**节点\_设备\_扩展**是非静态，客户端驱动程序不能引用。

## <a name="gap-count-optimization"></a>间隙计数优化

1394ohci.sys 总线驱动程序的默认行为是仅 IEEE 1394a 设备找到 1394年总线，不包括本地节点上时优化间隔计数。 例如，如果运行 1394ohci.sys 系统有符合 IEEE 1394b 的主控制器，但在总线上的所有设备都符合 IEEE 1394a，然后尝试为新的 1394年总线驱动程序优化的间隔计数。

仅当 1394ohci.sys 总线驱动程序确定本地节点是总线管理器，会出现间隙计数优化。

1394ohci.sys 总线驱动程序确定设备是否符合 IEEE 1394a 中节点的自助 id 数据包的速度设置。 如果速度 (sp) 中的节点集两个位自助 id 数据包，然后 1394ohci.sys 中的字段会认为节点符合 IEEE 1394b。 如果速度字段包含任何其他值，1394ohci.sys 会认为节点符合 IEEE 1394a。 使用的间隔计数值基于表 E-1 在 IEEE 1394a 规范中，为跃点的函数提供的间隔计数。 1394ohci.sys 总线驱动程序不会计算间隔计数。 可以使用注册表值来更改默认间隙计数行为。 有关详细信息，请参阅[修改 IEEE 1394 总线驱动程序的默认行为](https://docs.microsoft.com/windows-hardware/drivers/ieee/modifying-the-default-behavior-of-the-ieee-1394-bus-driver)。

## <a name="device-driver-interface-ddi-changes"></a>设备驱动程序接口 (DDI) 更改

在 Windows 7 中，1394 DDIs 都已更改为支持 1394b 规范规定并改进了简化的 1394年客户端驱动程序开发更快的速度。 有关新的 1394年总线驱动程序支持的常规 DDI 更改的详细信息，请参阅[在 Windows 7 中的设备驱动程序接口 (DDI) 更改](https://docs.microsoft.com/windows-hardware/drivers/ieee/device-driver-interface--ddi--changes-in-windows-7)。

## <a name="related-topics"></a>相关主题

[IEEE 1394 驱动程序堆栈](https://docs.microsoft.com/windows-hardware/drivers/ieee/the-ieee-1394-driver-stack)  
[检索 IEEE 1394 节点的配置 ROM 的内容](https://docs.microsoft.com/windows-hardware/drivers/ieee/retrieving-the-contents-of-a-ieee-1394-node-s-configuration-rom)  
