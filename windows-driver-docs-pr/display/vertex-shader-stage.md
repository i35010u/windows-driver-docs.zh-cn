---
title: 顶点着色器阶段
description: 顶点着色器阶段
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f7c61815115ce5d23c762ba698e3ba75ec452c8f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96825177"
---
# <a name="vertex-shader-stage"></a>顶点着色器阶段


顶点着色器阶段通过执行转换、外观和照明等操作来处理顶点。 顶点着色器始终在单个输入顶点上运行并生成单个输出顶点。 呈现管道的这一阶段必须始终处于活动状态。

Direct3D 运行时调用以下驱动程序函数来创建、设置和销毁顶点着色器：

[**CalcPrivateShaderSize**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_calcprivateshadersize)

[**CreateVertexShader (D3D10)**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createvertexshader)

[**DestroyShader**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_destroyshader)

[**VsSetConstantBuffers**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_setconstantbuffers)

[**VsSetSamplers**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_setsamplers)

[**VsSetShader**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_setshader)

[**VsSetShaderResources**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_setshaderresources)

 

