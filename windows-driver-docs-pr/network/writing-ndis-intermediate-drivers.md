---
title: 开始编写 NDIS 中间驱动程序
description: 开始编写 NDIS 中间驱动程序
ms.assetid: c37224b2-8d96-44c2-8b56-884089b9cfcd
keywords:
- 中间驱动程序 WDK 网络
- 网络驱动程序 WDK，中间驱动程序
- NDIS WDK，中间驱动程序
- NDIS 中间驱动程序 WDK
- NDIS 中间驱动程序 WDK，NDIS 6。0
- 中间驱动程序 WDK 网络，NDIS 6。0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2fc4a0b79f9e0718016545adef1926af86fb6eb9
ms.sourcegitcommit: 366a15d68eb58d01a8ca6de7b982f62ac8b7deaf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/19/2020
ms.locfileid: "90811988"
---
# <a name="getting-started-writing-ndis-intermediate-drivers"></a>开始编写 NDIS 中间驱动程序

除非另有说明，否则 NDIS 中间驱动程序提供的服务与微型端口驱动程序和协议驱动程序相同。 中间驱动程序的小型端口边缘提供微型端口驱动程序服务，协议边缘提供协议驱动程序服务。  (有关详细信息，请参阅 [编写 Ndis 微型端口驱动程序](./initializing-a-miniport-driver.md) 和 [编写 Ndis 协议驱动程序](initializing-a-protocol-driver.md)。 ) NDIS 6.0 和更高版本中间驱动程序的初始化不同于旧中间驱动程序的初始化。 此外，NDIS 6.0 和更高版本的驱动程序可以注册为组合微型端口中间驱动程序。

以下主题提供了有关中间驱动程序初始化的详细信息：

-   [初始化中间驱动程序](initializing-an-intermediate-driver.md)
-   [初始化微型端口中间驱动程序](initializing-a-miniport-intermediate-driver.md)
-   [卸载中间驱动程序](unloading-an-intermediate-driver.md)
-   [初始化虚拟微型端口](initializing-a-virtual-miniport.md)
-   [停止虚拟微型端口](halting-a-virtual-miniport.md)

 

