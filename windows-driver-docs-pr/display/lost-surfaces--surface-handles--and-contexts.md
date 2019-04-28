---
title: 丢失的图面、图面句柄和上下文
description: 丢失的图面、图面句柄和上下文
ms.assetid: d2458077-56f8-481b-b612-a706e9560314
keywords:
- 上下文 WDK Direct3D D3dCreateSurfaceEx
- D3dCreateSurfaceEx
- 图面处理 WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ca7eefde044f6a8b2f7a44a4986a513e5377d4ac
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63347531"
---
# <a name="lost-surfaces-surface-handles-and-contexts"></a>丢失的图面、图面句柄和上下文


## <span id="ddk_lost_surfaces_surface_handles_and_contexts_gg"></span><span id="DDK_LOST_SURFACES_SURFACE_HANDLES_AND_CONTEXTS_GG"></span>


某些图面应该是中引用上下文 （如呈现器目标、 Z 缓冲区或纹理），通常通过将这些应用层协议的句柄存储在驱动程序的上下文中。 可能会丢失这些图面设置变得 （销毁） 而言，驱动程序。 上下文本身可能会幸存，但现在可能已过时 （无效） 句柄丢失图面。 在运行时可保证时处于此状态，但仍是如何与已还原的图面重新关联上下文，才可再次开始呈现的问题没有呈现的命令传递到上下文。 在运行时可保证对于丢失的图面句柄不会更改。 这反过来可保证，如果保留为其图面 （呈现器目标、 Z 和纹理），则这些图面的句柄将始终重新创建 （已还原） 的上下文*具有相同处理值*呈现可以继续在此上下文之前。

某些驱动程序编写人员可能想要通过直接在上下文中，存储图面上的数据，而不是以取消句柄引用上的工作来优化上下文的状态每隔[ **D3dDrawPrimitives2** ](https://msdn.microsoft.com/library/windows/hardware/ff544704)调用. 与执行的批处理的开销相比，因为此取消引用的成本可能是小型*D3dDrawPrimitives2*令牌，此优化不建议。 但是，如果驱动程序编写人员想要执行此操作，则他们必须注意图面可能移动时还原它们。 这意味着，尽管该句柄可能相同，则不能保证图面还原具有相同**fpVidMem** (隶属[ **DD\_图面\_全局**](https://msdn.microsoft.com/library/windows/hardware/ff551726)结构) 创建它时采用的指针。 以这种方式进行了优化的上下文可能结尾过时的视频内存的指针，并没有在图面已移动的信息。 若要解决此问题的一种方法是与上下文 （如呈现目标、 Z 缓冲区或纹理） 相关联时，该驱动程序可能会标记的任何图面。 然后在[ **D3dCreateSurfaceEx** ](https://msdn.microsoft.com/library/windows/hardware/ff542840)时间，它可以搜索任何上下文中引用此图面，然后更新该上下文。

不建议一个面将指针保留到上下文，因为一个外围可能与多个上下文相关联。

这一概念*丢失*DirectDraw SDK 文档中引入了图面。 丢失的图面 DirectX 7.0 DDI 模型中有一些影响。 有关详细信息，请参阅[丢失和还原 DirectDraw 图面](losing-and-restoring-directdraw-surfaces.md)。

 

 





