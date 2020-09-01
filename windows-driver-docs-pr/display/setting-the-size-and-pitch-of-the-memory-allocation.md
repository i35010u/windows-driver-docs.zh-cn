---
title: 设置内存分配的大小和间距
description: 设置内存分配的大小和间距
ms.assetid: babd331f-7aec-4aee-aef9-7c10b98f9181
keywords:
- 内存分配 WDK 显示
- 分配内存 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 45a1db0781ef537ff18a9a34da15cd4e1c38c601
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89065996"
---
# <a name="setting-the-size-and-pitch-of-the-memory-allocation"></a>设置内存分配的大小和间距


## <span id="ddk_introduction_to_command_and_dma_buffers_gg"></span><span id="DDK_INTRODUCTION_TO_COMMAND_AND_DMA_BUFFERS_GG"></span>


支持 GDI 硬件加速的显示微型端口驱动程序应在处理以下分配调用时设置系统或视频内存分配的大小和间距。

<span id="DxgkDdiCreateAllocation"></span><span id="dxgkddicreateallocation"></span><span id="DXGKDDICREATEALLOCATION"></span>[**DxgkDdiCreateAllocation**](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_createallocation)  
当驱动程序处理对 *DxgkDdiCreateAllocation*的调用时，它应设置系统或视频内存分配的大小（以字节为单位）。 分配的大小通过[**pCreateAllocation**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_createallocation) *-&gt;* [**pAllocationInfo**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_allocationinfo) <em>-&gt;</em> **size**成员设置。 如果分配对 CPU 可见，则大小应包含螺距值，它是图面的宽度（包括边距）（以字节为单位）。

如果将[**pGetStandardAllocationDriverData**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_getstandardallocationdriverdata) *-* &gt; [**pCreateGdiSurfaceData**](/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_gdisurfacedata) <em>-&gt;</em> **类型**成员设置为 D3DKMDT \_ GDISURFACE \_ 暂存 \_ CPUVISIBLE 或 D3DKMDT \_ GDISURFACE \_ EXISTINGSYSMEM，则分配对 CPU 可见。 有关这些表面类型的属性，请参阅 [**D3DKMDT \_ GDISURFACETYPE**](/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_d3dkmdt_gdisurfacetype)中的说明。

<span id="DxgkDdiGetStandardAllocationDriverData"></span><span id="dxgkddigetstandardallocationdriverdata"></span><span id="DXGKDDIGETSTANDARDALLOCATIONDRIVERDATA"></span>[**DxgkDdiGetStandardAllocationDriverData**](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_getstandardallocationdriverdata)  
当驱动程序为对 CPU 可见的分配处理对 *DxgkDdiGetStandardAllocationDriverData* 的调用时，应执行以下操作：

1.  将[**pGetStandardAllocationDriverData**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_getstandardallocationdriverdata) *-* &gt; [**StandardAllocationType**](/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_d3dkmdt_standardallocation_type)成员设置为 D3DKMDT \_ STANDARDALLOCATION \_ GDISURFACE。

2.  设置可用于通过 GDI 硬件加速重定向的图面的说明，以及通过[**pGetStandardAllocationDriverData**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_getstandardallocationdriverdata)pCreateGdiSurfaceData 成员指向的[**D3DKMDT \_ GDISURFACEDATA**](/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_gdisurfacedata)结构的桌面 Windows Manager (DWM) 的说明 *-* &gt; **pCreateGdiSurfaceData** 。 例如，通过 D3DKMDT GDISURFACEDATA 的 **螺距** 成员设置分配的跨度 \_ 。

 

