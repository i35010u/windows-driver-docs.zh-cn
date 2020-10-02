---
title: 微型端口适配器同步 OID 请求
description: 了解微型端口适配器同步 OID 请求。 查看一个表，其中显示了同步 OID 和标准 OID 请求接口之间的关系。
ms.assetid: E169972C-2EFF-4005-B279-9EFC53B431E2
keywords: 微型端口适配器同步 OID 请求接口，微型端口适配器同步 OID 调用，WDK 微型端口适配器同步 oid，微型端口适配器同步 OID 请求
ms.date: 09/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0b5b2e9d5798213f343805f2d0cf78a238d9ed85
ms.sourcegitcommit: 372464be981a39781c71049126f36891cb5d0cad
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2020
ms.locfileid: "91646131"
---
# <a name="miniport-adapter-synchronous-oid-requests"></a>微型端口适配器同步 OID 请求

若要支持同步 OID 请求路径，微型端口驱动程序在调用[**NdisMRegisterMiniportDriver**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterminiportdriver)函数时在[**NDIS \_ 微型端口 \_ 驱动程序 \_ 特征**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_driver_characteristics)结构中提供[*MiniportSynchronousOidRequest*](/windows-hardware/drivers/ddi/ndis/nf-ndis-miniport_synchronous_oid_request)函数入口点。

对于微型端口驱动程序， *同步 OID 请求接口* 不同于普通的和直接 OID 请求接口，该小型端口驱动程序无需注册异步 *完成* 回调函数。 这是因为路径的同步特性。 有关常规、直接和同步 Oid 之间的差异的详细信息，请参阅 [NDIS 6.80 中的同步 Oid 请求接口](synchronous-oid-request-interface-in-ndis-6-80.md)。

> [!NOTE]
> NDIS 6.80 支持用于同步 OID 请求接口的特定 Oid。 不支持在 NDIS 6.80 和某些 NDIS 6.80 Oid 之前存在的 Oid。 若要确定是否可以在同步 OID 请求接口中使用 OID，请参见 "OID 引用" 页。

若要支持同步 OID 请求接口，请使用标准 OID 请求接口的文档。 下表显示了同步 OID 请求接口中的函数与标准 OID 请求接口之间的关系。

| 同步 OID 函数 | 标准 OID 函数 |
| --- | --- |
| [*MiniportSynchronousOidRequest*](/windows-hardware/drivers/ddi/ndis/nf-ndis-miniport_synchronous_oid_request) | [*MiniportOidRequest*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request) |