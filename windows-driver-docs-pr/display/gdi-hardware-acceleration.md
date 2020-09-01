---
title: GDI 硬件加速
description: GDI 硬件加速
ms.assetid: 03db58e6-a6d5-4b6f-ba71-d22a985f9c57
keywords:
- 微型端口驱动程序 WDK 显示
- GDI 硬件加速 WDK 显示
- 连接和配置显示 (CCD) WDK 显示
- 带有 GDI WDK 显示的硬件加速
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ec953a79fa7f39ab17a2617636fc973ddcaecd8b
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89065828"
---
# <a name="gdi-hardware-acceleration"></a>GDI 硬件加速


Windows 7 中引入的 GDI 硬件加速功能提供了加速核心图形设备接口 (对图形处理单元 (GPU) 的 GDI) 操作。

为了指示 GPU 和驱动程序支持此功能，显示微型端口驱动程序必须将 DXGKDDI \_ 接口 \_ 版本设置为 &gt; = DXGKDDI \_ 接口 \_ 版本 \_ WIN7。

显示微型端口驱动程序还应将[**DXGK \_ PRESENTATIONCAPS**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_presentationcaps) - &gt; **SupportKernelModeCommandBuffer**设置为**TRUE** ，以指示它支持 GDI 硬件加速命令缓冲区处理。 仅当存在缓存连贯的 GPU 口径段，并且 CPU 访问 GPU 内存时，驱动程序才应报告此类型的支持。

以下参考主题介绍了如何使用此功能：

<span id="Driver-Implemented_Functions"></span><span id="driver-implemented_functions"></span><span id="DRIVER-IMPLEMENTED_FUNCTIONS"></span>**驱动程序实现的函数**  
以下函数必须通过支持 GDI 硬件加速的显示微型端口驱动程序来实现：

[**DxgkDdiCreateAllocation**](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_createallocation)

[**DxgkDdiGetStandardAllocationDriverData**](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_getstandardallocationdriverdata)

[**DxgkDdiRenderKm**](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_renderkm)

<span id="Structures"></span><span id="structures"></span><span id="STRUCTURES"></span>**结构** 
[ **D3DKM \_ TRANSPARENTBLTFLAGS**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_d3dkm_transparentbltflags)

[**D3DKMDT \_ GDISURFACEDATA**](/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_gdisurfacedata)

[**D3DKMDT \_ GDISURFACEFLAGS**](/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_gdisurfaceflags)

[**驱动程序 \_ 初始化 \_ 数据**](/windows-hardware/drivers/ddi/dispmprt/ns-dispmprt-_driver_initialization_data)

[**DXGK \_ CREATECONTEXTFLAGS**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_createcontextflags)

[**DXGK \_ CREATEDEVICEFLAGS**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_createdeviceflags)

[**DXGK \_ GDIARG \_ ALPHABLEND**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_gdiarg_alphablend)

[**DXGK \_ GDIARG \_ BITBLT**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_gdiarg_bitblt)

[**DXGK \_ GDIARG \_ CLEARTYPEBLEND**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_gdiarg_cleartypeblend)

[**DXGK \_ GDIARG \_ COLORFILL**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_gdiarg_colorfill)

[**DXGK \_ GDIARG \_ STRETCHBLT**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_gdiarg_stretchblt)

[**DXGK \_ GDIARG \_ TRANSPARENTBLT**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_gdiarg_transparentblt)

[**DXGK \_ RENDERKM \_ 命令**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_renderkm_command)

[**DXGK \_ PRESENTATIONCAPS**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_presentationcaps)

[**DXGKARG \_ GETSTANDARDALLOCATIONDRIVERDATA**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_getstandardallocationdriverdata)

[**DXGKARG \_ 呈现**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_render)

<span id="Enumerations"></span><span id="enumerations"></span><span id="ENUMERATIONS"></span>**枚举** 
[ **D3DKMDT \_ STANDARDALLOCATION \_ 类型**](/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_d3dkmdt_standardallocation_type)

[**D3DKMDT \_ GDISURFACETYPE**](/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_d3dkmdt_gdisurfacetype)

[**DXGK \_ GDIROP \_ BITBLT**](/windows-hardware/drivers/ddi/d3dkmddi/ne-d3dkmddi-_dxgk_gdirop_bitblt)

[**DXGK \_ GDIROP \_ COLORFILL**](/windows-hardware/drivers/ddi/d3dkmddi/ne-d3dkmddi-_dxgk_gdirop_colorfill)

[**DXGK \_ RENDERKM \_ 操作**](/windows-hardware/drivers/ddi/d3dkmddi/ne-d3dkmddi-_dxgk_renderkm_operation)

有关如何在显示微型端口驱动程序中实现 GDI 硬件加速的详细信息，请参阅以下主题：

[设置内存分配的大小和间距](setting-the-size-and-pitch-of-the-memory-allocation.md)

[初始化和 DMA 缓冲区创建](initialization-and-dma-buffer-creation.md)

[报告渲染操作的可选支持](reporting-optional-support-for-rendering-operations.md)

[支持内核模式命令缓冲区](supporting-kernel-mode-command-buffers.md)

[指定 GDI 硬件加速渲染操作](specifying-gdi-hardware-accelerated-rendering-operations.md)

 

