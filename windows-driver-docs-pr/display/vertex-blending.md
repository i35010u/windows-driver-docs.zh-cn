---
title: 顶点混合
description: 顶点混合
keywords:
- 借贷 WDK Direct3D
- 顶点混合 WDK Direct3D
- Direct3D WDK Windows 2000 显示，顶点混合
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1ba760d6aca51b4374f262174f9d42af4a7eab33
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96798233"
---
# <a name="vertex-blending"></a>顶点混合


## <span id="ddk_vertex_blending_gg"></span><span id="DDK_VERTEX_BLENDING_GG"></span>


最新的直接 X 版本支持顶点混合操作。 顶点混合的工作方式如下：建模空间中的对象乘以4X4 世界矩阵，并将模型的原点置于相对于该世界空间原点的特定世界空间。 矩阵的一部分是方向，另一部分则是位置。 最多可应用三个世界矩阵，允许对象通过将顶点与对象范围内的不同权重混合为 "弯曲"。

接下来，将应用视图矩阵，这会有效地压缩相对于特定视点的空间;与相机非常类似于将现实世界呈现为二维图片。

 

 





