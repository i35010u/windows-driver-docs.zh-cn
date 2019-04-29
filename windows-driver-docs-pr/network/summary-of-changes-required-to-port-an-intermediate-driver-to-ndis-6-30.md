---
title: 若要移植到 NDIS 6.30 中间驱动程序的更改摘要
description: 若要更新的 NDIS 6.x 中间 (IM) 驱动程序以支持 NDIS 6.30，您必须修改以下各节中所述。
ms.assetid: 02FAC8B2-16B1-49C2-8B3A-29535A698CEA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 006c3baf552407484f36085a8b9c8f53044e61e7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376917"
---
# <a name="summary-of-changes-required-to-port-an-intermediate-driver-to-ndis-630"></a>将中间驱动程序移植到 NDIS 6.30 所要做出的更改摘要


若要更新的 NDIS 6.x 中间 (IM) 驱动程序以支持 NDIS 6.30，您必须修改以下各节中所述。

## <a name="build-environment"></a>构建环境


-   替换为预处理器定义 NDIS60 或 NDIS61 或 NDIS620，如果存在，NDIS630。
-   更新的主版本号和次的 NDIS 版本编号在 NDIS\_*Xxx*\_驱动程序\_特征结构中所述[实现 NDIS 6.30 驱动程序](implementing-an-ndis-6-30-driver.md).

## <a name="general-porting-requirements"></a>移植的一般要求


-   除外另行，协议驱动程序和微型端口驱动程序的更改也适用于中间驱动程序。 有关移植这些驱动程序的详细信息，请参阅[摘要的更改所需端口的协议或筛选器驱动程序添加到 NDIS 6.30](summary-of-changes-required-to-port-a-protocol-or-filter-driver-to-ndis-6-30.md)和[摘要的更改所需移植到 NDIS 6.30微型端口驱动程序](summary-of-changes-required-to-port-a-miniport-driver-to-ndis-6-30.md).

 

 





