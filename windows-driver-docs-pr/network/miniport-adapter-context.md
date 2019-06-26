---
title: 微型端口适配器上下文
description: 微型端口适配器上下文
ms.assetid: cb43d02d-cf52-46a4-b56d-aa3afcbd0ca5
keywords:
- 逻辑适配器 WDK 网络
- 上下文 WDK 微型端口适配器
- 微型端口适配器 WDK 网络、 上下文
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5b57eba4ae33598eeba55abcdba0821fd82dceee
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373975"
---
# <a name="miniport-adapter-context"></a>微型端口适配器上下文





NDIS 使用软件对象调用*微型端口适配器*来表示系统中的每个虚拟或物理网络设备。 此对象维护的 NDIS 和是不透明的微型端口驱动程序和协议驱动程序。 NDIS 将句柄传递给此微型端口驱动程序的结构[ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)函数。 微型端口驱动程序随后提供中所有调用的此句柄**Ndis * Xxx*** 与句柄指定的微型端口适配器相关的函数。

微型端口驱动程序调用以初始化它所管理的微型端口适配器，它会创建其自己的内部数据结构来表示微型端口适配器。 驱动程序将使用此结构，称为*微型端口适配器上下文*、 维护驱动程序管理的微型端口适配器所需的特定于设备的状态信息。 该驱动程序将一个句柄传递给到 NDIS 此结构。 有关指定的微型端口适配器上下文的详细信息，请参阅[初始化适配器](initializing-a-miniport-adapter.md)。

当 NDIS 调用微型端口驱动程序之一*MiniportXxx*微型端口适配器，NDIS 与相关的函数传递要标识正确的微型端口适配器添加到驱动程序的微型端口适配器上下文。 拥有和维护的微型端口驱动程序微型端口适配器上下文表示到 NDIS 和协议驱动程序不透明。

 

 





