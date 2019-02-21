---
title: 若要移植到 NDIS 6.20 的中间驱动程序的更改摘要
description: 若要移植到 NDIS 6.20 的中间驱动程序所需的更改的摘要
ms.assetid: 1ed2b2f6-f337-4aaa-9ce8-90adf7d05722
keywords:
- NDIS 6.20 WDK，移植中间驱动程序
- 移植到 NDIS 6.20 WDK 中间驱动程序
- 中间驱动程序 WDK
- 中间驱动程序 WDK，移植到 NDIS 6.20
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: db041a9df84df68357d18217f1434f69465e2ce9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541641"
---
# <a name="summary-of-changes-required-to-port-an-intermediate-driver-to-ndis-620"></a>若要移植到 NDIS 6.20 的中间驱动程序所需的更改的摘要





本主题概述了所需端口 NDIS 6 的更改。*x*中间驱动程序添加到 NDIS 6.20。

若要更新的中间驱动程序来支持 NDIS 6.20 环境，则必须修改 NDIS 6。*x*中间层驱动程序，如下所示：

<a href="" id="build-environment-------"></a>**构建环境**   
-   替换为预处理器定义 NDIS60\_微型端口\_驱动程序或 NDIS61\_微型端口\_驱动程序和 NDIS620\_微型端口\_驱动程序。

-   替换 NDIS620 NDIS61 或 NDIS60 的预处理器定义。

<a href="" id="general-porting-requirements-------"></a>**移植的一般要求**   
-   除外另行，协议驱动程序和微型端口驱动程序的更改也适用于中间驱动程序。 有关移植这些驱动程序的详细信息，请参阅协议驱动程序移植在摘要[摘要的更改所需端口协议驱动程序添加到 NDIS 6.20](summary-of-changes-required-to-port-a-protocol-driver-to-ndis-6-20.md)和微型端口驱动程序移植摘要，[摘要若要移植到 NDIS 6.20 的微型端口驱动程序所需的更改](summary-of-changes-required-to-port-a-miniport-driver-to-ndis-6-20.md)。

-   NDIS 5.x 筛选器中间驱动程序将不支持在 Microsoft Windows 版本后 Windows 7。 应为所有筛选器驱动程序使用 NDIS 筛选器驱动程序接口。 NDIS 筛选器驱动程序有关的详细信息，请参阅[摘要的更改所需端口筛选器驱动程序到 NDIS 6.20](summary-of-changes-required-to-port-a-filter-driver-to-ndis-6-20.md)。

 

 





