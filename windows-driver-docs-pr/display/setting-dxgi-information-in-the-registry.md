---
title: 在注册表中设置 DXGI 信息
description: 在注册表中设置 DXGI 信息
ms.assetid: 2d116c89-02dd-4104-be75-70a00fa5e06a
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 87ec69f3879b23862fba4dc2d3c4edcbdb93a0f6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390464"
---
# <a name="setting-dxgi-information-in-the-registry"></a>在注册表中设置 DXGI 信息


DXGI 和参考光栅器使用以下注册表项：

<span id="DWORD_Software_Microsoft_DXGI_DisableFullscreenWatchdog"></span><span id="dword_software_microsoft_dxgi_disablefullscreenwatchdog"></span><span id="DWORD_SOFTWARE_MICROSOFT_DXGI_DISABLEFULLSCREENWATCHDOG"></span>DWORD Software\\Microsoft\\DXGI\\DisableFullscreenWatchdog  
设置为 1 可禁用监视程序线程。

<span id="DWORD_Software_Microsoft_Direct3D_ReferenceDevice_FlushOften"></span><span id="dword_software_microsoft_direct3d_referencedevice_flushoften"></span><span id="DWORD_SOFTWARE_MICROSOFT_DIRECT3D_REFERENCEDEVICE_FLUSHOFTEN"></span>DWORD Software\\Microsoft\\Direct3D\\ReferenceDevice\\FlushOften  
设置为 1，经常刷新。

<span id="DWORD_Software_Microsoft_Direct3D_ReferenceDevice_FenceEachEntryPoint"></span><span id="dword_software_microsoft_direct3d_referencedevice_fenceeachentrypoint"></span><span id="DWORD_SOFTWARE_MICROSOFT_DIRECT3D_REFERENCEDEVICE_FENCEEACHENTRYPOINT"></span>DWORD Software\\Microsoft\\Direct3D\\ReferenceDevice\\FenceEachEntryPoint  
设置为 1，以使每次调用 GPU 使用 DDI 函数围墙。 隔离与 GPU 意味着以刷新命令批处理并阻止，直到 GPU 处于空闲状态。

<span id="DWORD_Software_Microsoft_Direct3D_ReferenceDevice_Debug"></span><span id="dword_software_microsoft_direct3d_referencedevice_debug"></span><span id="DWORD_SOFTWARE_MICROSOFT_DIRECT3D_REFERENCEDEVICE_DEBUG"></span>DWORD 软件\\Microsoft\\Direct3D\\ReferenceDevice\\调试  
将设置为 1 到：

-   通常刷新，并使每次调用 GPU 使用 DDI 函数围墙。

-   运行参考光栅器 (RefRast) 单线程。

<span id="DWORD_Software_Microsoft_Direct3D_ReferenceDevice_D3D10RefGdiDisplayMask"></span><span id="dword_software_microsoft_direct3d_referencedevice_d3d10refgdidisplaymask"></span><span id="DWORD_SOFTWARE_MICROSOFT_DIRECT3D_REFERENCEDEVICE_D3D10REFGDIDISPLAYMASK"></span>DWORD Software\\Microsoft\\Direct3D\\ReferenceDevice\\D3D10RefGdiDisplayMask  
DWORD 掩码中的每个位启用 (如果设置为 1) 或禁用 (如果设置为 0) 监视器，由引用设备控制。

<span id="DWORD_Software_Microsoft_Direct3D_ReferenceDevice_SingleThreaded"></span><span id="dword_software_microsoft_direct3d_referencedevice_singlethreaded"></span><span id="DWORD_SOFTWARE_MICROSOFT_DIRECT3D_REFERENCEDEVICE_SINGLETHREADED"></span>DWORD 软件\\Microsoft\\Direct3D\\ReferenceDevice\\SingleThreaded  
设置为 1 以启用正在运行 RefRast 单线程。

<span id="DWORD_Software_Microsoft_Direct3D_ReferenceDevice_ForceHeapAlloc"></span><span id="dword_software_microsoft_direct3d_referencedevice_forceheapalloc"></span><span id="DWORD_SOFTWARE_MICROSOFT_DIRECT3D_REFERENCEDEVICE_FORCEHEAPALLOC"></span>DWORD Software\\Microsoft\\Direct3D\\ReferenceDevice\\ForceHeapAlloc  
设置为 1，以使引用设备使用正则进程堆，与其他分配机制创建资源。

<span id="DWORD_Software_Microsoft_Direct3D_ReferenceDevice_AllowAsync"></span><span id="dword_software_microsoft_direct3d_referencedevice_allowasync"></span><span id="DWORD_SOFTWARE_MICROSOFT_DIRECT3D_REFERENCEDEVICE_ALLOWASYNC"></span>DWORD Software\\Microsoft\\Direct3D\\ReferenceDevice\\AllowAsync  
设置为 1 以允许引用设备的第二个线程，以异步方式运行 （也就是说，多个命令缓冲区允许将未完成）。

在第二个线程; 通常运行参考硬件但是，此第二个线程在主线程可以继续之前完成所有工作。

<span id="DWORD_Software_Microsoft_Direct3D_ReferenceDevice_SimulateInfinitelyFastHW"></span><span id="dword_software_microsoft_direct3d_referencedevice_simulateinfinitelyfasthw"></span><span id="DWORD_SOFTWARE_MICROSOFT_DIRECT3D_REFERENCEDEVICE_SIMULATEINFINITELYFASTHW"></span>DWORD Software\\Microsoft\\Direct3D\\ReferenceDevice\\SimulateInfinitelyFastHW  
设置为 1，以使引用设备模拟的硬件处理只有几个有限的命令使引用设备是大幅提升 （通过实质上不执行任何操作） 的外观。

作为一种性能工具，该驱动程序可以使用此密钥。

 

 





