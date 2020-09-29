---
title: D3dCreateSurfaceEx 句柄和交替
description: D3dCreateSurfaceEx 句柄和交替
ms.assetid: b87762fd-444d-437a-b076-189f51cc6dd1
keywords:
- 上下文 WDK Direct3D，D3dCreateSurfaceEx
- D3dCreateSurfaceEx
- 翻转 WDK Direct3D
- DdFlip
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 062c92aed5d4dbc23af5995b34769e11ff8887b0
ms.sourcegitcommit: f8619f20a0903dd64f8641a5266ecad6df5f1d57
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/29/2020
ms.locfileid: "91424006"
---
# <a name="d3dcreatesurfaceex-handles-and-flip"></a>D3dCreateSurfaceEx 句柄和交替


## <span id="ddk_d3dcreatesurfaceex_handles_and_flip_gg"></span><span id="DDK_D3DCREATESURFACEEX_HANDLES_AND_FLIP_GG"></span>


DirectDraw surface 结构设计用于表示概念图面，而不一定是视频内存中的特定位置。 此抽象的主要用法是在主翻转链中，其中，应用程序使用一个常数 surface 对象来表示后台缓冲区，即使后台缓冲区可能在视频内存中由于 [*DdFlip*](/windows/win32/api/ddrawint/nc-ddrawint-pdd_surfcb_flip) 函数而移动。

[*DdFlip*](/windows/win32/api/ddrawint/nc-ddrawint-pdd_surfcb_flip)函数采用一环面，并按顺序重新分配其视频内存指针。 在两个 surface 对象的特定情况下，该过程会减少，以便对其视频内存指针进行贸易。 此外，DirectDraw 运行时还会旋转与每个图面关联的 [**D3dCreateSurfaceEx**](/windows/win32/api/ddrawint/nc-ddrawint-pdd_createsurfaceex) 控点，以及每个图面的 **dwReserved1** 成员的驱动程序拥有的内容。 此行为对 DirectX 7.0 驱动程序有一些有趣的后果，并有效地将指针嵌入到驱动程序自身的 surface 结构内的 DirectDraw surface 结构内。

假设有两个图面对象 A 和 B，它们具有关联的句柄 H<sub>a</sub> 和 h<sub>B</sub>， **fpVidMem** ([**DD \_ surface \_ GLOBAL**](/windows/win32/api/ddrawint/ns-ddrawint-dd_surface_global) structure 的成员) F<sub>A</sub> 和 f<sub>B</sub>的值。 此外，假设应用程序使用的是 surface 结构 A 来引用反向链的后台缓冲区。 在 [*DdFlip*](/windows/win32/api/ddrawint/nc-ddrawint-pdd_surfcb_flip) 时，手柄和两个 **fpVidMem** 值都被交换，因此图面 A 具有 h<sub>b</sub> 和 f<sub>b</sub>，而 surface B 具有 h<sub>a</sub> 和 f<sub>a</sub>。 应用程序现在尝试绘制到后台缓冲区（图面 A），它应该代表 F<sub>B</sub> (的视频内存，因为该应用程序启动了对 *DdFlip*) 的调用。

向驱动程序发出一个绘图命令，该命令将查找与该表面关联的句柄， (现在为 H<sub>B</sub>，而不是 h<sub>A</sub>) 。 如果驱动程序只是存储一个指向 DirectDraw surface 结构的指针，会发生什么情况呢？ 该驱动程序将查找 H<sub>B</sub>，然后将存储的指针跟随到 surface B，该图面上的 **FpVidMem** 值为 F<sub>A</sub>。 绘图从 F<sub>A</sub>的视频内存开始。 这并不是应用程序的预期。 另一方面，如果驱动程序将表面数据存储在其自己的结构中，而不是使用指向 DirectDraw surface 结构的指针，则 H<sub>B</sub> 仍会解析为 F<sub>b</sub>，并在正确的图面上进行绘制。 后一种情况是实现当前 DDI 的方式。

 

