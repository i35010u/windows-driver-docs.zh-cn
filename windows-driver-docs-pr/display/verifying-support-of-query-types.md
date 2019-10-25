---
title: 验证查询类型支持
description: 验证查询类型支持
ms.assetid: 0f925796-d827-42ba-9232-8f221919e6d4
keywords:
- 异步查询操作 WDK DirectX 9.0，验证查询类型支持
- 查询操作 WDK DirectX 9.0，验证查询类型支持
- 查询类型 WDK DirectX 9。0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 579724169f8b5e77d31efbadf682e2b646e923c2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825319"
---
# <a name="verifying-support-of-query-types"></a>验证查询类型支持


## <span id="ddk_verifying_support_of_query_types_gg"></span><span id="DDK_VERIFYING_SUPPORT_OF_QUERY_TYPES_GG"></span>


DirectX 9.0 运行时必须验证驱动程序支持的查询类型，然后才能执行任何异步查询操作。 若要验证驱动程序支持的查询类型数量，运行时将使用 D3DGDI2\_类型\_GETD3DQUERYCOUNT 值发送**GetDriverInfo2**请求。 如果该驱动程序不支持任何查询类型，它将在此请求的[**DD\_GETD3DQUERYCOUNTDATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_dd_getd3dquerycountdata)结构的**dwNumQueries**成员中返回零。

若要接收每个支持的查询类型的相关信息，运行时将使用 D3DGDI2\_类型为每种类型\_GETD3DQUERY 值发送**GetDriverInfo2**请求。 然后，该驱动程序将返回[**DD\_GETD3DQUERYDATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_dd_getd3dquerydata)结构中有关查询类型的信息。 有关**GetDriverInfo2**的详细信息，请参阅[支持 GetDriverInfo2](supporting-getdriverinfo2.md)。

 

 





