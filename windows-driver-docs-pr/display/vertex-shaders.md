---
title: 顶点着色器
description: 顶点着色器
keywords:
- 顶点着色器 WDK DirectX 8。0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a353b62558a7aa7b2c6a99ed1d07481fb32591ac
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96825171"
---
# <a name="vertex-shaders"></a>顶点着色器


## <span id="ddk_vertex_shaders_gg"></span><span id="DDK_VERTEX_SHADERS_GG"></span>


支持 DirectX 8.0 DDI 的所有驱动程序都必须支持新的 DP2 令牌 D3DDP2OP \_ SETVERTEXSHADER，即使硬件中不支持可编程顶点着色器。 这是因为，D3DDP2OP \_ SETVERTEXSHADER 是在使用 fixed 函数和可编程顶点处理时，将传入顶点数据的 FVF 代码传达给驱动程序的机制。

\_可以使用 D3DDP2OP SETVERTEXSHADER 通知当前可编程顶点着色器的句柄要使用的驱动程序或用于固定函数顶点处理的顶点数据的 FVF 代码。 顶点着色器的句柄空间由运行时管理并包含有效的 FVF 代码。 因此，顶点着色器控点可以引用先前通过 D3DDP2OP CREATEVERTEXSHADER DP2 标记创建的可编程顶点着色器图柄 \_ ，或引用由固定函数顶点处理处理的顶点格式的 FVF 代码。

不支持可编程顶点处理的硬件的驱动程序应处理 D3DDP2OP \_ SETVERTEXSHADER 以确定 FVF (代码，从而对绑定到流零的顶点数据) 执行处理。 当处理 (UM) 基元的用户内存时，这一点特别重要。 在这种情况下，确定所提供的顶点数据的 FVF 代码的唯一方法是通过 D3DDP2OP \_ SETVERTEXSHADER 标记。 如果句柄的最小有效位设置 (1) ，则句柄为顶点着色器处理程序。 如果) 的最小有效位为明文 (0，则句柄为旧的 FVF 代码。

如果顶点缓冲区的 FVF 代码与 D3DDP2OP SETVERTEXSHADER 指定的代码冲突， \_ 则驱动程序应忽略顶点缓冲区的 FVF 代码，然后继续。

DirectX 运行时保证仅将 FVF 代码作为顶点着色器句柄传递到不支持可编程顶点处理的驱动程序。 但是，此类驱动程序应包含调试代码，以验证是否支持传递的 FVF 代码。

 

 





