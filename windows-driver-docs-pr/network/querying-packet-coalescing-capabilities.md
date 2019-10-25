---
title: 查询数据包合并功能
description: 查询数据包合并功能
ms.assetid: CD1839B5-2279-4E8C-ADD8-7869A3123B86
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 23964e3c7f2609f41511fb53ae5af74fe4132b79
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844884"
---
# <a name="querying-packet-coalescing-capabilities"></a>查询数据包合并功能


初始化微型端口驱动程序后，上层驱动程序和应用程序可以发出以下 OID 查询请求，以获取网络适配器的数据包合并功能：

-   [OID\_接收\_筛选器\_硬件\_功能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-hardware-capabilities)

-   [OID\_接收\_筛选器\_当前\_功能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-current-capabilities)

-   [OID\_接收\_筛选器\_全局\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-global-parameters)

NDIS 处理微型端口驱动程序的这些 OID 查询请求，并返回在 NDIS 调用驱动程序的[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)函数时，已注册的微型端口驱动程序的数据包合并功能。 因此，这些 OID 查询请求不由微型端口驱动程序处理。

有关微型端口驱动程序如何注册其包合并功能的详细信息，请参阅[确定接收筛选功能](determining-receive-filtering-capabilities.md)。

 

 





