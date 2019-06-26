---
title: 初始化和 DMA 缓冲区创建
description: 初始化和 DMA 缓冲区创建
ms.assetid: d84aed8a-9e22-4172-89c2-807b4e06108f
keywords:
- DMA 缓冲区 WDK 显示创建的 GDI 硬件加速
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c6783098afb47a38f8ee517a47c27cc4347a7844
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385197"
---
# <a name="initialization-and-dma-buffer-creation"></a>初始化和 DMA 缓冲区创建


## <span id="ddk_introduction_to_command_and_dma_buffers_gg"></span><span id="DDK_INTRODUCTION_TO_COMMAND_AND_DMA_BUFFERS_GG"></span>


若要指示 GPU 支持 GDI 硬件加速，显示微型端口驱动程序的实现[ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/display/driverentry-of-display-miniport-driver)函数必须填写**DxgkDdiRenderKm**的成员[**驱动程序\_初始化\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/ns-dispmprt-_driver_initialization_data)用一个指针指向由驱动程序实现的结构[ **DxgkDdiRenderKm** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_renderkm)函数。

DirectX 图形内核子系统调用*DxgkDdiRenderKm*函数以生成从传递由内核模式规范显示驱动程序 (CDD) 由操作系统提供的命令缓冲区 DMA 缓冲区。

当显示端口的 DirectX 图形内核子系统的驱动程序 (*Dxgkrnl.sys*) 调用[ **DxgkDdiCreateContext** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_createcontext)函数，它设置[**pCreateContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgkarg_createcontext)-&gt;[**标志**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_createcontextflags) - &gt; **GdiContext**成员以指示用于 GDI 硬件加速的上下文。

同样，当显示端口驱动程序调用[ **DxgkDdiCreateDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_createdevice)函数，它设置[ **pCreateDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgkarg_createdevice) - &gt; [**标志**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_createdeviceflags)-&gt;**GdiDevice**成员以指示用于 GDI 硬件的设备加速。

 

 





