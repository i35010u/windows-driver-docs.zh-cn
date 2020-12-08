---
title: 初始化和 DMA 缓冲区创建
description: 初始化和 DMA 缓冲区创建
keywords:
- DMA 缓冲 WDK 显示，为 GDI 硬件加速创建
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5e115793c8289dfd99ff5a5c0772d834be1d084c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839305"
---
# <a name="initialization-and-dma-buffer-creation"></a>初始化和 DMA 缓冲区创建


## <span id="ddk_introduction_to_command_and_dma_buffers_gg"></span><span id="DDK_INTRODUCTION_TO_COMMAND_AND_DMA_BUFFERS_GG"></span>


若要指示 GPU 支持 GDI 硬件加速，则 [**DriverEntry**](./driverentry-of-display-miniport-driver.md)函数的显示微型端口驱动程序的实现必须使用指向驱动程序实现的 [**DxgkDdiRenderKm**](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_renderkm)函数的指针填充 [**驱动程序 \_ 初始化 \_ 数据**](/windows-hardware/drivers/ddi/dispmprt/ns-dispmprt-_driver_initialization_data)结构的 **DxgkDdiRenderKm** 成员。

DirectX 图形内核子系统将调用 *DxgkDdiRenderKm* 函数，以便从由操作系统提供的内核模式规范显示驱动程序 (CDD) 传递的命令缓冲区生成 DMA 缓冲区。

当 DirectX 图形内核子系统的显示端口驱动程序 (*Dxgkrnl.sys*) 调用 [**DxgkDdiCreateContext**](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_createcontext)函数时，它会将 [**pCreateContext**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_createcontext) - &gt; [**Flags**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_createcontextflags) - &gt; **GdiContext** 成员设置为指示用于 GDI 硬件加速的上下文。

同样，当显示端口驱动程序调用 [**DxgkDdiCreateDevice**](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_createdevice)函数时，它会将 [**pCreateDevice**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_createdevice) - &gt; [**Flags**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_createdeviceflags) - &gt; **GdiDevice** 成员设置为指示用于 GDI 硬件加速的设备。

 

