---
title: 几何着色器阶段
description: 几何着色器阶段
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: da51ce033d88d30bf13feaef6b7229f1cc7a1e22
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96832415"
---
# <a name="geometry-shader-stage"></a>几何着色器阶段


 (GS) 阶段的几何着色器运行应用程序指定的着色器代码，并将顶点作为输入，并且可以在输出时生成顶点。 与在单个顶点上操作的顶点着色器不同，几何图形着色器的输入是一种完整的基元 (顶点，两个顶点用于三角形，三个顶点表示三角形，另一个顶点用于一个点) 再加上一个顶点的顶点数据 (也就是说，另外两个顶点用于直线，另外三个顶点用于三角形的) 。 下图显示了为几何图形着色器输入的基元示例。

![阐释几何着色器基元的关系图](images/geoshade.png)

几何着色器的另一输入是由输入汇编 (IA) 自动生成的基元 ID。 基元 ID 允许几何图形着色器提取或计算每个面部的数据（如果需要）。

"几何着色器" 阶段可以输出多个顶点以形成单个选定的拓扑。 可用的 GS 输出拓扑为 *tristrip*、 *linestrip* 和 *pointlist*。 几何着色器发出的基元数可能会有所不同，但几何着色器可以发出的最大顶点数必须以静态方式声明。 几何着色器发出的条带长度可以是任意 (有一个) **剪切** 的命令。

可以将几何图形着色器的输出发送到光栅器和内存中的顶点缓冲区。 发送到内存的输出将展开为单独的点、直线和三角形列表， (类似于输出传递到光栅化程序) 的方式。

几何着色器阶段可以实现以下算法：

-   点 Sprite 分割：着色器采用单个顶点并生成四个顶点 (两个输出三角形) ，这些三角形表示四个带任意 texcoords、法线和其他属性的四个角。

-   宽直线分割：着色器接收两个行顶点 (LV0 和 LV1) ，并为表示加宽线条的四颗四个顶点生成四个顶点。 此外，几何着色器还可以使用相邻的直线顶点 (AV0 和 AV1) 在行端点上执行 mitering。

-   毛皮/翼代：呈现多个偏移量可能有不同纹理 (延伸面) 来模拟毛皮的 parallactic 效果。 翼形是拉伸边缘，如果角度不是倾斜的，通常会淡出。 翼用于使对象在倾斜角度更好地显示。

-   卷影生成：用于确定是否凸出的邻接信息。

-   向多个纹理多维数据集面部的单次传递渲染：会将基元投影并发送到像素着色器六次。 每个基元都带有呈现目标数组索引，用于选择多维数据集。

-   将 barycentric 坐标设置为基元数据，以便像素着色器可以执行自定义属性内插。

-   一种反常的情况：应用程序将生成一些几何，然后使用 n 修补该几何，然后将卷影卷从该几何中 extrudes。 对于这种情况，多步是解决方案，它能够将顶点和基元数据输出到流，并对数据进行重新循环。

**注意**   由于对几何图形着色器的每个调用都可能产生不同的输出数，因此，在此阶段对硬件的并行调用比运行其他管道阶段 (如并行) 顶点或像素着色器阶段时更难。 尽管硬件实现会并行运行几何图形着色器调用，但完成并行几何图形着色器调用所需的复杂缓冲意味着应用程序不应要求在几何着色器阶段可实现的并行度与其他管道阶段一样多。 换句话说，几何图形着色器可能会成为管道中的瓶颈，具体取决于几何图形着色器具有的程序负载。 不过，其目标是，使用几何着色器功能的算法的运行效率仍比必须在无法以编程方式生成几何的硬件上模拟行为的应用程序更有效。

 

Direct3D 运行时调用以下驱动程序函数来创建、设置和销毁几何图形着色器：

[**CalcPrivateGeometryShaderWithStreamOutput**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_calcprivategeometryshaderwithstreamoutput)

[**CalcPrivateShaderSize**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_calcprivateshadersize)

[**CreateGeometryShader**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_creategeometryshader)

[**CreateGeometryShaderWithStreamOutput**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_creategeometryshaderwithstreamoutput)

[**DestroyShader**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_destroyshader)

[**GsSetConstantBuffers**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_setconstantbuffers)

[**GsSetSamplers**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_setsamplers)

[**GsSetShader**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_setshader)

[**GsSetShaderResources**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_setshaderresources)

 

