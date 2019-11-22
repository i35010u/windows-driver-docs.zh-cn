---
title: 设置内存分配的大小和间距
description: 设置内存分配的大小和间距
ms.assetid: babd331f-7aec-4aee-aef9-7c10b98f9181
keywords:
- 内存分配 WDK 显示
- 分配内存 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3437ad0257932ac02b7893c19cf14ac0d0e5a46e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829496"
---
# <a name="setting-the-size-and-pitch-of-the-memory-allocation"></a>设置内存分配的大小和间距


## <span id="ddk_introduction_to_command_and_dma_buffers_gg"></span><span id="DDK_INTRODUCTION_TO_COMMAND_AND_DMA_BUFFERS_GG"></span>


支持 GDI 硬件加速的显示微型端口驱动程序应在处理以下分配调用时设置系统或视频内存分配的大小和间距。

<span id="DxgkDdiCreateAllocation"></span><span id="dxgkddicreateallocation"></span><span id="DXGKDDICREATEALLOCATION"></span>[**DxgkDdiCreateAllocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_createallocation)  
当驱动程序处理对*DxgkDdiCreateAllocation*的调用时，它应设置系统或视频内存分配的大小（以字节为单位）。 分配的大小通过[**pCreateAllocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_createallocation) *-&gt;* [**pAllocationInfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_allocationinfo) <em>-&gt;</em>**大小**成员设置。 如果分配对 CPU 可见，则大小应包含螺距值，它是图面的宽度（包括边距）（以字节为单位）。

如果[**pGetStandardAllocationDriverData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_getstandardallocationdriverdata) *-* &gt;[**pCreateGdiSurfaceData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_gdisurfacedata) <em>-&gt;</em>**类型**成员的类型成员设置为 D3DKMDT\_GDISURFACE，则会对 CPU 显示分配\_暂存\_CPUVISIBLE 或 D3DKMDT\_GDISURFACE\_EXISTINGSYSMEM。 有关这些表面类型的属性，请参阅[**D3DKMDT\_GDISURFACETYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_d3dkmdt_gdisurfacetype)中的说明。

<span id="DxgkDdiGetStandardAllocationDriverData"></span><span id="dxgkddigetstandardallocationdriverdata"></span><span id="DXGKDDIGETSTANDARDALLOCATIONDRIVERDATA"></span>[**DxgkDdiGetStandardAllocationDriverData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_getstandardallocationdriverdata)  
当驱动程序为对 CPU 可见的分配处理对*DxgkDdiGetStandardAllocationDriverData*的调用时，应执行以下操作：

1.  将[**pGetStandardAllocationDriverData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_getstandardallocationdriverdata) *-* &gt;[**StandardAllocationType**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_d3dkmdt_standardallocation_type)成员设置为 D3DKMDT\_STANDARDALLOCATION\_GDISURFACE。

2.  通过[**pGetStandardAllocationDriverData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_getstandardallocationdriverdata) *-* &gt;**pCreateGdiSurfaceData**成员指向的[**D3DKMDT\_GDISURFACEDATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_gdisurfacedata)结构，设置可用于通过 GDI 硬件加速和桌面 Windows 管理器（DWM）进行重定向的图面描述。 例如，通过 D3DKMDT\_GDISURFACEDATA 的**螺距**成员设置分配的跨度。

 

 





