---
title: 纹理阶段
description: 纹理阶段
keywords:
- 多纹理 WDK Direct3D，纹理阶段
- 纹理阶段 WDK Direct3D
- 纹理管理 WDK Direct3D，阶段
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: df635def1a85ef782dd24aed6d0de7a2f28f169b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96801875"
---
# <a name="texture-stages"></a>纹理阶段


## <span id="ddk_texture_stages_gg"></span><span id="DDK_TEXTURE_STAGES_GG"></span>


纹理阶段指示纹理管道中纹理的位置。 具有最高非空纹理的位置与帧缓冲区最接近。 每个阶段都是一个纹理混合单元，它执行用于将关联纹理组合到多边形上的操作，如下图所示。

![阐释单个纹理阶段的关系图](images/d3dfig36.png)

当前纹理进入舞台，并与另一个纹理混合，并将结果传递到纹理管道中的下一阶段，如果这是最后一个阶段) ，则会将结果传递到纹理 (管道中的下一个阶段。

有8个纹理阶段，编号为0到7，零从帧缓冲区最远，并对应于 D3DRENDERSTATE \_ TEXTUREHANDLE （在 DIRECTX SDK 文档中介绍）。 驱动程序必须处理最多八个纹理坐标，即使硬件不支持这很多。

在多个纹理呈现中，编号较低的纹理阶段远远离帧缓冲区。 向上选取并筛选级联的最小纹理阶段，以获取 *纹素* 或纹理元素。 混合操作发生在该纹素和下一操作之间，因为它将纹理管道向下沿帧缓冲区向下进行级联。

例如，如果两个纹理 Texture0 和纹理1混合在一起，则生成的纹素将进入光栅化管道，就像单个纹理使用旧版纹理一样。 有三种纹理，Texture0 与纹理1混合。 然后，将根据某些可编程权重将生成的纹素与 Texture2 混合。 这意味着 Texture0 不能直接影响 Texture2;它只能与纹理1混合使用，如下图所示。

![阐释三阶段纹理管道的关系图](images/d3dfig35.png)

每个纹理阶段都在管道中引入了一个纹理。 像素管道是独立的，并且会在多个纹理操作之后发生。 这可能包括雾化应用程序或帧缓冲区 alpha 混合。

 

 





