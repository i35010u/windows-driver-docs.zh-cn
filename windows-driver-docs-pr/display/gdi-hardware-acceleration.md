---
title: GDI 硬件加速
description: GDI 硬件加速
ms.assetid: 03db58e6-a6d5-4b6f-ba71-d22a985f9c57
keywords:
- 微型端口驱动程序 WDK 显示
- GDI 硬件加速 WDK 显示
- 连接和配置显示 (CCD) WDK 显示
- 带有 GDI WDK 显示硬件加速
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7755e6dd1cd415b0388e22875e893b896f614de8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354743"
---
# <a name="gdi-hardware-acceleration"></a>GDI 硬件加速


与 Windows 7 中引入的 GDI 硬件加速功能提供加速的核心图形设备接口 (GDI) 在图形处理单元 (GPU) 上的操作。

若要指示 GPU 和驱动程序支持此功能，显示微型端口驱动程序必须设置 DXGKDDI\_接口\_版本&gt;= DXGKDDI\_接口\_版本\_WIN7。

显示微型端口驱动程序还应设置[ **DXGK\_PRESENTATIONCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_presentationcaps)-&gt;**SupportKernelModeCommandBuffer**向 **，则返回 TRUE**以指示它支持 GDI 硬件加速命令缓冲区处理。 仅当缓存连贯的 GPU aperture 段存在并且没有任何显著的性能损失 CPU 访问 GPU 内存时，该驱动程序应报告这种类型的支持。

以下参考主题介绍如何使用此功能：

<span id="Driver-Implemented_Functions"></span><span id="driver-implemented_functions"></span><span id="DRIVER-IMPLEMENTED_FUNCTIONS"></span>**驱动程序实现函数**  
支持 GDI 硬件加速的显示微型端口驱动程序必须实现以下函数：

[**DxgkDdiCreateAllocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_createallocation)

[**DxgkDdiGetStandardAllocationDriverData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_getstandardallocationdriverdata)

[**DxgkDdiRenderKm**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_renderkm)

<span id="Structures"></span><span id="structures"></span><span id="STRUCTURES"></span>**结构**
[**D3DKM\_TRANSPARENTBLTFLAGS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_d3dkm_transparentbltflags)

[**D3DKMDT\_GDISURFACEDATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmdt/ns-d3dkmdt-_d3dkmdt_gdisurfacedata)

[**D3DKMDT\_GDISURFACEFLAGS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmdt/ns-d3dkmdt-_d3dkmdt_gdisurfaceflags)

[**DRIVER\_INITIALIZATION\_DATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/ns-dispmprt-_driver_initialization_data)

[**DXGK\_CREATECONTEXTFLAGS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_createcontextflags)

[**DXGK\_CREATEDEVICEFLAGS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_createdeviceflags)

[**DXGK\_GDIARG\_ALPHABLEND**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_gdiarg_alphablend)

[**DXGK\_GDIARG\_BITBLT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_gdiarg_bitblt)

[**DXGK\_GDIARG\_CLEARTYPEBLEND**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_gdiarg_cleartypeblend)

[**DXGK\_GDIARG\_COLORFILL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_gdiarg_colorfill)

[**DXGK\_GDIARG\_STRETCHBLT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_gdiarg_stretchblt)

[**DXGK\_GDIARG\_TRANSPARENTBLT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_gdiarg_transparentblt)

[**DXGK\_RENDERKM\_命令**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_renderkm_command)

[**DXGK\_PRESENTATIONCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_presentationcaps)

[**DXGKARG\_GETSTANDARDALLOCATIONDRIVERDATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgkarg_getstandardallocationdriverdata)

[**DXGKARG\_呈现**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgkarg_render)

<span id="Enumerations"></span><span id="enumerations"></span><span id="ENUMERATIONS"></span>**枚举**
[**D3DKMDT\_STANDARDALLOCATION\_类型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmdt/ne-d3dkmdt-_d3dkmdt_standardallocation_type)

[**D3DKMDT\_GDISURFACETYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmdt/ne-d3dkmdt-_d3dkmdt_gdisurfacetype)

[**DXGK\_GDIROP\_BITBLT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ne-d3dkmddi-_dxgk_gdirop_bitblt)

[**DXGK\_GDIROP\_COLORFILL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ne-d3dkmddi-_dxgk_gdirop_colorfill)

[**DXGK\_RENDERKM\_操作**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ne-d3dkmddi-_dxgk_renderkm_operation)

有关如何在显示的微型端口驱动程序中实现 GDI 硬件加速的更多详细信息，请参阅以下主题：

[设置大小和内存分配的间距](setting-the-size-and-pitch-of-the-memory-allocation.md)

[DMA 缓冲区创建和初始化](initialization-and-dma-buffer-creation.md)

[适用于呈现操作的报告的可选支持](reporting-optional-support-for-rendering-operations.md)

[支持的内核模式命令缓冲区](supporting-kernel-mode-command-buffers.md)

[指定 GDI 硬件加速的呈现操作](specifying-gdi-hardware-accelerated-rendering-operations.md)

 

 





