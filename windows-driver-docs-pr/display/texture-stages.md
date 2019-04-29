---
title: 纹理阶段
description: 纹理阶段
ms.assetid: 98149615-ef64-4b0d-9adf-d6b72324e1b4
keywords:
- 多个纹理 WDK Direct3D，纹理阶段
- 纹理阶段 WDK Direct3D
- 纹理管理 WDK Direct3D，阶段
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 646d0bc618c5836d4ea062fb8c066e9a19815fea
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362626"
---
# <a name="texture-stages"></a>纹理阶段


## <span id="ddk_texture_stages_gg"></span><span id="DDK_TEXTURE_STAGES_GG"></span>


纹理阶段指示纹理管道中的纹理的位置。 与最高的非 NULL 纹理位置是最接近的帧缓冲区。 每个阶段是一种纹理，混合执行用于将合并到多边形、 相关的纹理，如下图中所示的操作的单元。

![说明单纹理阶段的关系图](images/d3dfig36.png)

当前的纹理进入阶段和向前传递给纹理管道 （或帧缓冲区，如果这是最后一个阶段） 中的下一阶段的结果与混合使用另一个纹理和漫射组件。

有八个纹理阶段，编号为 0 到 7，其中最远的地方帧缓冲区中，零为，而对应于呈现状态纹理处理 D3DRENDERSTATE\_TEXTUREHANDLE，DirectX SDK 文档中所述。 该驱动程序必须处理最多八个纹理坐标，即使在硬件不支持的很多。

在多个纹理呈现时，较低级别的纹理阶段是帧缓冲区距离较远。 提取并筛选，以获取级联中的最小纹理阶段*纹素*，或纹理元素。 混合操作之间发生的纹素和下一步为该操作将级联到帧缓冲区纹理管道向下。

例如，如果这两个纹理，Texture0 和纹理 1，混合在一起，生成的纹素进入光栅化管道就像单纹理会使用旧的纹理。 使用三个纹理 Texture0 获取与纹理 1 混合。 生成的纹素然后 Texture2 与混合根据某些可编程的权重。 这意味着 Texture0 不能直接调用影响 Texture2它可以仅实现通过与纹理 1，正在混合下图中所示。

![说明三阶段纹理管道的关系图](images/d3dfig35.png)

每个纹理阶段到管道中引入了一种纹理。 像素管道不同，多个纹理操作之后。 这可能包括雾应用程序或帧缓冲区 alpha 值混合处理。

 

 





