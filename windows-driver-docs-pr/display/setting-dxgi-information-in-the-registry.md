---
title: 在注册表中设置 DXGI 信息
description: 在注册表中设置 DXGI 信息
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 534fd0c50d64c19fc08521e73f7381a0540a78d2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96818595"
---
# <a name="setting-dxgi-information-in-the-registry"></a>在注册表中设置 DXGI 信息


DXGI 和参考光栅使用以下注册表项：

<span id="DWORD_Software_Microsoft_DXGI_DisableFullscreenWatchdog"></span><span id="dword_software_microsoft_dxgi_disablefullscreenwatchdog"></span><span id="DWORD_SOFTWARE_MICROSOFT_DXGI_DISABLEFULLSCREENWATCHDOG"></span>DWORD Software \\ Microsoft \\ DXGI \\ DisableFullscreenWatchdog  
设置为1可禁用监视程序线程。

<span id="DWORD_Software_Microsoft_Direct3D_ReferenceDevice_FlushOften"></span><span id="dword_software_microsoft_direct3d_referencedevice_flushoften"></span><span id="DWORD_SOFTWARE_MICROSOFT_DIRECT3D_REFERENCEDEVICE_FLUSHOFTEN"></span>DWORD Software \\ Microsoft \\ Direct3D \\ ReferenceDevice \\ FlushOften  
设置为1则通常刷新。

<span id="DWORD_Software_Microsoft_Direct3D_ReferenceDevice_FenceEachEntryPoint"></span><span id="dword_software_microsoft_direct3d_referencedevice_fenceeachentrypoint"></span><span id="DWORD_SOFTWARE_MICROSOFT_DIRECT3D_REFERENCEDEVICE_FENCEEACHENTRYPOINT"></span>DWORD Software \\ Microsoft \\ Direct3D \\ ReferenceDevice \\ FenceEachEntryPoint  
设置为1，使每个调用都使用 GPU 进行 DDI 功能防护。 带 GPU 的防护是指刷新命令批处理，并在 GPU 空闲之前进行阻止。

<span id="DWORD_Software_Microsoft_Direct3D_ReferenceDevice_Debug"></span><span id="dword_software_microsoft_direct3d_referencedevice_debug"></span><span id="DWORD_SOFTWARE_MICROSOFT_DIRECT3D_REFERENCEDEVICE_DEBUG"></span>DWORD Software \\ Microsoft \\ Direct3D \\ ReferenceDevice \\ 调试  
设置为1以：

-   通常使用 GPU 进行刷新，并使每次调用 DDI 功能防护。

-   在单线程)  (RefRast 中运行参考光栅化。

<span id="DWORD_Software_Microsoft_Direct3D_ReferenceDevice_D3D10RefGdiDisplayMask"></span><span id="dword_software_microsoft_direct3d_referencedevice_d3d10refgdidisplaymask"></span><span id="DWORD_SOFTWARE_MICROSOFT_DIRECT3D_REFERENCEDEVICE_D3D10REFGDIDISPLAYMASK"></span>DWORD Software \\ Microsoft \\ Direct3D \\ ReferenceDevice \\ D3D10RefGdiDisplayMask  
如果设置为) 1，则 DWORD 掩码中的每一位都将启用 (; 如果设置为) 0，则会禁用 (，这是由引用设备控制的。

<span id="DWORD_Software_Microsoft_Direct3D_ReferenceDevice_SingleThreaded"></span><span id="dword_software_microsoft_direct3d_referencedevice_singlethreaded"></span><span id="DWORD_SOFTWARE_MICROSOFT_DIRECT3D_REFERENCEDEVICE_SINGLETHREADED"></span>DWORD Software \\ Microsoft \\ Direct3D \\ ReferenceDevice \\ SingleThreaded  
设置为1以启用运行 RefRast 单线程。

<span id="DWORD_Software_Microsoft_Direct3D_ReferenceDevice_ForceHeapAlloc"></span><span id="dword_software_microsoft_direct3d_referencedevice_forceheapalloc"></span><span id="DWORD_SOFTWARE_MICROSOFT_DIRECT3D_REFERENCEDEVICE_FORCEHEAPALLOC"></span>DWORD Software \\ Microsoft \\ Direct3D \\ ReferenceDevice \\ ForceHeapAlloc  
设置为1以使引用设备使用常规进程堆创建资源，而不是使用其他分配机制。

<span id="DWORD_Software_Microsoft_Direct3D_ReferenceDevice_AllowAsync"></span><span id="dword_software_microsoft_direct3d_referencedevice_allowasync"></span><span id="DWORD_SOFTWARE_MICROSOFT_DIRECT3D_REFERENCEDEVICE_ALLOWASYNC"></span>DWORD Software \\ Microsoft \\ Direct3D \\ ReferenceDevice \\ AllowAsync  
如果设置为1，则允许引用设备的第二个线程以异步方式运行 (也就是说，允许多个命令缓冲区) 完成。

引用硬件通常在另一个线程中运行;但是，第二个线程完成其所有工作，主线程才能继续。

<span id="DWORD_Software_Microsoft_Direct3D_ReferenceDevice_SimulateInfinitelyFastHW"></span><span id="dword_software_microsoft_direct3d_referencedevice_simulateinfinitelyfasthw"></span><span id="DWORD_SOFTWARE_MICROSOFT_DIRECT3D_REFERENCEDEVICE_SIMULATEINFINITELYFASTHW"></span>DWORD Software \\ Microsoft \\ Direct3D \\ ReferenceDevice \\ SimulateInfinitelyFastHW  
如果设置为1，则引用设备的模拟硬件进程只需几个有限的命令，使引用设备在本质上 (完全不) 。

驱动程序可以将此密钥用作性能工具。

 

 





