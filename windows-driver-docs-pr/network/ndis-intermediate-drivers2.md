---
title: 中间的 NDIS 驱动程序
description: 中间的 NDIS 驱动程序
ms.assetid: 773d9711-fdea-4541-bb0d-6b07b50892fc
keywords:
- 中间驱动程序 WDK 网络
- 网络驱动程序 WDK，中间驱动程序
- NDIS WDK，中间驱动程序
- NDIS 中间驱动程序 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4393badc6ca918eaf0ecf5120de93f329f5d587b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520783"
---
# <a name="ndis-intermediate-drivers"></a>中间的 NDIS 驱动程序





NDIS 中间层之间的较高级别协议驱动程序和微型端口驱动程序的驱动程序接口。 某些应用程序可能需要中间驱动程序包括：

-   媒体的旧传输驱动程序和管理的媒体类型未知的传输驱动程序微型端口驱动程序之间的转换。

-   出于安全性或其他目的筛选的数据。

-   加载平衡故障转移 (LBFO) 解决方案。

-   监视和收集网络数据统计信息。

然后再尝试编写中间驱动程序，您应该了解 NDIS 微型端口和协议驱动程序。 有关 NDIS 微型端口驱动程序的详细信息，请参阅[NDIS 微型端口驱动程序](ndis-miniport-drivers.md)。 有关协议的 NDIS 驱动程序的详细信息，请参阅[协议的 NDIS 驱动程序](ndis-protocol-drivers.md)。

以下各节介绍中间驱动程序，并描述如何创建和安装此类驱动程序：

[用于开发中间的 NDIS 驱动程序的路线图](roadmap-for-developing-ndis-intermediate-drivers.md)

[中间的 NDIS 驱动程序简介](introduction-to-ndis-intermediate-drivers.md)

[编写 NDIS 中间驱动程序](writing-ndis-intermediate-drivers.md)

[中间驱动程序设计概念](intermediate-driver-design-concepts.md)

[安装中间驱动程序](installing-an-intermediate-driver.md)

 

 





