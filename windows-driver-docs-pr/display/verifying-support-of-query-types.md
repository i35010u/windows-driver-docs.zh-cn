---
title: 正在验证的查询类型的支持
description: 正在验证的查询类型的支持
ms.assetid: 0f925796-d827-42ba-9232-8f221919e6d4
keywords:
- 异步查询操作 WDK DirectX 9.0 中，验证的查询类型的支持
- 查询操作 WDK DirectX 9.0 中，验证的查询类型的支持
- 查询类型 WDK DirectX 9.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a6ae69298ebf203a16f2edbb9f431947309b6dbd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526827"
---
# <a name="verifying-support-of-query-types"></a>正在验证的查询类型的支持


## <span id="ddk_verifying_support_of_query_types_gg"></span><span id="DDK_VERIFYING_SUPPORT_OF_QUERY_TYPES_GG"></span>


DirectX 9.0 运行时必须验证可以执行哪些驱动程序支持在任何异步查询操作之前的查询类型。 若要验证的驱动程序支持的查询类型的数目，运行时发送**GetDriverInfo2**请求使用 D3DGDI2\_类型\_GETD3DQUERYCOUNT 值。 如果该驱动程序不支持任何查询类型，它将返回零**dwNumQueries**的成员[ **DD\_GETD3DQUERYCOUNTDATA** ](https://msdn.microsoft.com/library/windows/hardware/ff551539)此结构请求。

若要接收有关每个信息支持查询类型，运行时发送**GetDriverInfo2**请求使用 D3DGDI2\_类型\_GETD3DQUERY 每种类型的值。 该驱动程序然后返回中的查询类型有关的信息[ **DD\_GETD3DQUERYDATA** ](https://msdn.microsoft.com/library/windows/hardware/ff551541)结构。 有关详细信息**GetDriverInfo2**，请参阅[支持 GetDriverInfo2](supporting-getdriverinfo2.md)。

 

 





