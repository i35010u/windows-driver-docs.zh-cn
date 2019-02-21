---
title: MCM 驱动程序 vs。调用管理器
description: MCM 驱动程序 vs。
ms.assetid: 374716fb-c192-42fd-bef0-0097d622f791
keywords:
- 面向连接的 NDIS WDK，调用管理器
- CoNDIS WDK 网络、 调用管理器
- 面向连接的 NDIS WDK，MCM 驱动程序
- CoNDIS WDK 网络、 MCM 驱动程序
- MCM 驱动程序 WDK 网络
- 调用管理器 WDK 网络、 vs。MCM 驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b88cb3a89aa64c58e67d4ef18ca2f8086a678ded
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524184"
---
# <a name="mcm-drivers-vs-call-managers"></a>MCM 驱动程序 vs。调用管理器





集成的 MCM 驱动程序是一个面向连接的微型端口驱动程序，还向面向连接的客户端提供调用管理器服务。 在这种情况下，MCM 驱动程序执行的所有面向连接的功能的面向连接的微型端口驱动程序和呼叫管理器。 MCM 驱动程序必须使用所有微型端口驱动程序，如**Ndis * Xxx*** 调用与基础 NIC 硬件进行通信。

MCM 驱动程序不同于呼叫管理器两种主要方法：

-   呼叫管理器是面向连接的 NDIS*协议驱动程序*添加调用管理器功能。 MCM 驱动程序是面向连接的 NDIS*微型端口驱动程序*添加调用管理器功能。

-   呼叫管理器和一个面向连接的微型端口驱动程序之间的接口完全公开到 NDIS-即，呼叫管理器和微型端口驱动程序之间的所有通信通过 NDIS 都传送。 除外的激活和停用的客户端 VCs (VCs 用于将传出或传入客户端数据传输)，是不透明的 NDIS MCM 驱动程序的调用管理器部分与 MCM 驱动程序的微型端口驱动程序部分之间的接口。 因为 NDIS 跟踪的客户端 VCs，必须通过 NDIS 中实现的激活和停用的客户端 VCs。

以下各节中将进一步描述 MCM 驱动程序和呼叫管理器之间的差异：

[初始化之间的差异](differences-in-initialization.md)

[对 NdisXxx 函数的调用之间的差异](differences-in-calls-to-ndisxxx-functions.md)

[虚拟连接之间的差异](differences-in-virtual-connections.md)

 

 





