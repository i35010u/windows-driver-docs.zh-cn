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
ms.openlocfilehash: a529576ccdf71c7e9e7461700942c5f6d6b9bc56
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89067050"
---
# <a name="verifying-support-of-query-types"></a>验证查询类型支持


## <span id="ddk_verifying_support_of_query_types_gg"></span><span id="DDK_VERIFYING_SUPPORT_OF_QUERY_TYPES_GG"></span>


DirectX 9.0 运行时必须验证驱动程序支持的查询类型，然后才能执行任何异步查询操作。 若要验证驱动程序支持的查询类型数量，运行时将使用 D3DGDI2 **GetDriverInfo2** \_ 类型 GETD3DQUERYCOUNT 值发送 GetDriverInfo2 请求 \_ 。 如果驱动程序不支持任何查询类型，它将在此请求的[**DD \_ GETD3DQUERYCOUNTDATA**](/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_dd_getd3dquerycountdata)结构的**dwNumQueries**成员中返回零。

若要接收每个支持的查询类型的相关信息， **GetDriverInfo2**运行时将使用 D3DGDI2 \_ type \_ GETD3DQUERY 值为每个类型发送 GetDriverInfo2 请求。 然后，该驱动程序返回有关 [**DD \_ GETD3DQUERYDATA**](/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_dd_getd3dquerydata) 结构中的查询类型的信息。 有关 **GetDriverInfo2**的详细信息，请参阅 [支持 GetDriverInfo2](supporting-getdriverinfo2.md)。

 

