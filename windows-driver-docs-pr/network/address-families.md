---
title: 地址系列
description: 地址系列
ms.assetid: d40df44e-f88b-4181-84ab-3fbf37172aaf
keywords:
- 面向连接的 NDIS WDK，地址系列
- CoNDIS WDK 网络、 地址系列
- 地址系列 WDK 网络
- AFs WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c3e1360239b5d10ac36e01e8b069ff713cdc36a6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555403"
---
# <a name="address-families"></a>地址系列





*地址系列*(AF) 表示一个下列驱动程序集之间的关联：

-   面向连接的客户端、 调用 manager 和基础面向连接的微型端口驱动程序。

-   面向连接的客户端和 MCM 驱动程序特定的信号协议。

地址系列还指定了特定的信号协议。

呼叫管理器或 MCM 驱动程序通过 NDIS 中注册的地址族播发的特定的信号协议及其调用管理器服务。 NDIS 然后通知每个客户端上的新注册的地址族的绑定。 它可以使用提供的呼叫管理器或 MCM 驱动程序调用管理器服务之前，面向连接的客户端必须使用的呼叫管理器或播发它的 MCM 驱动程序打开的地址族。

有关对地址系列的操作的详细信息，请参阅[注册和打开地址族](registering-and-opening-an-address-family.md)并[关闭地址族](closing-an-address-family.md)。

 

 





