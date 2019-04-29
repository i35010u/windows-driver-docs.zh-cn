---
title: VGA 兼容的微型端口驱动程序的 HwVidStartIO
description: VGA 兼容的微型端口驱动程序的 HwVidStartIO
ms.assetid: e5a81f87-b220-4497-aed3-8c4d08504340
keywords:
- 微型端口驱动程序 WDK Windows 2000 中，VGA、 HwVidStartIO
- VGA WDK 视频微型端口 HwVidStartIO
- HwVidStartIO
- 不兼容的 VGA 视频微型端口驱动程序 WDK
- SVGA WDK 微型端口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8c7cf64a18633bbba8aaf664a794a34a3f53d697
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354830"
---
# <a name="vga-compatible-miniport-drivers-hwvidstartio"></a>VGA 兼容的微型端口驱动程序的 HwVidStartIO


## <span id="ddk_vga_compatible_miniport_driver_s_hwvidstartio_gg"></span><span id="DDK_VGA_COMPATIBLE_MINIPORT_DRIVER_S_HWVIDSTARTIO_GG"></span>


当用户切换回在窗口中，运行兼容的 VGA 的微型端口驱动程序的一个全屏幕 MS-DOS 应用程序*HwVidStartIO* i/o 控制代码 IOCTL\_视频\_保存\_硬件\_状态。 在用户切换到全屏模式下一次应用程序的情况下，微型端口驱动程序必须存储适配器的状态。

请注意，微型端口驱动程序*SvgaHwIoPortXxx*函数可能会缓冲一系列应用程序**IN**s 和/或**OUT**s，如中所述[验证说明中 SvgaHwIoPortXxx](validating-instructions-in-svgahwioportxxx.md)，当其*HwVidStartIO*函数调用以保存适配器状态。 微型端口驱动程序应在这些情况下，保存当前状态，包括缓冲的说明，以便*SvgaHwIoPortXxx*函数可以继续执行完全上次退出的位置如果用户的验证操作切换到全屏模式下一次应用程序。

微型端口驱动程序完成保存操作，端口驱动程序会自动禁用用于当前 IOPM *VDM*s 和微型端口驱动程序*SvgaHwIoPortXxx*函数。 如果应用程序再次切换到全屏模式的视频端口驱动程序会自动还原 IOPM。 它还会继续调用微型端口驱动程序*SvgaHwIoPortXxx*后它会调用微型端口驱动程序的正常*HwVidStartIO*函数和 IOCTL\_视频\_还原\_硬件\_状态请求。

 

 





