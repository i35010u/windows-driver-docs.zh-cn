---
title: 对 D3dDrawPrimitives2 DDI 施加要求
description: 对 D3dDrawPrimitives2 DDI 施加要求
ms.assetid: a016c127-14ad-42ba-aae5-97c6c97b01f6
keywords:
- 异步查询操作 WDK DirectX 9.0，D3dDrawPrimitives2
- 查询操作 WDK DirectX 9.0，D3dDrawPrimitives2
- D3dDrawPrimitives2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0a08057c8222dfedf72068006d4b5b920ec583f3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840460"
---
# <a name="imposing-requirements-on-the-d3ddrawprimitives2-ddi"></a>对 D3dDrawPrimitives2 DDI 施加要求


## <span id="ddk_imposing_requirements_on_the_d3ddrawprimitives2_ddi_gg"></span><span id="DDK_IMPOSING_REQUIREMENTS_ON_THE_D3DDRAWPRIMITIVES2_DDI_GG"></span>


用于处理异步查询的 DirectX 9.0 版本驱动程序的能力对驱动程序的[**D3dDrawPrimitives2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)函数有两个新的要求。 以下列表概述了[处理异步查询](handling-asynchronous-queries.md)主题中提到的这些要求：

-   驱动程序的*D3dDrawPrimitives2*函数必须确保它可以处理空的命令缓冲区，因为运行时可能会提交它们，以便驱动程序可以写入更多响应。 如果驱动程序之前返回的 D3DDP2OP\_RESPONSECONTINUE 操作代码位于响应缓冲区中，则运行时在传入命令流中提交空的命令缓冲区。

-   如果成功*D3dDrawPrimitives2* （ [**D3DHAL\_DRAWPRIMITIVES2DATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_drawprimitives2data)结构的**ddrval**设置为 D3D\_正常），则驱动程序必须确保它仅设置 dwErrorOffset 的**D3DHAL**成员\_当响应可用时，DRAWPRIMITIVES2DATA 为非零值。 如果驱动程序未响应任何查询， **ddrval**为 D3D\_"确定"，则**dwErrorOffset**必须设置为零。

 

 





