---
title: Direct3D 着色器代码
description: Direct3D 着色器代码
ms.assetid: 30d14bbe-10fe-46fc-99b3-ab2f989abb29
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 4dfb86c7b4a6547116f4a4df2a8013b75448279f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358005"
---
# <a name="direct3d-shader-codes"></a>Direct3D 着色器代码


像素着色器代码如下所示 D3DHAL\_DP2CREATEPIXELSHADER 命令流中的结构。 顶点着色器代码适用于 DirectX 8.1 及更早版本，如下所示 D3DHAL\_DP2CREATEVERTEXSHADER 结构。 顶点着色器代码 DirectX 9.0 和更高版本，如下所示 D3DHAL\_DP2CREATEVERTEXSHADERFUNC 结构。 运行时在调用驱动程序的 D3dDrawPrimitives2 函数创建像素或顶点着色器。 若要创建像素着色器，则运行时调用与 D3DDP2OP D3dDrawPrimitives2\_CREATEPIXELSHADER 操作代码。 若要创建顶点着色器在 DirectX 8.1 及更早版本，运行时调用与 D3DDP2OP D3dDrawPrimitives2\_CREATEVERTEXSHADER 操作代码。 若要创建顶点着色器在 DirectX 9.0 和更高版本，运行时调用与 D3DDP2OP D3dDrawPrimitives2\_CREATEVERTEXSHADERFUNC 操作代码。

本部分介绍各个着色器代码和构成每个着色器代码的令牌的格式。

[着色器代码格式](shader-code-format.md)

[着色器代码令牌](shader-code-tokens.md)

[着色器操作代码](https://msdn.microsoft.com/library/windows/hardware/ff569706)

[着色器寄存器类型](https://msdn.microsoft.com/library/windows/hardware/ff569707)

[着色器相对寻址](shader-relative-addressing.md)

 

 





