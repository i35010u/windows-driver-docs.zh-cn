---
title: 顶点混合
description: 顶点混合
ms.assetid: 58e740fb-01e4-4c8c-8e44-f0c358fd621a
keywords:
- 贷款 WDK Direct3D
- 混合 WDK Direct3D 的顶点
- Direct3D WDK Windows 2000 显示顶点值混合处理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2cb2073616de6260f2a715c36739b5371958d31a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390757"
---
# <a name="vertex-blending"></a>顶点混合


## <span id="ddk_vertex_blending_gg"></span><span id="DDK_VERTEX_BLENDING_GG"></span>


支持顶点混合操作的最新的直接 X 版本。 顶点混合在这种方式工作： 从建模空间对象乘以 4 X 4 世界矩阵，该全局空间相对于原点特定的世界空间中放置该模型的源。 矩阵的一个部分的作用方向和另一个部分的作用的位置。 可以有最多三个世界矩阵应用，允许对象来将"弯曲"通过的对象的范围内混合使用不同的权重的顶点。

接下来，应用视图矩阵，其中有效地压缩空间中的相对于特定视点中;呈现到二维图片上的实际非常类似于照相机。

 

 





