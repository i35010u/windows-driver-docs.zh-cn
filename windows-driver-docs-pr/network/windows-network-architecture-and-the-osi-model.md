---
title: Windows 网络体系结构和 OSI 模型
description: Windows 网络体系结构和 OSI 模型
ms.assetid: d57cadc7-c443-441d-b693-d85ffabe9f7f
keywords:
- OSI 参考模型 WDK 网络
- 传输层 WDK 网络
- 数据链路层 WDK 网络
- MAC 层 WDK 网络
- 物理层 WDK 网络
- Windows 网络体系结构 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dc437e15f2df7a4f5b1b2837c63467055aee6812
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844388"
---
# <a name="windows-network-architecture-and-the-osi-model"></a>Windows 网络体系结构和 OSI 模型


## 叙述<a href="" id="ddk-windows-network-architecture-and-the-osi-model-ng"></a>


Microsoft Windows 操作系统使用基于国际标准化组织（ISO）开发的七层网络模型的网络体系结构。 ISO 开放式系统互连（OSI）参考模型在1978中引入，它将网络描述为 "一系列协议层，其中包含分配给每个层的一组特定函数。 每一层都向更高层提供特定服务，同时从服务的实现方式的详细信息中屏蔽这些层。 每对相邻层之间的一个明确定义的接口定义由下层提供的服务和这些服务的访问方式。 下图说明了 OSI 参考模型。

![说明 osi 引用模型的关系图](images/101osi.png)

Microsoft Windows 网络驱动程序实现了 OSI 参考模型的底部四层：

## <a name="physical-layer"></a>物理层  
物理层是 OSI 模型的最低层。 此层管理非结构化原始位流在物理介质上的接收和传输。 它介绍了物理介质的电气/光纤、机械和功能接口。 物理层携带所有更高层的信号。 在 Windows 中，物理层由网络接口卡（NIC）、其收发器和 NIC 连接到的介质来实现。

## <a name="data-link-layer"></a>数据链接层  
数据链路层进一步除以电气和电子工程师协会（IEEE）到两个子层：逻辑链接控制（LLC）和媒体访问控制（MAC）。

### <a name="llc"></a>LLC

LLC 子层提供了从一个节点到另一个节点的无错误传输数据帧。 LLC 子层建立和终止逻辑链接、控制帧流、序列帧、确认帧以及重新传输未确认的帧。 LLC 子层使用帧确认和重新传输来提供通过指向上述层的链接的几乎无错误传输。

### <a name="mac"></a>MAC

MAC 子层管理对物理层的访问，检查帧错误，并管理接收到的帧的地址识别。

在 Windows 网络体系结构中，LLC 子层在传输驱动程序中实现，MAC 子层在 NIC 中实现。 NIC 由称为[微型端口驱动程序](ndis-miniport-drivers2.md)的软件设备驱动程序控制。 Windows 支持多种小型端口驱动程序的多种形式，包括 WDM 微型端口驱动程序、微型端口呼叫管理器（MCMs）和微型端口[中间驱动程序](ndis-miniport-drivers.md)。

## <a name="network-layer"></a>网络层
网络层控制子网的操作。 此层根据以下内容确定数据应采用的物理路径：

-   网络条件。

-   服务的优先级。

-   其他因素，如路由、流量控制、帧分段和重组、逻辑到物理地址映射和使用情况记帐。

## <a name="transport-layer"></a>传输层

传输层可确保消息按顺序无错误地传递，且不会丢失或重复。 此层从任何问题中免除了更高层的协议，因为在这些协议与其对等之间传输数据。 协议堆栈中需要最小传输层，其中包含提供虚拟线路功能的可靠网络或 LLC 子层。 例如，由于适用于 Windows 的 NetBEUI 传输驱动程序与 OSI 兼容的 LLC 子层，其传输层函数最小。 如果协议堆栈不包含 LLC 子层，并且网络层不可靠并且/或支持数据报（与 TCP/IP 的 IP 层或 NWLink 的 IPX 层相同），则传输层应包括帧序列化和确认，以及重新传输未确认的帧。

在 Windows 网络体系结构中，LLC、网络和传输层由称为[协议驱动](ndis-protocol-drivers.md)程序的软件驱动程序实现，这有时称为*传输驱动程序*。

 

 





