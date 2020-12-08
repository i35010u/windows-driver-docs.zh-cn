---
title: 使用筛选器 ID
description: 使用筛选器 ID
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7e235867edcd653d5eeff70797c36a1611b5a4a8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96790391"
---
# <a name="using-the-filter-id"></a>使用筛选器 ID


过量驱动程序通过发出 [oid \_ 接收 \_ 筛选器 \_ 集 \_ 筛选器](./oid-receive-filter-set-filter.md)的 oid 方法请求，将接收筛选器下载到微型端口驱动程序。 下载到微型端口驱动程序的每个接收筛选器都有一个唯一的筛选器标识符 (ID) 由 NDIS 生成。 过量驱动程序必须在后续 OID 请求中使用此筛选器 ID 才能执行以下操作：

-   查询接收筛选器参数。 有关如何查询接收筛选器参数的详细信息，请参阅 [查询数据包合并接收筛选器](querying-packet-coalescing-receive-filters.md)。

-   修改接收筛选器参数。 有关如何修改接收筛选器参数的详细信息，请参阅 [修改包合并接收筛选器](modifying-packet-coalescing-receive-filters.md)。

-   "免费" 或 " *清除*" 接收筛选器。 有关如何清除接收筛选器的详细信息，请参阅 [清除数据包合并接收筛选器](clearing-packet-coalescing-receive-filters.md)。

微型端口驱动程序必须保留已分配接收筛选器的筛选器 Id。 当接收到 OID 请求来修改、查询或释放接收筛选器时，微型端口驱动程序必须验证 OID 请求中的指定筛选器 ID 是否与 [oid 接收筛选器 \_ \_ \_ 集 \_ 筛选器](./oid-receive-filter-set-filter.md)以前的 oid 方法请求中的已分配接收筛选器匹配。 如果筛选器 ID 与任何分配的接收筛选器都不匹配，则微型端口驱动程序必须完成 OID 请求，状态为 "失败"。

 

