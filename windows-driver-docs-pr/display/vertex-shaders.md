---
title: 顶点着色器
description: 顶点着色器
ms.assetid: dfc421f7-b2fe-4023-a47b-cfd59fe5bdb4
keywords:
- 顶点着色器 WDK DirectX 8.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a178533248397eb06a2f3c6d6de62ed76710fffc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63387422"
---
# <a name="vertex-shaders"></a>顶点着色器


## <span id="ddk_vertex_shaders_gg"></span><span id="DDK_VERTEX_SHADERS_GG"></span>


支持 DirectX 8.0 DDI 的所有驱动程序必须支持新的 DP2 令牌 D3DDP2OP\_SETVERTEXSHADER 即使可编程顶点着色器不支持硬件中。 这是因为 D3DDP2OP\_SETVERTEXSHADER 是依据传入的顶点数据 FVF 代码会传送到该驱动程序时使用 fixed 的函数和可编程顶点处理的机制。

D3DDP2OP\_SETVERTEXSHADER 可用于通知的当前可编程顶点着色器使用任一句柄或固定的函数顶点处理的顶点数据 FVF 代码的驱动程序。 顶点着色器的句柄空间由运行时，包含有效 FVF 代码。 因此，顶点着色器句柄可以引用以前通过 D3DDP2OP 创建可编程的顶点着色器句柄到\_CREATEVERTEXSHADER DP2 令牌，或对某个顶点的 FVF 代码处理固定的函数顶点处理的格式。

不支持可编程顶点处理的硬件的驱动程序应处理 D3DDP2OP\_SETVERTEXSHADER 来确定 FVF 代码 (并因此将执行的处理) 的顶点数据绑定到流零。 处理用户内存 (UM) 基元时，这一点尤其重要。 在这种情况下，确定提供的顶点数据 FVF 代码的唯一方法是通过 D3DDP2OP\_SETVERTEXSHADER 令牌。 如果句柄的最低有效位设置 (1)，该句柄是顶点着色器处理程序。 如果最低有效位为清除 (0)，则该句柄是旧的 FVF 代码。

如果某个顶点的 FVF 代码与指定的 D3DDP2OP 缓冲冲突\_SETVERTEXSHADER 驱动程序应忽略的顶点缓冲区 FVF 代码并继续。

DirectX 运行时可保证只 FVF 代码作为顶点着色器句柄传递给不支持可编程顶点处理的驱动程序。 但是，此类驱动程序应具有调试代码，以验证传递的 FVF 代码受支持。

 

 





