---
title: Windows 网络体系结构和 OSI 模型
description: Windows 网络体系结构和 OSI 模型
ms.assetid: d57cadc7-c443-441d-b693-d85ffabe9f7f
keywords:
- OSI 引用模型 WDK 网络
- 传输层 WDK 网络
- 数据链接层 WDK 网络
- MAC 层 WDK 网络
- 物理层 WDK 网络
- Windows 网络体系结构 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e5da7810ac500c4458e9eb55344fa3270ceacd63
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335352"
---
# <a name="windows-network-architecture-and-the-osi-model"></a>Windows 网络体系结构和 OSI 模型


## 概述 <a href="" id="ddk-windows-network-architecture-and-the-osi-model-ng"></a>


Microsoft Windows 操作系统使用基于七层网络模型开发由国际标准化组织 (ISO) 的网络体系结构。 在 1978 年引进的 ISO 开放系统互连 (OSI) 引用模型描述网络为"一系列的协议层使用一组特定的函数分配给每个层。 每一层防护如何实现服务的详细信息从这些层同时提供了到较高的层的特定服务。 每对相邻的图层之间妥善定义的接口定义到更高版本的一个，如何访问这些服务的较低层提供的服务。" 下图说明了 OSI 参考模型。

![说明在 osi 引用模型的关系图](images/101osi.png)

Microsoft Windows 网络驱动程序实现 OSI 引用模型的底部四个层：

## <a name="physical-layer"></a>物理层  
物理层是 OSI 模型的最低层。 此层通过物理媒体管理接收和传输非结构化的原始位流。 它描述了物理介质的电气/光盘、 机械和功能接口。 物理层会带来较高的层的所有信号。 在 Windows 中，物理层实现通过网络接口卡 (NIC)、 其收发器和 NIC 附加到该介质。

## <a name="data-link-layer"></a>数据链路层  
数据链路层又进一步分为电气和电子工程师协会 (IEEE) 由两个子层： 逻辑链接控件 (LLC) 和媒体访问控制 (MAC)。

### <a name="llc"></a>LLC

LLC 子层提供了无错误的传输的数据帧从一个节点到另一个。 LLC 子层建立和终止逻辑链接、 控制帧流、 序列帧、 确认帧，和一段重新传输未确认的帧。 LLC 子层使用帧确认并重新传输通过上面的层的链接提供几乎无错误的传输。

### <a name="mac"></a>MAC

MAC 子层管理物理层访问检查帧错误，并管理接收到的帧的地址识别。

在 Windows 网络体系结构，LLC 子层实现在传输驱动程序，并在 NIC 中实现 MAC 子层 软件设备驱动程序调用由控制 NIC[微型端口驱动程序](ndis-miniport-drivers2.md)。 Windows 支持的微型端口驱动程序包括 WDM 微型端口驱动程序、 微型端口调用管理器 (MCMs) 和微型端口的多个变体[驱动程序的中间](ndis-miniport-drivers.md)。

## <a name="network-layer"></a>网络层
网络层控制的子网的操作。 此层将确定数据，应执行，基于以下的物理路径：

-   网络条件。

-   服务的优先级。

-   其他因素，如路由、 流量控制、 帧碎片和重组，逻辑到物理地址映射，以及使用记帐。

## <a name="transport-layer"></a>传输层

传输层可确保消息传送无错误的顺序和不带任何丢失或重复。 此层不从它们和其对等方之间传输数据的任何问题的更高层的协议。 最小传输层协议堆栈，包括可靠的网络或提供了虚拟线路功能的 LLC 子层中需要。 例如，因为 NetBEUI 传输驱动程序为 Windows OSI 符合 LLC 子层，其传输层函数是最小。 如果协议堆栈不包括 LLC 子层，并且网络层是不可靠和/或支持数据报 （与 TCP/IP IP 层或 NWLink 的 IPX 层）、 传输层应包括帧序列化和确认，以及未确认的帧的重新传输。

在 Windows 网络体系结构、 LLC、 网络和传输层实现的软件驱动程序称为[协议驱动程序](ndis-protocol-drivers.md)，这有时称为*传输驱动程序*。

 

 





