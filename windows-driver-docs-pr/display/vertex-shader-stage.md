---
title: 顶点着色器阶段
description: 顶点着色器阶段
ms.assetid: 310ef24a-7647-4f5e-b89f-a3ff330d5df4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d99fc1c973861cc9268926422a68bf01fa714b0f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829201"
---
# <a name="vertex-shader-stage"></a>顶点着色器阶段


顶点着色器阶段通过执行转换、外观和照明等操作来处理顶点。 顶点着色器始终在单个输入顶点上运行并生成单个输出顶点。 呈现管道的这一阶段必须始终处于活动状态。

Direct3D 运行时调用以下驱动程序函数来创建、设置和销毁顶点着色器：

[**CalcPrivateShaderSize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_calcprivateshadersize)

[**CreateVertexShader （D3D10）** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createvertexshader)

[**DestroyShader**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_destroyshader)

[**VsSetConstantBuffers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_setconstantbuffers)

[**VsSetSamplers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_setsamplers)

[**VsSetShader**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_setshader)

[**VsSetShaderResources**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_setshaderresources)

 

 





