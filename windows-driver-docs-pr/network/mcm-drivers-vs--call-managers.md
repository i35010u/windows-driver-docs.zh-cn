---
title: MCM 驱动程序与呼叫管理程序
description: MCM 驱动程序与
keywords:
- 面向连接的 NDIS WDK，呼叫管理器
- CoNDIS WDK 网络，呼叫管理器
- 面向连接的 NDIS WDK，MCM 驱动程序
- CoNDIS WDK 网络，MCM 驱动程序
- MCM 驱动程序 WDK 网络
- 呼叫管理器 WDK 网络，与 MCM 驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 62cffc3738ac82e20bd6b9d20e800755d0a433f4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96821287"
---
# <a name="mcm-drivers-vs-call-managers"></a>MCM 驱动程序与呼叫管理程序





集成的 MCM 驱动程序是面向连接的微型端口驱动程序，它还向面向连接的客户端提供呼叫管理器服务。 因此，MCM 驱动程序将执行面向连接的微型端口驱动程序和调用管理器的所有面向连接的函数。 与所有微型端口驱动程序一样，MCM 驱动程序必须使用 **Ndis * Xxx*** 调用来与基础 NIC 硬件通信。

MCM 驱动程序在以下两个主要方面不同于呼叫管理器：

-   呼叫管理器是一个 NDIS 连接的 *协议驱动程序* ，其中包含添加的呼叫管理器功能。 MCM 驱动程序是一个基于 NDIS 连接的 *微型端口驱动程序* ，其中添加了调用管理器功能。

-   呼叫管理器与面向连接的微型端口驱动程序之间的接口完全公开给 NDIS，也就是说，呼叫管理器与微型端口驱动程序之间的所有通信都通过 NDIS 传递。 除了激活和停用客户端 VCs (VCs 用于传输传出或传入的客户端数据) ，MCM 驱动程序的调用管理器部分与 MCM 驱动程序的微型端口驱动程序部分之间的接口是不透明的。 必须通过 NDIS 完成客户端 VCs 的激活和停用，因为 NDIS 跟踪客户端 VCs。

以下部分进一步介绍了 MCM 驱动程序与调用管理器之间的差异：

[初始化的差异](differences-in-initialization.md)

[NdisXxx 函数调用的差异](differences-in-calls-to-ndisxxx-functions.md)

[虚拟连接的差异](differences-in-virtual-connections.md)

 

 





