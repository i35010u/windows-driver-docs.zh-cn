---
title: 网络接口信息
description: 网络接口信息
keywords:
- NDIS 网络接口 WDK，有关
- 网络接口 WDK，有关
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7bfb311adb2b1d9849bee10f6d8d3d610d1116b7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96792671"
---
# <a name="network-interface-information"></a>网络接口信息





接口提供程序通过使用以下数据结构来提供有关每个注册接口的信息。

-   [**NET \_ IF \_ 信息**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_if_information)

-   [**NDIS \_ 接口 \_ 信息**](/windows/win32/api/ifdef/ns-ifdef-ndis_interface_information)

若要注册接口，提供程序会将指向已初始化的 NET \_ IF \_ 信息结构的指针传递到 [**NdisIfRegisterInterface**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisifregisterinterface) 函数。

NDIS 接口提供程序提供 [**ndis \_ 接口 \_ 信息**](/windows/win32/api/ifdef/ns-ifdef-ndis_interface_information) 结构，以响应 [oid 生成 \_ \_ 接口 \_ 信息](./oid-gen-interface-info.md) oid 的查询。

NDIS 还可以通过其他 Oid 来查询提供程序。 有关 NDIS 提供程序 Oid 的详细信息，请参阅 [用于 OID 映射的 Ndis 网络接口](mapping-of-ndis-network-interfaces-to-ndis-oids.md)。 有关在接口提供程序中处理 OID 请求的详细信息，请参阅 [在 NDIS 接口提供程序中处理 Oid 查询和设置请求](handling-oid-query-and-set-requests-in-an-ndis-interface-provider.md)。

 

