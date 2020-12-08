---
title: 复杂图面和附件
description: 复杂图面和附件
keywords:
- 绘图图面 WDK DirectDraw，复杂
- DirectDraw 图面，WDK Windows 2000 显示，复杂
- 表面 WDK DirectDraw，复杂
- 复杂图面 WDK DirectDraw
- surface DirectDraw，附件
- 绘图图面 WDK DirectDraw，附件
- DirectDraw 图面，WDK Windows 2000 显示，附件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5ffa2fee4aeac1f6361bc93bfc11afcf32fd6101
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96810223"
---
# <a name="complex-surfaces-and-attachments"></a>复杂图面和附件


## <span id="ddk_complex_surfaces_and_attachments_gg"></span><span id="DDK_COMPLEX_SURFACES_AND_ATTACHMENTS_GG"></span>


曲面可能比较 *复杂*，这意味着它们属于更大的关联曲面集合。 复杂曲面的示例包括：前台缓冲区和关联的后台缓冲区、MIP 地图的各个级别以及 cube 地图的各个面。

DirectDraw 运行时使用称为 " *表面附件* " 的概念来管理不同的简单图面到复杂表面的链接。 可以隐式方式附加表面，就像应用程序对 **IDirectDraw7：： CreateSurface** 进行一次调用以生成翻转链 (前台缓冲区和具有可能 Z 缓冲区的后台缓冲区) ;或显式，如应用程序通过调用 **IDirectDrawSurface7：： AddAttachedSurface** 将 Z 缓冲区与呈现目标相关联。

 

 





