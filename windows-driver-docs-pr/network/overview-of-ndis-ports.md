---
title: NDIS 端口概述
description: NDIS 端口概述
ms.assetid: 324f06c9-d482-4acd-a7a6-050721197c89
keywords:
- 有关 NDIS 端口端口 WDK NDIS
- NDIS 端口 WDK，有关 NDIS 端口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2a2c02d1c518289f3c5a57a8deb94c1c063021e3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63368931"
---
# <a name="overview-of-ndis-ports"></a>NDIS 端口概述





本部分介绍 NDIS 端口，哪些是 NDIS 6.0 功能，它实现了基础网络层来访问子接口。 在 NDIS，网络接口相关联的微型端口适配器，并为子接口的微型端口适配器*NDIS 端口*。

驱动程序堆栈的体系结构是因为每个网络接口都被视为微型端口适配器要简单得多。 例如，每个微型端口适配器具有其自己的 IP 和 MAC 地址。 在大多数情况下，基础驱动程序不需要的微型端口适配器虚拟或物理性质的信息或有关驱动程序堆栈的底部的物理设备的信息。

NDIS 微型端口适配器可以为物理设备或虚拟设备提供的接口。 中间的 NDIS 驱动程序提供了称为的虚拟设备的接口*虚拟微型端口*。 中间的 NDIS 驱动程序可以绑定到基础微型端口适配器或公开基础协议驱动程序将绑定到的虚拟微型端口。

在许多情况下，基础物理设备和虚拟微型端口之间没有一对一关系。 例如，实现故障转移功能的中间驱动程序可以创建一个虚拟的微型端口，以便支持多个物理设备和虚拟 LAN (VLAN) 中间驱动程序可以创建多个与单个相关联的虚拟微型端口物理设备。 此外，结合了故障转移和 VLAN 功能的驱动程序可以创建一组虚拟微型端口 (*N* Vlan 的数字) 时驱动程序绑定到多个物理设备 (*M*物理数设备）。 有关中间驱动程序和虚拟微型端口的详细信息，请参阅[NDIS 6.0 中间驱动程序](writing-ndis-intermediate-drivers.md)。

在某些应用程序，可以用于满足如下虚拟微型端口子接口是必需的或简化设计。 例如，可扩展身份验证协议 (EAP) 协议必须指定 EAP 数据包发送或接收到的物理设备。 如果多个物理设备与单个虚拟设备相关联，EAP 协议绑定到虚拟设备。 在这种情况下，在 NDIS 6.0 之前的 NDIS 接口隐藏子接口，并且 EAP 协议不能选择哪些基础物理设备应执行的 EAP 数据包。 EAP 协议然后没有任何对基础物理微型端口适配器的访问。 公开为 NDIS 端口的基础物理微型端口适配器允许 EAP 协议以面向特定的物理设备。

进一步的以下主题介绍 NDIS 端口：

[标识 NDIS 端口](identifying-an-ndis-port.md)

[默认 NDIS 端口](default-ndis-port.md)

[类型的 NDIS 端口](types-of-ndis-ports.md)

[NDIS 端口状态](ndis-port-states.md)

 

 





