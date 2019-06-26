---
title: 处理着色器代码
description: 处理着色器代码
ms.assetid: c858766c-b414-4971-b4d9-23ec94aca8ea
keywords:
- 用户模式显示驱动程序 WDK Windows Vista 中，着色器代码
- 着色器代码 WDK 显示
- 像素着色器代码 WDK 显示
- 顶点着色器代码 WDK 显示
- 顶点声明 WDK 显示
- 令牌 WDK 显示
- 最终令牌 WDK 显示
- 显示声明 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c0a80ce97f20035781860b4b62d82958a672a0a9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363714"
---
# <a name="processing-shader-codes"></a>处理着色器代码


用户模式下向程序着色器组装器显示驱动程序使用顶点声明，以及在每个单个像素和顶点着色器代码的令牌。

当 Microsoft Direct3D 运行时调用的驱动程序时，用户模式显示驱动程序收到顶点和像素着色器代码[ **CreateVertexShaderFunc** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_createvertexshaderfunc)并[ **CreatePixelShader** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_createpixelshader)函数。 用户模式显示驱动程序时运行时调用的驱动程序收到顶点声明[ **CreateVertexShaderDecl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_createvertexshaderdecl)函数。 顶点声明包含的数组[ **D3DDDIVERTEXELEMENT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddivertexelement)结构。 用户模式显示驱动程序将着色器代码和顶点着色器声明转换为特定于硬件的格式并将着色器代码和声明与着色器和声明句柄相关联。 运行时对的调用中使用创建句柄[ **SetVertexShaderDecl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_setvertexshaderdecl)， [ **SetVertexShaderFunc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_setvertexshaderfunc)，和[**SetPixelShader** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_setpixelshader)函数来设置顶点着色器声明和顶点和像素着色器，以便所有后续的绘图操作使用它们。

一个单独的着色器代码和构成每个着色器代码的令牌格式的详细信息，请参阅[Direct3D 着色器代码](https://docs.microsoft.com/windows-hardware/drivers/display/direct3d-shader-codes)。

**请注意**  着色器代码和每个声明时应用程序创建顶点着色器中，像素着色器和顶点声明，以结束[结束令牌](https://docs.microsoft.com/windows-hardware/drivers/display/end-token)。 在 Direct3D 运行时，反过来，通过顶点，并且为用户模式的像素着色器创建请求显示请求附带的驱动程序、 顶点和像素着色器代码结尾结束标记。 但是，在运行时通过顶点声明创建请求，伴随请求的顶点声明不以结尾结束标记。

 

 

 





