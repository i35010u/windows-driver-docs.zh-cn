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
ms.openlocfilehash: 294ca5ee5e744305ffc74475ef2fcc8a7e074919
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89064088"
---
# <a name="imposing-requirements-on-the-d3ddrawprimitives2-ddi"></a>对 D3dDrawPrimitives2 DDI 施加要求


## <span id="ddk_imposing_requirements_on_the_d3ddrawprimitives2_ddi_gg"></span><span id="DDK_IMPOSING_REQUIREMENTS_ON_THE_D3DDRAWPRIMITIVES2_DDI_GG"></span>


用于处理异步查询的 DirectX 9.0 版本驱动程序的能力对驱动程序的 [**D3dDrawPrimitives2**](/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb) 函数有两个新的要求。 以下列表概述了 [处理异步查询](handling-asynchronous-queries.md) 主题中提到的这些要求：

-   驱动程序的 *D3dDrawPrimitives2* 函数必须确保它可以处理空的命令缓冲区，因为运行时可能会提交它们，以便驱动程序可以写入更多响应。 如果驱动程序以前在 \_ 响应缓冲区中返回了 D3DDP2OP RESPONSECONTINUE 操作代码，则运行时在传入命令流中提交空的命令缓冲区。

-   如果成功 (*D3dDrawPrimitives2*将[**D3DHAL \_ DRAWPRIMITIVES2DATA**](/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_drawprimitives2data)结构的**ddrval**设置为 D3D \_ OK) ，则驱动程序必须确保在响应可用时，该驱动程序必须将 dwErrorOffset D3DHAL 的**DRAWPRIMITIVES2DATA**成员设置 \_ 为非零。 如果驱动程序没有响应任何查询并且 **ddrval** 为 D3D，则 \_ 必须将 **dwErrorOffset** 设置为零。

 

