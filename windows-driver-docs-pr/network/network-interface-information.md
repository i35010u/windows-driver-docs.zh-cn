---
title: 网络接口信息
description: 网络接口信息
ms.assetid: 4d8cd9c2-6f78-4c70-83bd-f36fffbf1c35
keywords:
- NDIS 网络接口 WDK，有关
- 网络接口 WDK，有关
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 61390aa3b9ed90ce6910cc58cc25502e1e9dba63
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827224"
---
# <a name="network-interface-information"></a>网络接口信息





接口提供程序通过使用以下数据结构来提供有关每个注册接口的信息。

-   [**NET\_IF\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_if_information)

-   [**NDIS\_接口\_信息**](https://docs.microsoft.com/windows/desktop/api/ifdef/ns-ifdef-_ndis_interface_information)

若要注册接口，提供程序会将指向已初始化的 NET\_的指针传递到[**NdisIfRegisterInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisifregisterinterface)函数的\_信息结构。

NDIS 接口提供程序提供一个[**NDIS\_接口\_信息**](https://docs.microsoft.com/windows/desktop/api/ifdef/ns-ifdef-_ndis_interface_information)结构，以响应[oid\_第一代\_接口\_INFO](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-interface-info) OID 的查询。

NDIS 还可以通过其他 Oid 来查询提供程序。 有关 NDIS 提供程序 Oid 的详细信息，请参阅[用于 OID 映射的 Ndis 网络接口](mapping-of-ndis-network-interfaces-to-ndis-oids.md)。 有关在接口提供程序中处理 OID 请求的详细信息，请参阅[在 NDIS 接口提供程序中处理 Oid 查询和设置请求](handling-oid-query-and-set-requests-in-an-ndis-interface-provider.md)。

 

 





