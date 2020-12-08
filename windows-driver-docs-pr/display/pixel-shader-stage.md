---
title: 像素着色器阶段
description: 像素着色器阶段
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 356a39d51bdd2db4861bb0372ee13490df9c52c9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838047"
---
# <a name="pixel-shader-stage"></a>像素着色器阶段


可用于 "像素着色器" 阶段的输入数据包括可以在每个元素的基础上选择的顶点属性，使其可以包含或不带透视更正，或视为每个基元的常量。

输出是当前像素位置的输出数据的一个或多个向量，如果该像素被丢弃) ，则不 (颜色。

Direct3D 运行时调用以下驱动程序函数来创建、设置和销毁像素着色器：

[**CalcPrivateShaderSize**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_calcprivateshadersize)

[**CreatePixelShader (D3D10)**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createpixelshader)

[**DestroyShader**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_destroyshader)

[**PsSetConstantBuffers**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_setconstantbuffers)

[**PsSetSamplers**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_setsamplers)

[**PsSetShader**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_setshader)

[**PsSetShaderResources**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_setshaderresources)

 

