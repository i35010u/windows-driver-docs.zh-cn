---
title: 多个渲染器目标的必需功能
description: 多个渲染器目标的必需功能
ms.assetid: fa807bde-8c3b-4ba8-b899-cdcd0b8d2458
keywords:
- 呈现多个目标 WDK DirectX 9.0，必需的功能
- 多个呈现器目标 WDK DirectX 9.0 中，所需的功能
- 同时呈现器目标 WDK DirectX 9.0 中，所需的功能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 141c176389218f3efc798aa7f464c356213efd20
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383218"
---
# <a name="required-features-for-multiple-render-targets"></a>多个渲染器目标的必需功能


## <span id="ddk_required_features_for_multiple_render_targets_gg"></span><span id="DDK_REQUIRED_FEATURES_FOR_MULTIPLE_RENDER_TARGETS_GG"></span>


支持同时呈现到多个目标的 DirectX 9.0 版本驱动程序必须支持以下功能：

-   为给定的多个的所有曲面都呈现目标组以原子方式分配。 将此视为一种新型的图面格式有交错的多个 RGBA 通道可解决此限制。

-   支持仅 32 位图面上格式 （例如，RGBA8、 RGBA10、 U16V16 和 R32f 键入格式）。 通过新的图面上格式的名称来表示此限制。

-   多个的呈现器目标组不能为主要 （显示面）。 多个呈现器目标组必须仅为屏外。 通过 surface 格式枚举来表示此限制。

-   多个的呈现器目标组不能为 mipmap。 也就是说，MIP 链创建会失败。

-   多个的呈现器目标组的元素不能在同一时间为呈现器目标设置为纹理。 但是，组面上的不同元素可以同时为纹理，并呈现器目标。

-   支持多个的呈现器目标组未抗锯齿。

-   多个元素呈现目标组时使用，因为不能筛选的纹理。 也就是说，没有采样器状态可能会影响查找。

-   不能锁定的多个呈现器目标组的元素。

-   可以通过将每个元素分配给与典型的纹理相同的各个阶段同时，使用多个的呈现器目标组的多个元素。

-   多个元素呈现目标组支持 gamma 2.2 1.0 转换在读取时，就像其他纹理格式。

-   D3DDP2OP\_清除操作代码清除多个的呈现器目标组的所有元素。

 

 





