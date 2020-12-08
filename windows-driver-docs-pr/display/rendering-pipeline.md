---
title: 渲染管道
description: 渲染管道
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 60bd786229c9c86777b572c132ef1ed53a652bb4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96783991"
---
# <a name="rendering-pipeline"></a>渲染管道


支持 Direct3D 版本10的图形硬件可以通过共享的可编程着色器核心来设计。 图形处理单元 (GPU) 可以对可在构成渲染管道的各个功能块之间计划的着色器内核进行编程。 此负载平衡意味着硬件开发人员无需使用每个着色器类型，只是执行渲染所需的类型。 然后，此负载平衡可以释放处于活动状态的着色器类型的资源。 下图显示了呈现管道的功能块。 该图后面的部分将更详细地描述这些块。

![阐释呈现管道的功能块的关系图](images/pipeline.png)

### <a name="span-idinput_assemblerspanspan-idinput_assemblerspan-input-assembler"></a><span id="input_assembler"></span><span id="INPUT_ASSEMBLER"></span> 输入组装器

" [输入装配](input-assembler-stage.md) 器" 阶段使用固定的函数操作从内存中读取顶点。 然后，输入汇编会形成几何基元，并创建管道工作项。 自动生成的顶点标识符、实例标识符 (可用于顶点着色器) ， (几何着色器或像素着色器可用的基元标识符) 启用特定于标识符的处理。 图中的虚线显示特定于标识符的处理流程。

### <a name="span-idvertex_shaderspanspan-idvertex_shaderspan-vertex-shader"></a><span id="vertex_shader"></span><span id="VERTEX_SHADER"></span> 顶点着色器

[顶点着色器](vertex-shader-stage.md)阶段使用一个顶点作为输入，并输出一个顶点。

### <a name="span-idgeometry_shaderspanspan-idgeometry_shaderspan-geometry-shader"></a><span id="geometry_shader"></span><span id="GEOMETRY_SHADER"></span> 几何着色器

[几何着色器](geometry-shader-stage.md)阶段使用一个基元作为输入，输出零个、一个或多个基元。 输出基元包含的数据可能会超出几何着色器的可能数量。 每个操作的输出数据总量 (顶点大小 x 顶点计数) 。

### <a name="span-idstream_outputspanspan-idstream_outputspan-stream-output"></a><span id="stream_output"></span><span id="STREAM_OUTPUT"></span> 流输出

[流输出](stream-output-stage.md)阶段将) 基元 (流连接起来，从而将几何图形着色器的输出传递到输出缓冲区。 流输出与几何图形着色器相关联，并且两者同时进行了编程。

### <a name="span-idrasterizerspanspan-idrasterizerspan-rasterizer"></a><span id="rasterizer"></span><span id="RASTERIZER"></span> 光栅器

[光栅](rasterizer-block.md)器阶段剪辑 (包括自定义剪辑边界) 基元，对基元执行透视划分，实现视区和剪选，执行呈现目标选择，并执行基元设置。

### <a name="span-idpixel_shaderspanspan-idpixel_shaderspan-pixel-shader"></a><span id="pixel_shader"></span><span id="PIXEL_SHADER"></span> 像素着色器

" [像素着色器](pixel-shader-stage.md) " 阶段使用一个像素作为输入，并输出同一位置上的一个像素或无像素。 像素着色器无法读取当前渲染器目标。

### <a name="span-idoutput_mergerspanspan-idoutput_mergerspan-output-merger"></a><span id="output_merger"></span><span id="OUTPUT_MERGER"></span> 输出合并

[输出合并](output-merger-stage.md)阶段执行固定的函数呈现-目标混合、深度和模具操作。

 

 





