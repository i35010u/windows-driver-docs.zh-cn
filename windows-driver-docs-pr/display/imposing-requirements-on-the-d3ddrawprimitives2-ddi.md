---
title: 对 D3dDrawPrimitives2 DDI 施加要求
description: 对 D3dDrawPrimitives2 DDI 施加要求
ms.assetid: a016c127-14ad-42ba-aae5-97c6c97b01f6
keywords:
- 异步查询操作 WDK DirectX 9.0 D3dDrawPrimitives2
- 查询操作 WDK DirectX 9.0 D3dDrawPrimitives2
- D3dDrawPrimitives2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2360ec25c89bb3324d5fe0bfc47d3821d9dacd80
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383932"
---
# <a name="imposing-requirements-on-the-d3ddrawprimitives2-ddi"></a>对 D3dDrawPrimitives2 DDI 施加要求


## <span id="ddk_imposing_requirements_on_the_d3ddrawprimitives2_ddi_gg"></span><span id="DDK_IMPOSING_REQUIREMENTS_ON_THE_D3DDRAWPRIMITIVES2_DDI_GG"></span>


DirectX 9.0 版本驱动程序能够处理异步查询对施加两个新驱动程序的要求[ **D3dDrawPrimitives2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)函数。 这些要求中所述[处理异步查询](handling-asynchronous-queries.md)主题，以下列表总结了：

-   在驱动程序*D3dDrawPrimitives2*函数必须确保它可以处理空命令缓冲区，因为运行时可能会将其提交，以便该驱动程序可以编写更多的答复。 在运行时提交时传入的命令流中的空命令缓冲区，如果该驱动程序之前返回 D3DDP2OP\_RESPONSECONTINUE 响应缓冲区中的操作代码。

-   上的成功*D3dDrawPrimitives2* (**ddrval**的[ **D3DHAL\_DRAWPRIMITIVES2DATA** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/ns-d3dhal-_d3dhal_drawprimitives2data)结构设置为 D3D\_确定)，该驱动程序必须确保其唯一集**dwErrorOffset** D3DHAL 成员\_DRAWPRIMITIVES2DATA 到响应可用时，非零值。 如果该驱动程序不响应任何查询并**ddrval**是 D3D\_确定， **dwErrorOffset**必须设置为零。

 

 





