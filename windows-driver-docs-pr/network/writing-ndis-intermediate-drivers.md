---
title: 编写 NDIS 中间驱动程序
description: 编写 NDIS 中间驱动程序
ms.assetid: c37224b2-8d96-44c2-8b56-884089b9cfcd
keywords:
- 中间驱动程序 WDK 网络
- 网络驱动程序 WDK，中间驱动程序
- NDIS WDK，中间驱动程序
- NDIS 中间驱动程序 WDK
- NDIS 中间层驱动程序 WDK、 NDIS 6.0
- 中间驱动程序 WDK 网络 NDIS 6.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 778305aac1f12c04b2a1569e32533e7aba4fe4f5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544752"
---
# <a name="writing-ndis-intermediate-drivers"></a>编写 NDIS 中间驱动程序





除非另有说明，中间的 NDIS 驱动程序提供与微型端口驱动程序和协议驱动程序相同的服务。 中间的驱动程序微型端口边缘提供微型端口驱动程序服务，协议 edge 提供协议驱动程序服务。 (有关详细信息，请参阅[编写 NDIS 微型端口驱动程序](writing-ndis-miniport-drivers.md)并[编写 NDIS 协议驱动程序](writing-ndis-protocol-drivers.md)。)NDIS 6.0 和更高版本中间驱动程序初始化是不同于旧中间驱动程序的初始化。 此外，NDIS 6.0 和更高版本的驱动程序可以将注册为组合的中间微型端口驱动程序。

以下主题提供有关中间驱动程序初始化的详细信息：

-   [初始化中间驱动程序](initializing-an-intermediate-driver.md)
-   [初始化中间微型端口驱动程序](initializing-a-miniport-intermediate-driver.md)
-   [卸载中间驱动程序](unloading-an-intermediate-driver.md)
-   [初始化虚拟微型端口](initializing-a-virtual-miniport.md)
-   [正在停止虚拟微型端口](halting-a-virtual-miniport.md)

 

 





