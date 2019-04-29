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
ms.openlocfilehash: 7a6ec582440317c85574b81987c5405065f3366f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363848"
---
# <a name="gdi-hardware-acceleration"></a>GDI 硬件加速


与 Windows 7 中引入的 GDI 硬件加速功能提供加速的核心图形设备接口 (GDI) 在图形处理单元 (GPU) 上的操作。

若要指示 GPU 和驱动程序支持此功能，显示微型端口驱动程序必须设置 DXGKDDI\_接口\_版本&gt;= DXGKDDI\_接口\_版本\_WIN7。

显示微型端口驱动程序还应设置[ **DXGK\_PRESENTATIONCAPS**](https://msdn.microsoft.com/library/windows/hardware/ff562004)-&gt;**SupportKernelModeCommandBuffer**向 **，则返回 TRUE**以指示它支持 GDI 硬件加速命令缓冲区处理。 仅当缓存连贯的 GPU aperture 段存在并且没有任何显著的性能损失 CPU 访问 GPU 内存时，该驱动程序应报告这种类型的支持。

以下参考主题介绍如何使用此功能：

<span id="Driver-Implemented_Functions"></span><span id="driver-implemented_functions"></span><span id="DRIVER-IMPLEMENTED_FUNCTIONS"></span>**驱动程序实现函数**  
支持 GDI 硬件加速的显示微型端口驱动程序必须实现以下函数：

[**DxgkDdiCreateAllocation**](https://msdn.microsoft.com/library/windows/hardware/ff559606)

[**DxgkDdiGetStandardAllocationDriverData**](https://msdn.microsoft.com/library/windows/hardware/ff559673)

[**DxgkDdiRenderKm**](https://msdn.microsoft.com/library/windows/hardware/ff559800)

<span id="Structures"></span><span id="structures"></span><span id="STRUCTURES"></span>**结构**
[**D3DKM\_TRANSPARENTBLTFLAGS**](https://msdn.microsoft.com/library/windows/hardware/ff548468)

[**D3DKMDT\_GDISURFACEDATA**](https://msdn.microsoft.com/library/windows/hardware/ff546021)

[**D3DKMDT\_GDISURFACEFLAGS**](https://msdn.microsoft.com/library/windows/hardware/ff546031)

[**DRIVER\_INITIALIZATION\_DATA**](https://msdn.microsoft.com/library/windows/hardware/ff556169)

[**DXGK\_CREATECONTEXTFLAGS**](https://msdn.microsoft.com/library/windows/hardware/ff561037)

[**DXGK\_CREATEDEVICEFLAGS**](https://msdn.microsoft.com/library/windows/hardware/ff561039)

[**DXGK\_GDIARG\_ALPHABLEND**](https://msdn.microsoft.com/library/windows/hardware/ff561074)

[**DXGK\_GDIARG\_BITBLT**](https://msdn.microsoft.com/library/windows/hardware/ff561079)

[**DXGK\_GDIARG\_CLEARTYPEBLEND**](https://msdn.microsoft.com/library/windows/hardware/ff561082)

[**DXGK\_GDIARG\_COLORFILL**](https://msdn.microsoft.com/library/windows/hardware/ff561083)

[**DXGK\_GDIARG\_STRETCHBLT**](https://msdn.microsoft.com/library/windows/hardware/ff561089)

[**DXGK\_GDIARG\_TRANSPARENTBLT**](https://msdn.microsoft.com/library/windows/hardware/ff561091)

[**DXGK\_RENDERKM\_命令**](https://msdn.microsoft.com/library/windows/hardware/ff562026)

[**DXGK\_PRESENTATIONCAPS**](https://msdn.microsoft.com/library/windows/hardware/ff562004)

[**DXGKARG\_GETSTANDARDALLOCATIONDRIVERDATA**](https://msdn.microsoft.com/library/windows/hardware/ff557598)

[**DXGKARG\_呈现**](https://msdn.microsoft.com/library/windows/hardware/ff557648)

<span id="Enumerations"></span><span id="enumerations"></span><span id="ENUMERATIONS"></span>**枚举**
[**D3DKMDT\_STANDARDALLOCATION\_类型**](https://msdn.microsoft.com/library/windows/hardware/ff546589)

[**D3DKMDT\_GDISURFACETYPE**](https://msdn.microsoft.com/library/windows/hardware/ff546039)

[**DXGK\_GDIROP\_BITBLT**](https://msdn.microsoft.com/library/windows/hardware/ff561095)

[**DXGK\_GDIROP\_COLORFILL**](https://msdn.microsoft.com/library/windows/hardware/ff561102)

[**DXGK\_RENDERKM\_操作**](https://msdn.microsoft.com/library/windows/hardware/ff562029)

有关如何在显示的微型端口驱动程序中实现 GDI 硬件加速的更多详细信息，请参阅以下主题：

[设置大小和内存分配的间距](setting-the-size-and-pitch-of-the-memory-allocation.md)

[DMA 缓冲区创建和初始化](initialization-and-dma-buffer-creation.md)

[适用于呈现操作的报告的可选支持](reporting-optional-support-for-rendering-operations.md)

[支持的内核模式命令缓冲区](supporting-kernel-mode-command-buffers.md)

[指定 GDI 硬件加速的呈现操作](specifying-gdi-hardware-accelerated-rendering-operations.md)

 

 





