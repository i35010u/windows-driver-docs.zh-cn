---
title: 顶点着色器阶段
description: 顶点着色器阶段
ms.assetid: 310ef24a-7647-4f5e-b89f-a3ff330d5df4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 190afa763f1aca1fb88fd3a3d3c7cb44a6f88cc1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567750"
---
# <a name="vertex-shader-stage"></a>顶点着色器阶段


顶点着色器阶段的执行操作，例如转换、 外观设置和照明处理顶点。 顶点着色器始终在单个输入顶点上运行并生成单个输出顶点。 此阶段呈现管道必须始终处于活动状态。

Direct3D 运行时调用以下的驱动程序函数，来创建、 设置，并销毁顶点着色器：

[**CalcPrivateShaderSize**](https://msdn.microsoft.com/library/windows/hardware/ff538315)

[**CreateVertexShader(D3D10)**](https://msdn.microsoft.com/library/windows/hardware/ff540720)

[**DestroyShader**](https://msdn.microsoft.com/library/windows/hardware/ff552805)

[**VsSetConstantBuffers**](https://msdn.microsoft.com/library/windows/hardware/ff570573)

[**VsSetSamplers**](https://msdn.microsoft.com/library/windows/hardware/ff570574)

[**VsSetShader**](https://msdn.microsoft.com/library/windows/hardware/ff570575)

[**VsSetShaderResources**](https://msdn.microsoft.com/library/windows/hardware/ff570576)

 

 





