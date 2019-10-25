---
title: 处理着色器代码
description: 处理着色器代码
ms.assetid: c858766c-b414-4971-b4d9-23ec94aca8ea
keywords:
- 用户模式显示驱动程序 WDK Windows Vista，着色器代码
- 着色器代码 WDK 显示
- 象素着色器代码 WDK 显示
- 顶点着色器代码 WDK 显示
- 顶点声明 WDK 显示
- 令牌 WDK 显示
- 结束令牌 WDK 显示
- 声明 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3b18df81c9763f1a3ec21a78f4d03cea60276435
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829686"
---
# <a name="processing-shader-codes"></a>处理着色器代码


用户模式显示驱动程序使用顶点声明以及每个单独像素和顶点着色器代码中的标记来编程着色器组装器。

当 Microsoft Direct3D runtime 分别调用驱动程序的[**CreateVertexShaderFunc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createvertexshaderfunc)和[**CreatePixelShader**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createpixelshader)函数时，用户模式显示驱动程序将接收顶点和像素着色器代码。 当运行时调用驱动程序的[**CreateVertexShaderDecl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createvertexshaderdecl)函数时，用户模式显示驱动程序将接收顶点声明。 顶点声明包含[**D3DDDIVERTEXELEMENT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddivertexelement)结构的数组。 用户模式显示驱动程序将着色器代码和顶点着色器声明转换为特定于硬件的格式，并将着色器代码和声明与着色器和声明句柄相关联。 运行时在调用[**SetVertexShaderDecl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_setvertexshaderdecl)、 [**SetVertexShaderFunc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_setvertexshaderfunc)和[**SetPixelShader**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_setpixelshader)函数时使用创建的句柄来设置顶点着色器声明以及顶点和像素着色器，以便所有后续绘图操作使用它们。

有关各个着色器代码的格式和组成每个着色器代码的标记的详细信息，请参阅[Direct3D 着色器代码](https://docs.microsoft.com/windows-hardware/drivers/display/direct3d-shader-codes)。

**请注意**   当应用程序创建顶点着色器、像素着色器和顶点声明时，每个以[结束标记](https://docs.microsoft.com/windows-hardware/drivers/display/end-token)结尾的着色器代码和声明。 当 Direct3D 运行时依次将顶点和像素着色器创建请求传递给用户模式显示驱动程序时，请求附带的顶点着色器代码将以结束标记结束。 但是，当运行时传递顶点声明创建请求时，请求附带的顶点声明不会以结束标记结束。

 

 

 





