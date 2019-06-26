---
title: 查询数据包合并功能
description: 查询数据包合并功能
ms.assetid: CD1839B5-2279-4E8C-ADD8-7869A3123B86
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9f2b8c656d99a9816ab5884517a2c49a529e00e6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353303"
---
# <a name="querying-packet-coalescing-capabilities"></a>查询数据包合并功能


初始化微型端口驱动程序，过量驱动程序和应用程序可以发出以下 OID 查询请求以获取网络适配器的数据包合并功能：

-   [OID\_RECEIVE\_FILTER\_HARDWARE\_CAPABILITIES](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-hardware-capabilities)

-   [OID\_RECEIVE\_FILTER\_CURRENT\_CAPABILITIES](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-current-capabilities)

-   [OID\_接收\_筛选器\_GLOBAL\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-global-parameters)

NDIS 处理这些 OID 查询请求的微型端口驱动程序，并返回的数据包合并功能的微型端口驱动程序时 NDIS 称为驱动程序的注册[ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)函数。 因此，由微型端口驱动程序不处理这些 OID 查询请求。

合并功能，请参阅有关微型端口驱动程序如何注册其数据包[确定收到的筛选功能](determining-receive-filtering-capabilities.md)。

 

 





