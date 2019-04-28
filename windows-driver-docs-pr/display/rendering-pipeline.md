---
title: 渲染管道
description: 渲染管道
ms.assetid: 63672d6e-5c5d-4873-a104-991e0b17d128
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c6245eb3154b6688c298a5a46dd1fa1e0d54d7d0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63350252"
---
# <a name="rendering-pipeline"></a>渲染管道


支持 Direct3D 版本 10 的图形硬件可以设计为具有共享可编程的着色器内核。 图形处理单元 (GPU) 可以编程可以安排跨组成呈现管道的功能块的着色器内核。 此负载平衡意味着硬件开发人员不需要使用每个着色器类型，但仅执行呈现所需的那些。 此负载平衡随后可以释放处于活动状态的着色器类型的资源。 下图显示了呈现管道的功能块。 以下各节图介绍了更多详细信息中的块。

![说明呈现管道的功能块的关系图](images/pipeline.png)

### <a name="span-idinputassemblerspanspan-idinputassemblerspan-input-assembler"></a><span id="input_assembler"></span><span id="INPUT_ASSEMBLER"></span> 输入装配器

[输入装配器](input-assembler-stage.md)阶段使用 fixed 的函数操作来读取内存不足的顶点。 然后，输入装配器窗体几何基元，并创建工作项的管道。 自动生成的顶点标识符、 实例标识符 （可向顶点着色器） 和基元标识符 （供几何着色器或像素着色器） 启用特定于标识符的处理。 点线图中显示特定于标识符的处理的流程。

### <a name="span-idvertexshaderspanspan-idvertexshaderspan-vertex-shader"></a><span id="vertex_shader"></span><span id="VERTEX_SHADER"></span> 顶点着色器

[顶点着色器](vertex-shader-stage.md)阶段作为输入的一个顶点，然后输出一个顶点。

### <a name="span-idgeometryshaderspanspan-idgeometryshaderspan-geometry-shader"></a><span id="geometry_shader"></span><span id="GEOMETRY_SHADER"></span> 几何着色器

[几何着色器](geometry-shader-stage.md)阶段一个基元作为输入，然后输出零行、 一行或多个基元。 输出基元可包含比没有几何着色器的更多数据。 每个操作的输出数据的总量是 （顶点大小 x 顶点计数）。

### <a name="span-idstreamoutputspanspan-idstreamoutputspan-stream-output"></a><span id="stream_output"></span><span id="STREAM_OUTPUT"></span> Stream 输出

[流式处理输出](stream-output-stage.md)阶段连接到达几何着色器向输出缓冲区的输出 （流出） 基元。 流输出与几何着色器关联，两者一起进行编程。

### <a name="span-idrasterizerspanspan-idrasterizerspan-rasterizer"></a><span id="rasterizer"></span><span id="RASTERIZER"></span> 光栅器

[光栅器](rasterizer-block.md)阶段 （包括自定义剪辑边界） 的剪辑基元、 基元上执行角度来看除、 实现视区和剪刀选择、 执行呈现器目标选择和执行基元的安装程序.

### <a name="span-idpixelshaderspanspan-idpixelshaderspan-pixel-shader"></a><span id="pixel_shader"></span><span id="PIXEL_SHADER"></span> 像素着色器

[像素着色器](pixel-shader-stage.md)阶段采用一个像素作为输入并输出一个像素中的相同位置或任何像素。 像素着色器无法读取当前呈现器目标。

### <a name="span-idoutputmergerspanspan-idoutputmergerspan-output-merger"></a><span id="output_merger"></span><span id="OUTPUT_MERGER"></span> 输出合并器

[输出合并器](output-merger-stage.md)阶段执行固定的函数呈现器目标混合，深度和模具操作。

 

 





