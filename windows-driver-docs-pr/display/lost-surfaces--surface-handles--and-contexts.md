---
title: 丢失的图面、图面句柄和上下文
description: 丢失的图面、图面句柄和上下文
ms.assetid: d2458077-56f8-481b-b612-a706e9560314
keywords:
- 上下文 WDK Direct3D，D3dCreateSurfaceEx
- D3dCreateSurfaceEx
- surface 处理 WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f7395ce401f96cd5dbd82df27871b2d3cdf95252
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89065756"
---
# <a name="lost-surfaces-surface-handles-and-contexts"></a>丢失的图面、图面句柄和上下文


## <span id="ddk_lost_surfaces_surface_handles_and_contexts_gg"></span><span id="DDK_LOST_SURFACES_SURFACE_HANDLES_AND_CONTEXTS_GG"></span>


某些表面应在上下文 (如呈现器目标、Z 缓冲区或纹理) 中引用，通常是在驱动程序的上下文中存储这些图面的句柄。 当驱动程序涉及到 (销毁) 时，这些表面可能会丢失。 上下文本身可能仍然存在，但现在可能已过时 (无效的) 句柄丢失面。 运行时保证当呈现命令处于此状态时，不会将其传递到上下文，但仍存在如何将上下文与还原后的图面重新关联的问题，然后才能再次开始呈现。 运行时保证丢失表面的句柄不会改变。 这反过来保证，如果上下文在 (呈现目标、Z 和纹理) 的图面上保留其图面，则这些表面始终是 *使用相同的句柄值* 重新创建的 () 还原后，才能在此上下文上恢复。

某些驱动程序编写器可能想要通过直接在上下文中存储图面数据来优化上下文的状态，而不是在每个 [**D3dDrawPrimitives2**](/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb) 调用上取消引用句柄。 由于此取消引用的成本可能比执行一批 *D3dDrawPrimitives2* 令牌的成本小，因此不建议使用此优化。 但是，如果驱动程序编写器希望执行此操作，则它们必须知道在还原后，可能会移动表面。 这意味着尽管句柄可能是相同的，但不保证使用同一 **fpVidMem** 还原图面， (与创建它的 [**DD \_ surface \_ 全局**](/windows/desktop/api/ddrawint/ns-ddrawint-_dd_surface_global) 结构) 指针的成员。 以这种方式优化的上下文可能最终会得到陈旧的视频内存指针，并且没有图面已移动的信息。 处理此情况的一种方法是，当驱动程序与 (为呈现目标、Z 缓冲区或纹理) 的上下文相关联时，该驱动程序可以标记任何图面。 然后在 [**D3dCreateSurfaceEx**](/windows/desktop/api/ddrawint/nc-ddrawint-pdd_createsurfaceex) 时，它可以搜索引用此表面的任何上下文，然后更新该上下文。

不建议在表面上保留指向上下文的指针，因为一个图面可能与多个上下文相关联。

DirectDraw SDK 文档中引入了 *丢失* 表面的概念。 丢失的曲面在 DirectX 7.0 DDI 模型中存在一些含义。 有关详细信息，请参阅 [丢失和还原 DirectDraw 表面](losing-and-restoring-directdraw-surfaces.md)。

 

