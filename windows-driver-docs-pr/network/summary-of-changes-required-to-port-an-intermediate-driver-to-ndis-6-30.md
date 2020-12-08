---
title: 将中间驱动程序移植到 NDIS 6.30 的更改摘要
description: 若要更新 NDIS 1.x 中间 (IM) 驱动程序以支持 NDIS 6.30，必须按照以下各节中所述修改它。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5c753ee540eedbd09fbbf503856d08e3b102cb3f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96825405"
---
# <a name="summary-of-changes-required-to-port-an-intermediate-driver-to-ndis-630"></a>将中间驱动程序移植到 NDIS 6.30 所要做出的更改摘要


若要更新 NDIS 1.x 中间 (IM) 驱动程序以支持 NDIS 6.30，必须按照以下各节中所述修改它。

## <a name="build-environment"></a>生成环境


-   将预处理器定义 NDIS60 或 NDIS61 或 NDIS620 （如果存在）替换为 NDIS630。
-   \_*Xxx* \_ \_ 如 [实现 ndis 6.30 驱动程序](implementing-an-ndis-6-30-driver.md)中所述，在 ndis Xxx 驱动程序特征结构中更新主要和次要的 ndis 版本号。

## <a name="general-porting-requirements"></a>一般移植要求


-   除非另外注明，否则协议驱动程序和微型端口驱动程序更改也适用于中间驱动程序。 有关移植这些驱动程序的详细信息，请参阅将 [协议或筛选器驱动程序移植到 ndis 6.30 所需的更改摘要](summary-of-changes-required-to-port-a-protocol-or-filter-driver-to-ndis-6-30.md) 和将 [微型端口驱动程序移植到 Ndis 6.30 所需的更改摘要](summary-of-changes-required-to-port-a-miniport-driver-to-ndis-6-30.md)。

 

 





