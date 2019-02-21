---
title: 设置大小和内存分配的间距
description: 设置大小和内存分配的间距
ms.assetid: babd331f-7aec-4aee-aef9-7c10b98f9181
keywords:
- 内存分配 WDK 显示
- 分配的内存 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eb189d800a37b48433c19afd339334ec72d12d98
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523937"
---
# <a name="setting-the-size-and-pitch-of-the-memory-allocation"></a>设置大小和内存分配的间距


## <span id="ddk_introduction_to_command_and_dma_buffers_gg"></span><span id="DDK_INTRODUCTION_TO_COMMAND_AND_DMA_BUFFERS_GG"></span>


处理以下的分配调用时，支持 GDI 硬件加速的显示微型端口驱动程序应设置的大小和间距的系统或视频内存的分配。

<span id="DxgkDdiCreateAllocation"></span><span id="dxgkddicreateallocation"></span><span id="DXGKDDICREATEALLOCATION"></span>[**DxgkDdiCreateAllocation**](https://msdn.microsoft.com/library/windows/hardware/ff559606)  
当驱动程序处理对调用*DxgkDdiCreateAllocation*，它应设置大小，以字节为单位的系统或视频内存分配。 通过设置分配的大小[ **pCreateAllocation** ](https://msdn.microsoft.com/library/windows/hardware/ff557559) *- &gt;* [ **pAllocationInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff560960) <em>- &gt;</em>**大小**成员。 如果分配给 CPU 可见，大小应包括间距值，该值是图面，包括填充，以字节为单位的宽度。

分配是对 CPU 可见如果[ **pGetStandardAllocationDriverData** ](https://msdn.microsoft.com/library/windows/hardware/ff557598) *-* &gt; [ **pCreateGdiSurfaceData**](https://msdn.microsoft.com/library/windows/hardware/ff546021)<em>-&gt;</em>**类型**成员设置为 D3DKMDT\_GDISURFACE\_暂存\_CPUVISIBLE 或 D3DKMDT\_GDISURFACE\_EXISTINGSYSMEM。 这些图面上的类型的属性，请参阅中的说明[ **D3DKMDT\_GDISURFACETYPE**](https://msdn.microsoft.com/library/windows/hardware/ff546039)。

<span id="DxgkDdiGetStandardAllocationDriverData"></span><span id="dxgkddigetstandardallocationdriverdata"></span><span id="DXGKDDIGETSTANDARDALLOCATIONDRIVERDATA"></span>[**DxgkDdiGetStandardAllocationDriverData**](https://msdn.microsoft.com/library/windows/hardware/ff559673)  
当驱动程序处理对调用*DxgkDdiGetStandardAllocationDriverData*对 CPU 是可见的分配时，它应：

1.  设置[ **pGetStandardAllocationDriverData**](https://msdn.microsoft.com/library/windows/hardware/ff557598)*-*&gt;[**StandardAllocationType**](https://msdn.microsoft.com/library/windows/hardware/ff546589)成员添加到 D3DKMDT\_STANDARDALLOCATION\_GDISURFACE。

2.  设置的说明可用于通过 GDI 硬件加速并通过桌面 Windows 管理器 (DWM) 重定向图面[ **D3DKMDT\_GDISURFACEDATA** ](https://msdn.microsoft.com/library/windows/hardware/ff546021)结构通过指向[ **pGetStandardAllocationDriverData**](https://msdn.microsoft.com/library/windows/hardware/ff557598)*-*&gt;**pCreateGdiSurfaceData**成员。 例如，设置通过分配的音调**间距**D3DKMDT 成员\_GDISURFACEDATA。

 

 





