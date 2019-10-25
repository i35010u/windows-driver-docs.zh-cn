---
title: 微型端口适配器同步 OID 请求
description: 本主题介绍微型端口适配器同步 OID 请求
ms.assetid: E169972C-2EFF-4005-B279-9EFC53B431E2
keywords: 微型端口适配器同步 OID 请求接口，微型端口适配器同步 OID 调用，WDK 微型端口适配器同步 oid，微型端口适配器同步 OID 请求
ms.date: 09/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c6b055941a4ed1da1bd033b4d3d3ee85bf796387
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844242"
---
# <a name="miniport-adapter-synchronous-oid-requests"></a>微型端口适配器同步 OID 请求

若要支持同步 OID 请求路径，小型端口驱动程序会在\_NDIS 中提供[*MiniportSynchronousOidRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-miniport_synchronous_oid_request)函数入口点[ **\_驱动\_程序**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_driver_characteristics)在调用[**NdisMRegisterMiniportDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterminiportdriver)函数。

对于微型端口驱动程序，*同步 OID 请求接口*不同于普通的和直接 OID 请求接口，该小型端口驱动程序无需注册异步*完成*回调函数。 这是因为路径的同步特性。 有关常规、直接和同步 Oid 之间的差异的详细信息，请参阅[NDIS 6.80 中的同步 Oid 请求接口](synchronous-oid-request-interface-in-ndis-6-80.md)。

> [!NOTE]
> NDIS 6.80 支持用于同步 OID 请求接口的特定 Oid。 不支持在 NDIS 6.80 和某些 NDIS 6.80 Oid 之前存在的 Oid。 若要确定是否可以在同步 OID 请求接口中使用 OID，请参见 "OID 引用" 页。

若要支持同步 OID 请求接口，请使用标准 OID 请求接口的文档。 下表显示了同步 OID 请求接口中的函数与标准 OID 请求接口之间的关系。

| 同步 OID 函数 | 标准 OID 函数 |
| --- | --- |
| [*MiniportSynchronousOidRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-miniport_synchronous_oid_request) | [*MiniportOidRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request) |

