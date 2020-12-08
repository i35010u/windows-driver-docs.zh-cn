---
title: 将中间驱动程序移植到 NDIS 6.20 的更改摘要
description: 将中间驱动程序移植到 NDIS 6.20 所要做出的更改摘要
keywords:
- NDIS 6.20 WDK，移植中间驱动程序
- 将中间驱动程序移植到 NDIS 6.20 WDK
- 中间驱动程序 WDK
- 中级驱动程序 WDK，移植到 NDIS 6.20
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: def81cf6b227e6587a346bd1eef8dfba78f34a42
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96825409"
---
# <a name="summary-of-changes-required-to-port-an-intermediate-driver-to-ndis-620"></a>将中间驱动程序移植到 NDIS 6.20 所要做出的更改摘要





本主题概述了移植 NDIS 6 所需的更改。*x* 中级驱动程序到 NDIS 6.20。

若要更新中间驱动程序以支持 NDIS 6.20 环境，必须修改 NDIS 6。*x* 中间驱动程序，如下所示：

<a href="" id="build-environment-------"></a>**生成环境**   
-   将预处理器定义 NDIS60 \_ 微型端口 \_ 驱动程序或 NDIS61 微型端口驱动程序替换 \_ \_ 为 NDIS620 \_ 微型端口驱动 \_ 程序。

-   将预处理器定义 NDIS61 或 NDIS60 替换为 NDIS620。

<a href="" id="general-porting-requirements-------"></a>**一般移植要求**   
-   除非另外注明，否则协议驱动程序和微型端口驱动程序更改也适用于中间驱动程序。 有关移植这些驱动程序的详细信息，请参阅协议驱动程序迁移摘要，其中概述了在将[微型端口驱动程序移植到 ndis 6.20](summary-of-changes-required-to-port-a-miniport-driver-to-ndis-6-20.md)所需的更改所[需的将协议驱动程序移植到 ndis 6.20](summary-of-changes-required-to-port-a-protocol-driver-to-ndis-6-20.md)和微型端口驱动程序的更改摘要。

-   Windows 7 之后的 Microsoft Windows 版本中不支持 NDIS 1.x 筛选器中间驱动程序。 应为所有筛选器驱动程序使用 NDIS 筛选器驱动程序接口。 有关 NDIS 筛选器驱动程序的详细信息，请参阅 [将筛选器驱动程序移植到 NDIS 6.20 所需的更改摘要](summary-of-changes-required-to-port-a-filter-driver-to-ndis-6-20.md)。

 

 





