---
title: 几何着色器阶段
description: 几何着色器阶段
ms.assetid: 390eb917-3289-4b6e-be23-8db24cdd2bd7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7b1336682c1644ed9d5e7760c0bc8ade4970aa2e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839681"
---
# <a name="geometry-shader-stage"></a>几何着色器阶段


几何着色器（GS）阶段以顶点作为输入来运行应用程序指定的着色器代码，并在输出时生成顶点。 与在单个顶点上操作的顶点着色器不同，几何图形着色器的输入是完整基元的顶点（即线条的两个顶点、三角形的三个顶点或一个点的单个顶点）加上边缘的顶点数据基元（即线条的其他两个顶点或三角形的附加三个顶点）。 下图显示了为几何图形着色器输入的基元示例。

![阐释几何着色器基元的关系图](images/geoshade.png)

几何着色器的另一输入是由输入汇编程序（IA）自动生成的基元 ID。 基元 ID 允许几何图形着色器提取或计算每个面部的数据（如果需要）。

"几何着色器" 阶段可以输出多个顶点以形成单个选定的拓扑。 可用的 GS 输出拓扑为*tristrip*、 *linestrip*和*pointlist*。 几何着色器发出的基元数可能会有所不同，但几何着色器可以发出的最大顶点数必须以静态方式声明。 几何着色器发出的条带长度可以是任意的（"**剪切**" 命令）。

可以将几何图形着色器的输出发送到光栅器和内存中的顶点缓冲区。 发送到内存的输出将被扩展到各个点、行和三角列表（类似于输出传递到光栅化程序的方式）。

几何着色器阶段可以实现以下算法：

-   点 Sprite 分割：着色器采用单个顶点，并生成四个顶点（两个输出三角形），这四个顶点使用任意 texcoords、法线和其他属性表示四个四个角。

-   宽直线分割：着色器接收两个直线顶点（LV0 和 LV1），并为表示加宽线条的四个四个顶点生成四个顶点。 此外，几何图形着色器还可以使用相邻的直线顶点（AV0 和 AV1）对行端点执行 mitering。

-   毛皮/翼代：呈现可能有不同纹理（延伸表面）的多个偏移量，以模拟毛皮的 parallactic 效果。 翼形是拉伸边缘，如果角度不是倾斜的，通常会淡出。 翼用于使对象在倾斜角度更好地显示。

-   卷影生成：用于确定是否凸出的邻接信息。

-   向多个纹理多维数据集面部的单次传递渲染：会将基元投影并发送到像素着色器六次。 每个基元都带有呈现目标数组索引，用于选择多维数据集。

-   将 barycentric 坐标设置为基元数据，以便像素着色器可以执行自定义属性内插。

-   一种反常的情况：应用程序将生成一些几何，然后使用 n 修补该几何，然后将卷影卷从该几何中 extrudes。 对于这种情况，多步是解决方案，它能够将顶点和基元数据输出到流，并对数据进行重新循环。

**请注意**   因为对几何图形着色器的每次调用都会产生不同的输出数，所以，在此阶段对硬件的并行调用比并行运行其他管道阶段（例如顶点或像素着色器阶段）更难。 尽管硬件实现会并行运行几何图形着色器调用，但完成并行几何图形着色器调用所需的复杂缓冲意味着应用程序不应要求在几何图形着色器中可实现的并行度阶段与其他管道阶段一样多。 换句话说，几何图形着色器可能会成为管道中的瓶颈，具体取决于几何图形着色器具有的程序负载。 不过，其目标是，使用几何着色器功能的算法的运行效率仍比必须在无法以编程方式生成几何的硬件上模拟行为的应用程序更有效。

 

Direct3D 运行时调用以下驱动程序函数来创建、设置和销毁几何图形着色器：

[**CalcPrivateGeometryShaderWithStreamOutput**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_calcprivategeometryshaderwithstreamoutput)

[**CalcPrivateShaderSize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_calcprivateshadersize)

[**CreateGeometryShader**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_creategeometryshader)

[**CreateGeometryShaderWithStreamOutput**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_creategeometryshaderwithstreamoutput)

[**DestroyShader**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_destroyshader)

[**GsSetConstantBuffers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_setconstantbuffers)

[**GsSetSamplers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_setsamplers)

[**GsSetShader**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_setshader)

[**GsSetShaderResources**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_setshaderresources)

 

 





