---
title: 筛选模块同步 OID 请求
description: 本主题介绍了筛选器模块同步 OID 请求
ms.assetid: 14C6555D-D8E6-4DEB-96C8-D4F18F06CE6B
keywords: 筛选器模块同步 OID 请求接口，筛选器模块同步 OID 调用，WDK 筛选器模块同步 Oid，筛选器模块同步 OID 请求
ms.date: 04/03/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9ad38bda86c3cd938ae7bececf60dd5dd631e04d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555231"
---
# <a name="filter-module-synchronous-oid-requests"></a>筛选模块同步 OID 请求

若要支持同步 OID 请求路径，筛选器驱动程序提供[ *FilterSynchronousOidRequest* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-filter_synchronous_oid_request)函数中的入口点[ **NDIS\_筛选器\_驱动程序\_特征**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_filter_driver_characteristics)结构时它们调用[ **NdisFRegisterFilterDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfregisterfilterdriver)函数。

> [!NOTE]
> NDIS 6.81 支持用于同步的 OID 请求接口的特定 Oid。 不支持 NDIS 6.80 和一些 NDIS 6.80 Oid 之前即已存在的 Oid。 若要确定是否可以在同步 OID 请求界面中使用 OID，请参阅 OID 引用页。

若要支持同步 OID 请求接口，使用标准的 OID 请求接口的文档。 下表显示了同步 OID 请求接口中的函数和标准的 OID 请求接口之间的关系。

| 同步 OID 函数 | 标准 OID 函数 |
| --- | --- |
| [*FilterSynchronousOidRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-filter_synchronous_oid_request) | [*FilterOidRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_oid_request) |
| [*FilterSynchronousOidRequestComplete*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-filter_synchronous_oid_request_complete) | [*FilterOidRequestComplete*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_oid_request_complete) | 
