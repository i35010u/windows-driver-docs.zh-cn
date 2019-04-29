---
title: 使用筛选器 ID
description: 使用筛选器 ID
ms.assetid: 005AD1CF-37EB-44E8-BFA0-676ACCF69D47
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f65bd0a76e721999b7516d7f58a83fdddf1641ef
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373756"
---
# <a name="using-the-filter-id"></a>使用筛选器 ID


过量驱动程序下载到微型端口驱动程序筛选器接收通过发出的 OID 方法请求[OID\_接收\_筛选器\_设置\_筛选器](https://msdn.microsoft.com/library/windows/hardware/ff569795)。 每个下载到微型端口驱动程序的接收筛选器具有由 NDIS 生成唯一的筛选器标识符 (ID)。 基础驱动程序必须更高版本的 OID 请求中使用此筛选器 ID，以便执行以下操作：

-   查询的接收筛选器参数。 有关如何查询接收筛选器的参数的详细信息，请参阅[查询数据包合并接收筛选器](querying-packet-coalescing-receive-filters.md)。

-   修改接收筛选器参数。 有关如何修改的接收筛选器参数的详细信息，请参阅[修改数据包合并接收筛选器](modifying-packet-coalescing-receive-filters.md)。

-   免费的或者*清除*，接收筛选器。 有关如何清除接收筛选器的详细信息，请参阅[清除数据包合并接收筛选器](clearing-packet-coalescing-receive-filters.md)。

微型端口驱动程序必须保留已分配的接收筛选器的筛选器 Id。 微型端口驱动程序时收到 OID 请求修改、 查询，或免费接收筛选器，必须验证 OID 请求中指定的筛选器 ID 匹配的前一个 OID 方法请求的已分配的接收筛选器[OID\_接收\_筛选器\_设置\_筛选器](https://msdn.microsoft.com/library/windows/hardware/ff569795)。 如果筛选器 ID 不匹配任何已分配的接收筛选器，微型端口驱动程序必须完成 OID 请求具有失败状态。

 

 





