---
title: 裁剪已转换的顶点
description: 裁剪已转换的顶点
keywords:
- DirectX 8.0 发行说明 WDK Windows 2000 显示，剪切转换的顶点
- pretransformed 顶点 WDK DirectX 8。0
- 剪辑 WDK DirectX 8。0
- 顶点剪辑 WDK DirectX 8。0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3eeb521117811382780bbc089c121bb58c9ea283
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96810303"
---
# <a name="clipping-transformed-vertices"></a>裁剪已转换的顶点


## <span id="ddk_clipping_transformed_vertices_gg"></span><span id="DDK_CLIPPING_TRANSFORMED_VERTICES_GG"></span>


Direct3D 8.0 运行时完全支持通过 **DrawPrimitive** 和 **ProcessVertices** API 调用来剪裁 pretransformed 顶点。 此剪辑包括用户定义的剪辑平面以及 Z 和 X 和 Y 视区区。 但是，运行时不保证 posttransformed 顶点的剪裁。 Posttransformed 顶点数据由运行时从应用程序直接传递给驱动程序。 这并不意味着需要使用驱动程序来完全剪裁 posttransformed 顶点数据。 已为 DirectX 8.0 添加了新功能标志 D3DPMISCCAPS \_ CLIPTLVERTS。 如果驱动程序在 D3DCAPS8 结构的 **PrimitiveMiscCaps** 字段中设置此标志，则应用程序可以假定驱动程序将 posttransformed 顶点数据完全剪辑到 Z 和 X 和 Y 视区区。 Posttransformed 数据不支持剪辑到用户定义的剪辑平面。 如果驱动程序未设置此标志，则需要应用程序将 posttransformed 数据剪裁到 Z 区，并 (至少) X 和 Y 中的防护带区。

请注意，运行时不会验证应用程序是否已正确剪裁 posttransformed 数据，这一点很重要。 如果在设置此标志时传递了未剪辑或错误剪切的数据，则驱动程序的责任是确保不会发生崩溃或挂起。

 

 





