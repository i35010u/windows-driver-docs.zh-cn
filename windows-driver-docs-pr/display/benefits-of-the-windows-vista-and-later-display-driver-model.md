---
title: Windows 显示驱动程序模型 (WDDM) 的优势
description: Windows 显示驱动程序模型 (WDDM) 的优势
ms.assetid: 0e8cd1a9-7137-4fd2-91ab-56768713c9f1
keywords:
- 显示驱动程序模型 WDK Windows Vista 中，优点
- Windows Vista 显示器驱动程序模型 WDK，权益
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3eeebf753a7ffe3452e5ce939ccba286abd8da72
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568801"
---
# <a name="benefits-of-the-windows-display-driver-model-wddm"></a>Windows 显示驱动程序模型 (WDDM) 的优势


## <span id="ddk_benefits_of_the_longhorn_display_driver_model_gg"></span><span id="DDK_BENEFITS_OF_THE_LONGHORN_DISPLAY_DRIVER_MODEL_GG"></span>


创建显示器驱动程序是使用 Windows 显示驱动程序模型 (WDDM)，而不使用 Windows vista 中，从开始，提供更容易[Windows 2000 显示驱动程序模型 (XDDM)](windows-2000-display-driver-model-design-guide.md)，由于以下增强功能。 此外，WDDM 驱动程序对更高版本操作系统的稳定性和安全性参与，因为更少的驱动程序代码运行在内核模式下，它可以访问系统地址空间，并可能导致崩溃。

**请注意**  XDDM 和 VGA 驱动程序不会在 Windows 8 和更高版本上进行编译。 如果显示硬件附加到没有认证支持 WDDM 1.2 或更高版本的驱动程序的 Windows 8 计算机，则系统会默认到正在运行的 Microsoft 基本显示驱动程序。

 

-   Microsoft Direct3D 运行时和 Microsoft DirectX 图形内核子系统执行多个显示处理 （也就是说，更多的代码中的运行时和而不是驱动程序的子系统是）。 这包括管理视频内存的代码和计划的 GPU 直接内存访问 (DMA) 缓冲区。 有关详细信息，请参阅[视频内存管理和 GPU 计划](video-memory-management-and-gpu-scheduling.md)。

-   图面上创建需要更少内核模式阶段。

    图面上的创建操作系统上前面比 Windows Vista 需要以下连续的内核模式下调用：

    1.  [*DdCanCreateSurface*](https://msdn.microsoft.com/library/windows/hardware/ff549213)
    2.  [*DdCreateSurface*](https://msdn.microsoft.com/library/windows/hardware/ff549263)
    3.  [**D3dCreateSurfaceEx**](https://msdn.microsoft.com/library/windows/hardware/ff542840)

    WDDM 中的图面上创建仅需要[ **CreateResource** ](https://msdn.microsoft.com/library/windows/hardware/ff540688)用户模式显示驱动程序调用，后者又调用[ **pfnAllocateCb** ](https://msdn.microsoft.com/library/windows/hardware/ff568893)函数。 内核模式下的调用[ **DxgkDdiCreateAllocation** ](https://msdn.microsoft.com/library/windows/hardware/ff559606)函数则会发生。

-   调用的创建和销毁图面和的锁定和解锁资源更均匀地配对。

-   WDDM 中具有相同处理视频内存、 系统内存和托管的图面。 Windows Vista 之前的操作系统略有不同的方式处理这些组件。

-   显示器驱动程序的用户模式部分中执行着色器转换。

    此方法可以避免在内核模式下执行着色器转换时，发生以下复杂性：

    -   与设备驱动程序接口 (DDI) 抽象不匹配的硬件型号
    -   在转换中使用的复杂的编译器技术

    因为着色器处理完全发生每个进程，并且不需要硬件访问，则不需要处理的内核模式着色器。 因此，可以在用户模式下处理着色器转换代码。

    您必须编写 try/except 用户模式转换代码周围的代码。 转换错误会导致返回到应用程序处理。

    背景翻译 （即，从其他显示处理线程在一个单独的线程中运行的转换代码） 是更轻松地为用户模式下编写。

 

 





