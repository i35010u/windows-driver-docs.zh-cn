---
title: 地址系列
description: 地址系列
keywords:
- 面向连接的 NDIS WDK，地址系列
- CoNDIS WDK 网络，地址系列
- 地址系列 WDK 网络
- AFs WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3283b32abe49f73b06566bf02c9fbe1551cdc9c5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96833419"
---
# <a name="address-families"></a>地址系列





*地址系列* (AF) 表示以下一组驱动程序之间的关联：

-   面向连接的客户端、呼叫管理器和面向连接的基础微型端口驱动程序。

-   面向连接的客户端和特定信号协议的 MCM 驱动程序。

地址族还指定特定的信号协议。

调用管理器或 MCM 驱动程序通过将地址族注册到 NDIS，为特定的信号协议公布其呼叫管理器服务。 然后，NDIS 通知每个客户端绑定新注册的地址族。 在使用呼叫管理器或 MCM 驱动程序提供的呼叫管理器服务之前，面向连接的客户端必须使用调用管理器或 MCM 驱动程序打开该地址族。

有关地址系列上的操作的详细信息，请参阅 [注册和打开地址族](registering-and-opening-an-address-family.md) 并 [关闭地址族](closing-an-address-family.md)。

 

 





