---
title: 了解中间驱动程序
description: 了解中间驱动程序
keywords:
- 无连接驱动程序 WDK 网络
- 面向连接的驱动程序 WDK 网络
- 中级驱动程序 WDK 网络，无连接的下边缘
- NDIS 中间驱动程序 WDK，无连接的下边缘
- 中级驱动程序 WDK 网络，面向连接的下边缘
- NDIS 中间驱动程序 WDK，面向连接的下边缘
- 网络驱动程序 WDK，类型
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a45edf18cb66c4c1aba55b10e685c39fc7373bdb
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96789707"
---
# <a name="learning-about-intermediate-drivers"></a>了解中间驱动程序





可以编写一个中间驱动程序，该驱动程序具有无连接或面向连接的下边缘。 以下列表说明了应阅读哪些 WDK 文档部分，具体取决于你编写的中间驱动程序的类型：

<a href="" id="intermediate-drivers-that-have-a-connectionless-lower-edge"></a>**具有无连接下边缘的中间驱动程序**  
如果你正在编写一个中间驱动程序，其下边缘提供连接到无连接微型端口驱动程序的接口，请阅读：

-   [NDIS 中间驱动程序](ndis-intermediate-drivers.md)

<a href="" id="intermediate-drivers-that-have-a-connection-oriented-lower-edge"></a>**具有面向连接的下边缘的中间驱动程序**  
如果你正在编写一个中间驱动程序，该驱动程序的下边缘提供面向连接的微型端口驱动程序的接口，请阅读：

-   [NDIS 中间驱动程序](ndis-intermediate-drivers.md)

-   [面向连接的 NDIS](connection-oriented-ndis.md)

 

 





