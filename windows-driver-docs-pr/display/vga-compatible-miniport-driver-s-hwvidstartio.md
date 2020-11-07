---
title: VGA 兼容的微型端口驱动程序的 HwVidStartIO
description: VGA 兼容的微型端口驱动程序的 HwVidStartIO
ms.assetid: e5a81f87-b220-4497-aed3-8c4d08504340
keywords:
- 视频微型端口驱动程序 WDK Windows 2000、VGA、HwVidStartIO
- VGA WDK 视频微型端口，HwVidStartIO
- HwVidStartIO
- 非 VGA 兼容视频微型端口驱动程序 WDK
- SVGA WDK 视频微型端口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1b3375343b694c4dbe2afa7d6822bcfed6e8d582
ms.sourcegitcommit: a44ade167cdfb541cf1818e9f9e3726f23f90b66
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/07/2020
ms.locfileid: "94361431"
---
# <a name="vga-compatible-miniport-drivers-hwvidstartio"></a>VGA 兼容的微型端口驱动程序的 HwVidStartIO


## <span id="ddk_vga_compatible_miniport_driver_s_hwvidstartio_gg"></span><span id="DDK_VGA_COMPATIBLE_MINIPORT_DRIVER_S_HWVIDSTARTIO_GG"></span>


当用户将全屏 MS-DOS 应用程序切换回在窗口中运行时， *会向 VGA* 兼容的微型端口驱动程序的 [*HwVidStartIO*](/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_start_io)函数发送 I/o 控制代码 IOCTL \_ 视频 \_ 保存 \_ 硬件 \_ 状态。 小型端口驱动程序必须存储适配器的状态，以防用户再次将应用程序切换到全屏模式。

请注意，微型端口驱动程序的 *SvgaHwIoPortXxx* 函数可能已 **在** s 和/或 **OUT** 中缓冲了一系列应用程序，如在 [SvgaHwIoPortXxx 中验证指令](validating-instructions-in-svgahwioportxxx.md)中所述，当调用其 *HwVidStartIO* 函数以保存适配器状态时，将在其中进行说明。 在这些情况下，微型端口驱动程序应保存当前状态（包括缓冲指令），以便在用户再次将应用程序切换到全屏模式时， *SvgaHwIoPortXxx* 函数可以从中断的位置继续执行验证操作。

当微型端口驱动程序完成保存操作时，端口驱动程序会自动禁用 *VDM* 的当前 IOPM 和微型端口驱动程序的 *SvgaHwIoPortXxx* 函数。 如果应用程序再次切换到全屏模式，视频端口驱动程序会自动还原 IOPM。 它在调用微型端口驱动程序的 *HwVidStartIO* 函数和 IOCTL *SvgaHwIoPortXxx* \_ 视频 \_ 还原 \_ 硬件 \_ 状态请求后，还会继续调用微型端口驱动程序的 SvgaHwIoPortXxx 函数。

 

