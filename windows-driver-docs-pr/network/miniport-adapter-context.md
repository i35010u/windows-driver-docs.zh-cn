---
title: 微型端口适配器上下文
description: 微型端口适配器上下文
ms.assetid: cb43d02d-cf52-46a4-b56d-aa3afcbd0ca5
keywords:
- 逻辑适配器 WDK 网络
- 上下文 WDK 微型端口适配器
- 微型端口适配器 WDK 网络，上下文
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 704f2e08434f274f53f609f4f44fbbbe40f700bb
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844260"
---
# <a name="miniport-adapter-context"></a>微型端口适配器上下文





NDIS 使用称为*微型端口适配器*的软件对象来表示系统中的每个虚拟或物理网络设备。 此对象由 NDIS 维护，对于微型端口驱动程序和协议驱动程序是不透明的。 NDIS 将此结构的句柄传递给微型端口驱动程序的[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)函数。 然后，微型端口驱动程序会在所有对**Ndis * Xxx*** 函数的调用中提供该句柄，该句柄与句柄指定的微型端口适配器相关。

当调用微型端口驱动程序来初始化它所管理的微型端口适配器时，它会创建自己的内部数据结构来表示微型端口适配器。 驱动程序使用此结构（称为*微型端口适配器上下文*）来维护设备特定的状态信息，驱动程序需要此信息来管理微型端口适配器。 驱动程序将此结构的句柄传递到 NDIS。 有关指定微型端口适配器上下文的详细信息，请参阅[初始化适配器](initializing-a-miniport-adapter.md)。

当 NDIS 调用微型端口驱动程序的*MiniportXxx*函数之一时，ndis 会将微型端口适配器上下文传递给驱动程序，以确定正确的微型端口适配器。 微型端口适配器上下文由微型端口驱动程序拥有和维护，并且对于 NDIS 和协议驱动程序是不透明的。

 

 





