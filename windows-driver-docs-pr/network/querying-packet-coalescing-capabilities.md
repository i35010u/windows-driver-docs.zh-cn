---
title: 查询数据包合并功能
description: 查询数据包合并功能
ms.assetid: CD1839B5-2279-4E8C-ADD8-7869A3123B86
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9842f5db04a05c9c60bd80a23f64c2aa7676173d
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89212055"
---
# <a name="querying-packet-coalescing-capabilities"></a>查询数据包合并功能


初始化微型端口驱动程序后，上层驱动程序和应用程序可以发出以下 OID 查询请求，以获取网络适配器的数据包合并功能：

-   [OID \_ 接收 \_ 筛选器 \_ 硬件 \_ 功能](./oid-receive-filter-hardware-capabilities.md)

-   [OID \_ 接收 \_ 筛选器 \_ 当前 \_ 功能](./oid-receive-filter-current-capabilities.md)

-   [OID \_ 接收 \_ 筛选器 \_ 全局 \_ 参数](./oid-receive-filter-global-parameters.md)

NDIS 处理微型端口驱动程序的这些 OID 查询请求，并返回在 NDIS 调用驱动程序的 [*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize) 函数时，已注册的微型端口驱动程序的数据包合并功能。 因此，这些 OID 查询请求不由微型端口驱动程序处理。

有关微型端口驱动程序如何注册其包合并功能的详细信息，请参阅 [确定接收筛选功能](determining-receive-filtering-capabilities.md)。

 

