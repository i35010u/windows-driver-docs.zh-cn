---
title: 使用跨适配器资源在独立的 GPU 中进行渲染
description: 从 Windows 8.1 开始，离散 GPU 使用跨适配器资源作为位块传输的目标 (bitblt) 或呈现操作，但不使用拉伸或颜色转换。操作系统请求用户模式显示驱动程序在其上执行 bitblt 或当前操作的资源。集成的 GPU 使用跨适配器资源作为桌面窗口管理器 (DWM) 进行组合时的纹理。GDI 硬件加速的呈现目标。显示主。不作为三维操作的呈现目标。
ms.assetid: 88CE2D2F-BBD8-4CE4-9183-BBFB0659990E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3c1838c34b093d5c7a646fd1ac2b2dab2434cb55
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89067272"
---
# <a name="span-iddisplayrendering_on_a_discrete_gpu_using_cross-adapter_resourcesspanrendering-on-a-discrete-gpu-using-cross-adapter-resources"></a><span id="display.rendering_on_a_discrete_gpu_using_cross-adapter_resources"></span>使用跨适配器资源在独立的 GPU 中进行渲染


从 Windows 8.1 开始， [离散 GPU](using-cross-adapter-resources-in-a-hybrid-system.md) 使用 [跨适配器资源](using-cross-adapter-resources-in-a-hybrid-system.md) ，如下所示：

-   位块传输的目标 (bitblt) 或当前操作，但是无需拉伸或颜色转换。
-   操作系统请求用户模式显示驱动程序对其执行 bitblt 或当前操作的资源。

[集成 GPU](using-cross-adapter-resources-in-a-hybrid-system.md)使用[跨适配器资源](using-cross-adapter-resources-in-a-hybrid-system.md)，如下所示：

-   由桌面窗口管理器 (DWM) 进行组合时的纹理。
-   [GDI 硬件加速](gdi-hardware-acceleration.md)的呈现目标。
-   显示主。
-   不作为三维操作的呈现目标。

以下各节描述了在混合系统内的独立 GPU 上呈现应用程序的三种可能情况下所涉及的体系结构和过程。

## <a name="span-idredirected_bitblt_modelspanspan-idredirected_bitblt_modelspanredirected-bitblt-presentation-model"></a><span id="redirected_bitblt_model"></span><span id="REDIRECTED_BITBLT_MODEL"></span>重定向的 bitblt 表示模型


![应用用于在离散 gpu 上呈现的混合图形重定向 bitblt 模型。](images/hybrid-graphics-arch-blit.png)

1.  顶层窗口的跨适配器资源以内核模式创建，作为集成 GPU 上的标准分配。
2.  当在离散 GPU 上打开此资源时，Microsoft DirectX 图形内核子系统 ( # A0) 会调用 [*DxgkDdiGetStandardAllocationDriverData*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_getstandardallocationdriverdata) 函数，并使用与集成 gpu 相同的后备存储器 (大容量存储设备) ，在离散 GPU 上创建新的资源。
3.  Microsoft Direct3D 运行时指示离散 GPU 的用户模式显示驱动程序使用专用驱动程序数据打开跨适配器资源。
4.  DirectX 应用程序在离散 GPU 上呈现为后台缓冲区资源。 请参阅图中的 "Render" 操作。
5.  当 DirectX 应用程序调用 **当前** 方法时，Direct3D 运行时将调用离散 GPU 的用户模式驱动程序的 [*PresentDXGI*](/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi_ddi_base_functions) (或 *pfnPresent*) 函数，将后台缓冲区复制到跨适配器资源。 请参阅图中的 "显示" 操作。
6.  当 Windows 图形设备接口 (GDI) 应用程序呈现到顶级窗口时，DirectX 图形内核子系统将调用集成 GPU 的显示微型端口驱动程序的 [*DxgkDdiRenderKm*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_renderkm) 函数，并指示跨适配器资源是一个呈现器目标。 请参阅此图中的 GDI 应用程序和跨适配器图面之间的连接。
7.  DWM 进程会在集成 GPU 中打开跨适配器资源，并在组合过程中将其用作源纹理。 请参阅图中的 "撰写" 运算。

## <a name="span-iddirect_flip_modelspanspan-iddirect_flip_modelspandirect-flip-presentation-model"></a><span id="direct_flip_model"></span><span id="DIRECT_FLIP_MODEL"></span>直接翻转演示模型


![应用用于在离散 gpu 上呈现的混合图形直接翻转模型。](images/hybrid-graphics-arch-flip.png)

1.  Direct3D 运行时指示离散 GPU 的用户模式显示驱动程序为每个交换链图面创建一个跨适配器资源。
2.  在离散 GPU 上，如果直接翻转模式可用，Direct3D 运行时可能会设置[**D3DDDI \_ ALLOCATIONINFO**](/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_d3dddi_allocationinfo)结构的**主**成员和**VidPnSourceId**成员。 调用 [*pfnAllocateCb*](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_allocatecb) 函数时，应传递这些成员值。
3.  Direct3D 运行时指示集成 GPU 的用户模式显示驱动程序打开将由 DWM 管理的跨适配器资源。
4.  使用呈现目标纹理作为目标，在离散 GPU 上呈现应用程序。 请参阅图中的 "Render" 操作。
5.  当应用程序调用 **当前** 方法时，Direct3D 运行时将调用离散 GPU 的用户模式驱动程序的 [*BltDXGI*](/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi_ddi_base_functions) (或 *pfnBlt*) 函数，以对跨适配器资源执行复制。 然后，运行时调用离散 GPU 的用户模式驱动程序的 [*PresentDXGI*](/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi_ddi_base_functions) (或 *pfnPresent*) 函数，并将 source 设置为跨适配器资源，并将目标分配设置为 **NULL**。 请参阅图中的 "复制" 操作。
6.  DWM 使用集成 GPU 中的资源执行其组合。 如果需要直接翻转操作 ([**DXGK \_ SEGMENTFLAGS**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_segmentflags)。**DirectFlip** 设置) ，DWM 指示集成 GPU 的显示微型端口驱动程序执行从一个跨适配器分配到另一个跨适配器分配的反向操作。 请参阅图中的 "DWM 翻转" 操作。

## <a name="span-idfullscreen_modelspanspan-idfullscreen_modelspanfull-screen-model"></a><span id="fullscreen_model"></span><span id="FULLSCREEN_MODEL"></span>全屏模型


1.  Direct3D 运行时指示集成 GPU 的用户模式显示驱动程序为每个交换链图面创建跨适配器共享主分配。
2.  Direct3D 运行时指示离散 GPU 的用户模式显示驱动程序打开跨适配器资源。
3.  应用程序使用呈现目标纹理作为目标，在离散 GPU 上呈现。
4.  当应用程序调用 **当前** 方法时，Direct3D 运行时指示离散 GPU 的用户模式显示驱动程序对跨适配器资源执行复制。
5.  集成 GPU 的用户模式显示驱动程序和显示微型端口驱动程序将指示切换到此跨适配器资源。

 

