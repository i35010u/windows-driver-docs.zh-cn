---
title: NDIS 端口概述
description: NDIS 端口概述
keywords:
- 端口 WDK NDIS，关于 NDIS 端口
- NDIS 端口 WDK，关于 NDIS 端口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0b0c2e3aa46bb4531ba35d301fe8174a27558f55
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96801359"
---
# <a name="overview-of-ndis-ports"></a>NDIS 端口概述





本部分介绍 NDIS 端口，这是一个 NDIS 6.0 功能，可用于访问 subinterfaces。 在 NDIS 中，网络接口与微型端口适配器相关联，而微型端口适配器的 subinterfaces 称为 *NDIS 端口*。

由于每个网络接口都被视为微型端口适配器，因此驱动程序堆栈的体系结构更简单。 例如，每个微型端口适配器都有其自己的 IP 和 MAC 地址。 在大多数情况下，过量驱动程序不需要有关微型端口适配器的虚拟或物理特性的信息，或者有关驱动程序堆栈底部的物理设备的信息。

NDIS 微型端口适配器可以为物理设备或虚拟设备提供接口。 NDIS 中间驱动程序为称为 *虚拟微型端口* 的虚拟设备提供接口。 NDIS 中间驱动程序可以绑定到基础微型端口适配器，并公开过量协议驱动程序绑定到的虚拟微型端口。

在许多情况下，基础物理设备与 virtual 微型端口之间没有一对一关系。 例如，实现故障转移功能的中间驱动程序可以创建一个虚拟小型端口来支持多个物理设备，而虚拟 LAN (VLAN) 中间驱动程序可以创建多个与单个物理设备关联的虚拟微型端口。 同时，同时结合故障转移和 VLAN 功能的驱动程序可以创建一组虚拟微型端口 (*N* 个 vlan) ，同时驱动程序绑定到多个物理设备 (*M* 个物理设备) 。 有关中间驱动程序和虚拟微型端口的详细信息，请参阅 [NDIS 6.0 中间驱动程序](writing-ndis-intermediate-drivers.md)。

在某些应用程序中，能够处理低于 virtual 微型端口的 subinterfaces 是必需的，也可以简化设计。 例如， (EAP) 协议的可扩展身份验证协议必须指定在其上发送或接收 EAP 数据包的物理设备。 如果有多个物理设备与单个虚拟设备相关联，则 EAP 协议将绑定到该虚拟设备。 在这种情况下，NDIS 6.0 之前的 NDIS 接口隐藏 subinterfaces，EAP 协议不能选择应携带 EAP 数据包的底层物理设备。 然后，EAP 协议不会有任何访问基础物理微型端口适配器的权限。 将基础物理微型端口适配器作为 NDIS 端口公开后，EAP 协议允许 EAP 协议面向特定的物理设备。

以下主题进一步描述了 NDIS 端口：

[标识 NDIS 端口](identifying-an-ndis-port.md)

[默认 NDIS 端口](default-ndis-port.md)

[NDIS 端口的类型](types-of-ndis-ports.md)

[NDIS 端口状态](ndis-port-states.md)

 

 





