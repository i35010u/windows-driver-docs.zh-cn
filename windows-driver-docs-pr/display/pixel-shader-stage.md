---
title: 像素着色器阶段
description: 像素着色器阶段
ms.assetid: 969b6cb9-7b03-4c9f-bf4a-e8d9b442c847
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7ec1c0e0bdda7e7a246b332bf2075af41caf72b9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523247"
---
# <a name="pixel-shader-stage"></a>像素着色器阶段


可供在像素着色器阶段的输入的数据包含属性，可以选择，对于每个元素，以使用或不透视校正内, 插或被视为常量的每个基元的顶点。

输出是一个或多个的 4 向量的输出数据的当前像素位置或没有颜色 （如果放弃像素）。

Direct3D 运行时调用以下的驱动程序函数，来创建、 设置，并销毁像素着色器：

[**CalcPrivateShaderSize**](https://msdn.microsoft.com/library/windows/hardware/ff538315)

[**CreatePixelShader(D3D10)**](https://msdn.microsoft.com/library/windows/hardware/ff540670)

[**DestroyShader**](https://msdn.microsoft.com/library/windows/hardware/ff552805)

[**PsSetConstantBuffers**](https://msdn.microsoft.com/library/windows/hardware/ff569207)

[**PsSetSamplers**](https://msdn.microsoft.com/library/windows/hardware/ff569208)

[**PsSetShader**](https://msdn.microsoft.com/library/windows/hardware/ff569209)

[**PsSetShaderResources**](https://msdn.microsoft.com/library/windows/hardware/ff569210)

 

 





