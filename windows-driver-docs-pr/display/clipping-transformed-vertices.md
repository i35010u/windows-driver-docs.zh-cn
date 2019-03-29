---
title: 裁剪已转换的顶点
description: 裁剪已转换的顶点
ms.assetid: 33b03264-780e-4b05-a108-6d1a017e8c27
keywords:
- 显示 DirectX 8.0 发行说明 WDK Windows 2000，剪辑已转换的顶点
- pretransformed 的顶点 WDK DirectX 8.0
- 剪辑 WDK DirectX 8.0
- 剪辑 WDK DirectX 8.0 的顶点
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c1ced8e7305e8c15daa07fd1032ed51eaef4043c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56569315"
---
# <a name="clipping-transformed-vertices"></a>裁剪已转换的顶点


## <span id="ddk_clipping_transformed_vertices_gg"></span><span id="DDK_CLIPPING_TRANSFORMED_VERTICES_GG"></span>


Direct3D 8.0 运行时完全支持通过两 pretransformed 顶点的剪辑**DrawPrimitive**并**ProcessVertices** API 调用。 此剪辑包含用户定义剪辑平面和 Z，X 和 Y 的视区扩展盘区。 但是，在运行时不保证 posttransformed 顶点的剪辑。 运行时传递 posttransformed 的顶点数据直接从应用程序到驱动程序。 这并不意味着一个驱动程序所需完全剪辑 posttransformed 的顶点数据。 新的功能标志 D3DPMISCCAPS\_CLIPTLVERTS 已添加对 DirectX 8.0。 如果驱动程序设置此标志**PrimitiveMiscCaps** D3DCAPS8 结构，该应用程序的字段可以假定该驱动程序完全剪辑到 Z 和 X 和 Y 视区扩展盘区 posttransformed 的顶点数据。 Posttransformed 数据永远不会支持用户定义的剪辑平面的剪辑。 该驱动程序不会设置此标志，该应用程序是否需要执行剪切的 posttransformed 数据到 Z 盘区和 （至少） 的防护外区中 X 和 Y。

请务必注意，运行时不会验证应用程序已正确剪辑 posttransformed 的数据。 它是驱动程序的责任，以确保，崩溃或挂起不会发生时设置此标志，如果传递未剪辑或错误地裁剪后的数据。

 

 





