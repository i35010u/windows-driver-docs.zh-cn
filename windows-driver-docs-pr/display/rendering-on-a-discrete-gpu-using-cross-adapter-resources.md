---
title: 使用跨适配器资源是分立的 GPU 上呈现
description: 从 Windows 8.1，是分立的 GPU 使用跨适配器资源为目标但不支持拉伸或颜色转换的位块传输 (bitblt) 或存在操作。操作系统请求用户模式下的资源显示驱动程序来执行 bitblt 或存在到操作和 from.integrated GPU 纹理作为桌面窗口管理器 (DWM) 组合期间使用跨适配器资源。GDI 硬件加速呈现器目标。主显示器。不是作为呈现器目标的三维操作。
ms.assetid: 88CE2D2F-BBD8-4CE4-9183-BBFB0659990E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 91990d20e5d0f1b8781285a50ca026416f0da7b4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520597"
---
# <a name="span-iddisplayrenderingonadiscretegpuusingcross-adapterresourcesspanrendering-on-a-discrete-gpu-using-cross-adapter-resources"></a><span id="display.rendering_on_a_discrete_gpu_using_cross-adapter_resources"></span>使用跨适配器资源是分立的 GPU 上呈现


在 Windows 8.1 中启动[分立的 GPU](using-cross-adapter-resources-in-a-hybrid-system.md)使用[跨适配器资源](using-cross-adapter-resources-in-a-hybrid-system.md)作为：

-   但不支持拉伸或颜色转换位块传输 (bitblt) 或存在操作的目标。
-   操作系统请求用户模式显示驱动程序来执行 bitblt 或存在操作与该资源。

[集成 GPU](using-cross-adapter-resources-in-a-hybrid-system.md)使用[跨适配器资源](using-cross-adapter-resources-in-a-hybrid-system.md)作为：

-   撰写的桌面窗口管理器 (DWM) 期间纹理。
-   有关呈现器目标[GDI 硬件加速](gdi-hardware-acceleration.md)。
-   主显示器。
-   不是作为呈现器目标的三维操作。

以下部分介绍在混合系统中是分立的 GPU 上的体系结构和应用程序会呈现其中三个可能的方案中所涉及的进程。

## <a name="span-idredirectedbitbltmodelspanspan-idredirectedbitbltmodelspanredirected-bitblt-presentation-model"></a><span id="redirected_bitblt_model"></span><span id="REDIRECTED_BITBLT_MODEL"></span>重定向的 bitblt 表示模型


![混合图形重定向 bitblt 模型应用中使用的分立的 gpu 上呈现。](images/hybrid-graphics-arch-blit.png)

1.  集成在 GPU 上的标准分配内核模式中创建跨适配器资源为顶层窗口。
2.  Microsoft DirectX 图形内核子系统 (Dxgkrnl.sys) 分立的 GPU 上打开此资源时，调用[ *DxgkDdiGetStandardAllocationDriverData* ](https://msdn.microsoft.com/library/windows/hardware/ff559673)函数，并创建一个新分立的 GPU 使用同一个后备存储区 （大容量存储设备） 与集成的 GPU 上的资源。
3.  Microsoft Direct3D 运行时指示分立的 GPU 用户模式显示驱动程序，以打开跨适配器资源使用专用驱动程序数据。
4.  DirectX 应用程序中的呈现到后台缓冲区资源分立的 GPU。 请参阅图中的"呈现"操作。
5.  在 DirectX 应用程序调用**存在**方法中，Direct3D 运行时调用[ *PresentDXGI* ](https://msdn.microsoft.com/library/windows/hardware/ff569179) (或*pfnPresent*) 的函数分立的 GPU 用户模式驱动程序将后台缓冲区复制到跨适配器资源。 请参阅图中的"Present"操作。
6.  当 Windows 图形设备接口 (GDI) 应用程序呈现到顶级窗口时，调用 DirectX 图形内核子系统[ *DxgkDdiRenderKm* ](https://msdn.microsoft.com/library/windows/hardware/ff559800)集成的 GPU 显示函数微型端口驱动程序，它指示跨适配器资源是呈现器目标。 请参阅 GDI 应用程序和在图中的跨适配器面之间的连接。
7.  DWM 进程将在集成的 GPU 中打开跨适配器资源，并将其作为源纹理的组合期间。 请参阅图中的"撰写"操作。

## <a name="span-iddirectflipmodelspanspan-iddirectflipmodelspandirect-flip-presentation-model"></a><span id="direct_flip_model"></span><span id="DIRECT_FLIP_MODEL"></span>直接翻转表示模型


![混合图形直接应用中使用的分立的 gpu 上呈现的翻转模式。](images/hybrid-graphics-arch-flip.png)

1.  Direct3D 运行时指示分立的 GPU 用户模式显示驱动程序创建跨适配器资源的每个交换链图面。
2.  分立的 GPU，Direct3D 运行时可能设置**主**并**VidPnSourceId**的成员[ **D3DDDI\_ALLOCATIONINFO**](https://msdn.microsoft.com/library/windows/hardware/ff544364)结构直接翻转模式是否可用。 这些成员值应传递何时[ *pfnAllocateCb* ](https://msdn.microsoft.com/library/windows/hardware/ff568893)调用函数。
3.  Direct3D 运行时指示集成的 GPU 的用户模式显示驱动程序，打开要由 DWM 的跨适配器资源。
4.  应用程序将呈现在分立的 GPU 上呈现器目标纹理用作目标。 请参阅图中的"呈现"操作。
5.  当应用程序调用**存在**方法中，Direct3D 运行时调用[ *BltDXGI* ](https://msdn.microsoft.com/library/windows/hardware/ff538252) (或*pfnBlt*) 的离散函数GPU 的用户模式驱动程序来执行复制到跨适配器资源。 然后，运行时调用[ *PresentDXGI* ](https://msdn.microsoft.com/library/windows/hardware/ff569179) (或*pfnPresent*) 分立的 GPU 用户模式驱动程序，与源的函数将设置为跨适配器资源和设置为的目标分配**NULL**。 请参阅图中的"复制"操作。
6.  DWM 执行其组合使用集成的 GPU 的资源。 如果需要直接翻转操作 ([**DXGK\_SEGMENTFLAGS**](https://msdn.microsoft.com/library/windows/hardware/ff562039)。**DirectFlip**设置)，DWM 指示集成的 GPU 显示微型端口驱动程序可以通过执行翻转操作一个跨适配器分配。 请参阅图中的"DWM 翻转"操作。

## <a name="span-idfullscreenmodelspanspan-idfullscreenmodelspanfull-screen-model"></a><span id="fullscreen_model"></span><span id="FULLSCREEN_MODEL"></span>全屏幕模型


1.  Direct3D 运行时指示集成的 GPU 的用户模式显示驱动程序创建跨适配器共享主分配的每个交换链图面。
2.  Direct3D 运行时指示分立的 GPU 用户模式显示驱动程序，以打开跨适配器资源。
3.  应用程序将呈现在分立的 GPU 上呈现器目标纹理用作目标。
4.  当应用程序调用**存在**方法，Direct3D 运行时指示分立的 GPU 用户模式显示驱动程序来执行复制到跨适配器资源。
5.  指示集成的 GPU 的用户模式显示驱动程序和显示微型端口驱动程序对此跨适配器资源翻转。

 

 





