---
title: 光栅器块
description: 光栅器块
ms.assetid: 115c265d-0264-4a8a-b07b-710438394c68
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ed23f122fb8a13fb17d175d2b9f9f660e94705eb
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385036"
---
# <a name="rasterizer-block"></a>光栅器块


光栅器块剪辑、 设置基元，并确定如何调用像素着色器阶段。 Direct3D 运行时不会不查看管道中阶段的光栅器块。 相反，Direct3D 运行时将光栅器块视为碰巧执行固定的函数操作的一组重要的管道阶段之间的接口。 许多这些固定的函数操作可以通过软件开发人员进行调整。

光栅器始终确定输入的位置在剪贴空间内提供、 执行剪切和角度来看除，然后应用视区缩放和偏移量。

Direct3D 运行时调用以下的驱动程序函数，来创建、 设置，并销毁光栅化程序的状态：

[**CalcPrivateRasterizerStateSize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_calcprivaterasterizerstatesize)

[**CreateRasterizerState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createrasterizerstate)

[**DestroyRasterizerState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_destroyrasterizerstate)

[**SetRasterizerState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_setrasterizerstate)

[**SetScissorRects**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_setscissorrects)

[**SetViewports**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_setviewports)

 

 





