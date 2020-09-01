---
title: Windows 显示驱动程序模型 (WDDM) 的优势
description: Windows 显示驱动程序模型 (WDDM) 的优势
ms.assetid: 0e8cd1a9-7137-4fd2-91ab-56768713c9f1
keywords:
- 显示驱动程序模型 WDK Windows Vista，优点
- Windows Vista 显示器驱动程序模型 WDK，优点
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e8b853e6d5af61864a0521cfb20fc9ccae3fa6d4
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89067480"
---
# <a name="benefits-of-the-windows-display-driver-model-wddm"></a>Windows 显示驱动程序模型 (WDDM) 的优势


## <span id="ddk_benefits_of_the_longhorn_display_driver_model_gg"></span><span id="DDK_BENEFITS_OF_THE_LONGHORN_DISPLAY_DRIVER_MODEL_GG"></span>


由于以下增强，使用 windows Vista (WDDM) （从 Windows Vista 开始提供），可以更轻松地创建显示驱动程序，而不是使用 [windows 2000 显示器驱动程序模型 (XDDM) ](windows-2000-display-driver-model-design-guide.md)。 此外，WDDM 驱动程序会导致更高的操作系统稳定性和安全性，因为更少的驱动程序代码在可访问系统地址空间并可能导致崩溃的内核模式下运行。

**注意**   在 Windows 8 及更高版本上，XDDM 和 VGA 驱动程序将不会编译。 如果将显示硬件连接到 Windows 8 计算机，而该计算机上没有一个已认证为支持 WDDM 1.2 或更高版本的驱动程序，则系统默认为运行 Microsoft 基本显示驱动程序。

 

-   Microsoft Direct3D 运行时和 Microsoft DirectX 图形内核子系统执行更多的显示处理 (即，更多代码位于运行时和子系统中，而不是驱动程序) 。 这包括管理视频内存的代码，并计划 (DMA) 缓冲区的直接内存访问。 有关详细信息，请参阅 [视频内存管理和 GPU 计划](video-memory-management-and-gpu-scheduling.md)。

-   创建图面需要的内核模式阶段更少。

    在早于 Windows Vista 的操作系统上创建表面需要执行以下连续的内核模式调用：

    1.  [*DdCanCreateSurface*](/previous-versions/windows/hardware/drivers/ff549213(v=vs.85))
    2.  [*DdCreateSurface*](/previous-versions/windows/hardware/drivers/ff549263(v=vs.85))
    3.  [**D3dCreateSurfaceEx**](/windows/desktop/api/ddrawint/nc-ddrawint-pdd_createsurfaceex)

    在 WDDM 中创建 Surface 只需要 [**CreateResource**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createresource) 用户模式显示驱动程序调用，后者又会调用 [**pfnAllocateCb**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_allocatecb) 函数。 然后对内核模式 [**DxgkDdiCreateAllocation**](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_createallocation) 函数进行调用。

-   用于创建和销毁表面以及锁定和解锁资源的调用将更均匀地配对。

-   视频内存、系统内存和托管的图面在 WDDM 中的处理方式相同。 在 Windows Vista 之前的操作系统，这些组件的处理方式稍有不同。

-   着色器转换是在显示驱动程序的用户模式部分中执行的。

    此方法消除了在内核模式下执行着色器转换时发生的以下复杂性：

    -   与设备驱动程序接口不匹配的硬件型号 (DDI) 抽象
    -   翻译中使用的复杂编译器技术

    由于着色器处理是按进程完全进行的，并且不需要对硬件进行访问，因此不需要进行内核模式着色器处理。 因此，可以在用户模式下处理着色器转换代码。

    必须围绕用户模式转换代码编写 try/except 代码。 转换错误应导致返回应用程序处理。

    后台转换 (也就是说，在不同于其他显示处理) 线程的同一线程中运行的翻译代码，在用户模式下更易于编写。

 

