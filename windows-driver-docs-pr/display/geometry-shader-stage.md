---
title: 几何着色器阶段
description: 几何着色器阶段
ms.assetid: 390eb917-3289-4b6e-be23-8db24cdd2bd7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 066a47fbea947df7700cbd1990f714f30d032d7f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379981"
---
# <a name="geometry-shader-stage"></a>几何着色器阶段


几何着色 (GS) 与作为输入，并可以生成输出上的顶点的顶点运行应用程序指定着色器代码。 与顶点着色器，在单个顶点执行，不同，几何着色器的输入是一个完整的基元 （即，线、 三角形的三个顶点或单个顶点的点的两个顶点） 的顶点以及边缘相邻的顶点数据基元 （即，其他两个顶点的行） 或一个三角形其他三个顶点。 下图显示了示例输入基元几何着色器。

![关系图演示几何着色器基元](images/geoshade.png)

几何着色器的另一个输入是由输入装配器 (IA) 自动生成一个基元 ID。 如果需要，每个面的数据，基元 ID 允许到 fetch 或计算、 几何着色器。

几何着色器阶段可以输出以形成单个的选定的拓扑的多个顶点。 可用 GS 输出拓扑都*tristrip*， *linestrip*，并*pointlist*。 几何着色器发出的基元的数字也会有所不同，但必须以静态方式声明的可发出几何着色器的顶点的最大数量。 几何着色器发出的条带长度可以是任意 (没有**剪切**命令)。

可以将几何着色器的输出发送到光栅化程序和顶点缓冲区在内存中。 输出发送到内存扩展到行中，单个点和三角形列出 （类似于如何将输出传递给光栅化程序）。

几何着色器阶段可以实现以下算法：

-   点子画面分割：着色器在单个顶点中使用，并生成 （两个输出三角形） 的四个表示四任意 texcoords、 normals，与其他属性的四个角顶点。

-   加宽线分割：着色器接收两个行顶点 （LV0 和 LV1），并生成表示加宽的行四核的四个顶点。 此外，几何着色器可以使用相邻行顶点 （AV0 和 AV1） 来执行 mitering 行终结点上。

-   毛皮/Fin 生成：呈现可能具有不同的纹理 （延伸面） 来模拟毛皮 parallactic 效果的多个偏移量。 翼片是通常淡出，如果不倾斜角度的拉伸的边缘。 翼片用于使对象看起来更好地倾斜角度。

-   卷影卷生成：用于确定是否要拉伸的相邻信息。

-   单次传递到多个纹理多维数据集的人脸的呈现：基元是投影和发出到像素着色器六倍。 每个基元伴随呈现器目标数组索引，后者选择多维数据集文本。

-   将设置重心坐标为基元数据以便像素着色器可以执行自定义属性内插。

-   反常情况中：应用程序生成的几何图形的一些几何形状，然后 n 修补程序，然后拉伸超出该几何图形的卷影卷。 对于这种情况下，多通路是能够输出顶点和基元数据写入流，并使循环返回的数据解决方案。

**请注意**  几何着色器对每个调用会产生的输出数不同，因为对硬件的并行调用会更加困难在此阶段比时运行另一个管道阶段 （例如顶点或像素着色器阶段） 中并行。 中并行的复杂缓冲，完成应用程序不应要求在几何着色器可实现并行性级别的并行几何着色器调用方法所需的硬件实现将运行时调用几何着色器阶段是作为其他管道阶段得多。 换而言之，几何着色器可能会成为根据程序负载几何着色器具有管道中的瓶颈。 但是，目标是仍将比具有要模拟的行为不能以编程方式生成几何图形的硬件上的应用程序更有效地运行使用几何着色器的功能的算法。

 

Direct3D 运行时调用以下的驱动程序函数，来创建、 设置，并销毁几何着色器：

[**CalcPrivateGeometryShaderWithStreamOutput**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_calcprivategeometryshaderwithstreamoutput)

[**CalcPrivateShaderSize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_calcprivateshadersize)

[**CreateGeometryShader**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_creategeometryshader)

[**CreateGeometryShaderWithStreamOutput**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_creategeometryshaderwithstreamoutput)

[**DestroyShader**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_destroyshader)

[**GsSetConstantBuffers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_setconstantbuffers)

[**GsSetSamplers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_setsamplers)

[**GsSetShader**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_setshader)

[**GsSetShaderResources**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_setshaderresources)

 

 





