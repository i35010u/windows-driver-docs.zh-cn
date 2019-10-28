---
title: Direct3D 着色器代码
description: Direct3D 着色器代码
ms.assetid: 30d14bbe-10fe-46fc-99b3-ab2f989abb29
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: c04e6c11064fd6b4d8cbfd5461624b54cbc6b390
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839006"
---
# <a name="direct3d-shader-codes"></a>Direct3D 着色器代码


像素着色器代码遵循命令流中的 D3DHAL\_DP2CREATEPIXELSHADER 结构。 对于 DirectX 8.1 及更早版本，顶点着色器代码遵循 D3DHAL\_DP2CREATEVERTEXSHADER 结构。 对于 DirectX 9.0 和更高版本，顶点着色器代码遵循 D3DHAL\_DP2CREATEVERTEXSHADERFUNC 结构。 运行时在调用驱动程序的 D3dDrawPrimitives2 函数时，将创建像素或顶点着色器。 若要创建像素着色器，运行时将使用 D3DDP2OP\_CREATEPIXELSHADER 操作代码调用 D3dDrawPrimitives2。 若要在 DirectX 8.1 和更早版本中创建顶点着色器，运行时将使用 D3DDP2OP\_CREATEVERTEXSHADER 操作代码调用 D3dDrawPrimitives2。 若要在 DirectX 9.0 和更高版本中创建顶点着色器，运行时将使用 D3DDP2OP\_CREATEVERTEXSHADERFUNC 操作代码调用 D3dDrawPrimitives2。

本节介绍单个着色器代码的格式和组成每个着色器代码的标记。

[着色器代码格式](shader-code-format.md)

[着色器代码标记](shader-code-tokens.md)

[着色器操作代码](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d9types/ne-d3d9types-_d3dshader_instruction_opcode_type)

[着色器寄存器类型](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d9types/ne-d3d9types-_d3dshader_param_register_type)

[着色器相对寻址](shader-relative-addressing.md)

 

 





