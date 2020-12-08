---
title: AV/C 驱动程序堆栈
description: AV/C 驱动程序堆栈
keywords:
- AV/C WDK，驱动程序堆栈
- 驱动程序堆栈 WDK AV/C
- 堆栈 WDK AV/C
- Avc.sys 函数驱动程序 WDK，驱动程序堆栈
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: caf5f1786fbf67bd3d8bdd8625b5a7f9d16526ba
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96834017"
---
# <a name="avc-driver-stacks"></a>AV/C 驱动程序堆栈





将 AV/C 设备添加到 IEEE 1394 总线并从中删除后，即插即用管理器将加载并卸载相应的子源驱动程序。 供应商通过编写 Windows 加载到 *Avc.sys* 上的 IEEE 1394 堆栈上的子单位驱动程序来实现唯一的 AV/C 子单位功能。 *Avc.sys* 使用基础 IEEE 1394 和 IEC-61883 驱动程序提供的功能来控制设备并连接和管理插头。 有关这些基础驱动程序堆栈的详细信息，请参阅 [IEEE 1394 驱动程序堆栈](../ieee/the-ieee-1394-driver-stack.md) 和 [IEC-61883 客户端驱动程序](../ieee/iec-61883-client-drivers.md)。

对等驱动程序堆栈适用于外部 AV/C 设备上的子单元连接。 与此相反，虚拟驱动程序堆栈是单独的驱动程序堆栈，该堆栈将计算机作为 AV/C 设备公开到在 IEEE 1394 总线上连接的其他 AV/C 设备。 下图演示了两个不同的 *Avc.sys* 堆栈。

![阐释单独的对等节点和虚拟子单位堆栈的关系图](images/avcdiag.gif)

驱动程序堆栈的基础是 *1394ohci.sys* 和 *1394bus.sys*。 这些驱动程序提供基本 IEEE 1394 总线基础结构支持。 对于系统中的每个物理 IEEE 1394 适配器，都有这些驱动程序的实例。

堆积 *1394ohci.sys* 和 *1394bus.sys* *61883.sys*。 IEEE 1394 总线上的每个启用 IEC 61883 的节点都有 *61883.sys* 的实例。 驱动程序的 *61883.sys* 为 IEC 61883 协议提供以下支持：

-   连接管理协议 (CMP) IEC 61883-1

-   常见的同步数据包 (CIP) IEC 61883-1

-   函数控制协议 (FCP) IEC 61883-1

上堆叠 *61883.sys* 是 *Avc.sys* 的，它支持 av/c 协议、每个 av/c 设备上活动子单元连接的即插即用枚举，以及 av/c 子单位的插头连接管理和控制。 有关插入连接和格式管理的详细信息，请参阅 [AV/C 子单位插入连接和格式管理](av-c-subunit-plug-connection-and-format-management.md)。

子单位驱动程序堆积 *Avc.sys*。 这是供应商实现其 AV/C 子位置独有的功能的层。 通常，对于 AV/C 子实体的每个物理实例，都有该子实体的驱动程序的对应实例。 也就是说，每个设备标识符 (ID) 由 *Avc.sys* 的实例表示。 但是， *Avc.sys* 允许基于 AV/C 单元的设备标识符的 ***供应商** _ 和/或 _*_型号_*_ 字段来重写此行为。 有关 _Avc.sys 中生成的设备标识符字符串的 " _*_供应商_*_"、" _*_型号_*_"、" _*_SubunitType_*_" 和 " _*_SubunitID_*_ " 字段的详细信息，请参阅 [AV/C 设备 id](av-c-device-identifiers.md)。

 

