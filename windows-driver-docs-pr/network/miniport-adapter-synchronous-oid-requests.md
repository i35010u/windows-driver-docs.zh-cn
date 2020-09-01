---
title: 微型端口适配器同步 OID 请求
description: 本主题介绍微型端口适配器同步 OID 请求
ms.assetid: E169972C-2EFF-4005-B279-9EFC53B431E2
keywords: 微型端口适配器同步 OID 请求接口，微型端口适配器同步 OID 调用，WDK 微型端口适配器同步 oid，微型端口适配器同步 OID 请求
ms.date: 09/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 93f31469518ee4b290cd465ad56071a095eb6765
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89215566"
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