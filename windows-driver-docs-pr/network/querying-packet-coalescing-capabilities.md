---
title: 查询数据包合并功能
description: 查询数据包合并功能
ms.assetid: CD1839B5-2279-4E8C-ADD8-7869A3123B86
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a5bf109b70aa92325922e99847fc969e86c3161f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63340001"
---
# <a name="querying-packet-coalescing-capabilities"></a>查询数据包合并功能


初始化微型端口驱动程序，过量驱动程序和应用程序可以发出以下 OID 查询请求以获取网络适配器的数据包合并功能：

-   [OID\_RECEIVE\_FILTER\_HARDWARE\_CAPABILITIES](https://msdn.microsoft.com/library/windows/hardware/ff569791)

-   [OID\_RECEIVE\_FILTER\_CURRENT\_CAPABILITIES](https://msdn.microsoft.com/library/windows/hardware/ff569786)

-   [OID\_接收\_筛选器\_GLOBAL\_参数](https://msdn.microsoft.com/library/windows/hardware/ff569790)

NDIS 处理这些 OID 查询请求的微型端口驱动程序，并返回的数据包合并功能的微型端口驱动程序时 NDIS 称为驱动程序的注册[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)函数。 因此，由微型端口驱动程序不处理这些 OID 查询请求。

合并功能，请参阅有关微型端口驱动程序如何注册其数据包[确定收到的筛选功能](determining-receive-filtering-capabilities.md)。

 

 





