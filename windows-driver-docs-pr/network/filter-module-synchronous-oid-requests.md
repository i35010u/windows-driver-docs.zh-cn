---
title: 筛选器模块同步 OID 请求
description: 本主题介绍筛选器模块同步 OID 请求
ms.assetid: 14C6555D-D8E6-4DEB-96C8-D4F18F06CE6B
keywords: 筛选器模块同步 OID 请求接口，筛选器模块同步 OID 调用，WDK 筛选器模块同步 oid，筛选器模块同步 OID 请求
ms.date: 04/03/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4a47b10973c0b8f82f8c17e05063c5d08f0d81d0
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89213969"
---
# <a name="filter-module-synchronous-oid-requests"></a>筛选器模块同步 OID 请求

为了支持同步 OID 请求路径，筛选器驱动程序会在调用[**NdisFRegisterFilterDriver**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfregisterfilterdriver)函数时在[**NDIS \_ 筛选器 \_ 驱动程序 \_ 特征**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_filter_driver_characteristics)结构中提供[*FilterSynchronousOidRequest*](/windows-hardware/drivers/ddi/ndis/nf-ndis-filter_synchronous_oid_request)函数入口点。

> [!NOTE]
> NDIS 6.81 支持用于同步 OID 请求接口的特定 Oid。 不支持在 NDIS 6.80 和某些 NDIS 6.80 Oid 之前存在的 Oid。 若要确定是否可以在同步 OID 请求接口中使用 OID，请参见 "OID 引用" 页。

若要支持同步 OID 请求接口，请使用标准 OID 请求接口的文档。 下表显示了同步 OID 请求接口中的函数与标准 OID 请求接口之间的关系。

| 同步 OID 函数 | 标准 OID 函数 |
| --- | --- |
| [*FilterSynchronousOidRequest*](/windows-hardware/drivers/ddi/ndis/nf-ndis-filter_synchronous_oid_request) | [*FilterOidRequest*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_oid_request) |
| [*FilterSynchronousOidRequestComplete*](/windows-hardware/drivers/ddi/ndis/nf-ndis-filter_synchronous_oid_request_complete) | [*FilterOidRequestComplete*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_oid_request_complete) |