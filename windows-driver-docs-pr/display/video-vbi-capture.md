---
title: 视频 VBI 捕获
description: 视频 VBI 捕获
ms.assetid: 40544838-8678-4832-8e6f-e96202f987ad
keywords:
- 视频 VBI 捕获 WDK DirectDraw
- 消隐 WDK DirectDraw
- VBI WDK DirectDraw
- DxTransfer
- DxApi 微型端口驱动程序 WDK DirectDraw，VBI 捕获
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cd0696abed9b168383c9b79bc2482eac763f7069
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372615"
---
# <a name="video-vbi-capture"></a>视频 VBI 捕获


## <span id="ddk_video_vbi_capture_gg"></span><span id="DDK_VIDEO_VBI_CAPTURE_GG"></span>


DirectX 5.2 引入了两个视频的垂直遮蔽间隔 (VBI) 捕获的 DirectDraw 驱动程序函数。 这些函数是[ *DxTransfer* ](https://docs.microsoft.com/windows/desktop/api/dxmini/nc-dxmini-pdx_transfer)并[ *DxGetTransferStatus*](https://docs.microsoft.com/windows/desktop/api/dxmini/nc-dxmini-pdx_gettransferstatus)。

*DxTransfer*函数有利于视频和 VBI 捕获。 因为在 IRQ 时调用此函数时，它必须尽快返回。 如果显示硬件未准备好时不要总线主控*DxTransfer*调用，则微型端口驱动程序应保留内部队列的总线主机数 (总线母版保存到队列中的实际数目最多是驱动程序开发人员）。 这样，硬件准备就绪后执行总线 master 的硬件。 换而言之，驱动程序不应轮询和等待总线 master 完成。

当调用 DirectDraw *DxTransfer*函数，它会提供中的传输 ID **dwTransferID**的成员[ **DDTRANSFERININFO** ](https://docs.microsoft.com/windows/desktop/api/dxmini/ns-dxmini-_ddtransferininfo)结构。 微型端口驱动程序然后可以使用此标识时*DxGetTransferStatus*调用函数。

总线 master 完成后，显示硬件必须生成一个 IRQ。 然后，微型端口驱动程序必须调用[ **IRQCallback** ](https://docs.microsoft.com/windows/desktop/api/dxmini/nc-dxmini-pdx_irqcallback)函数中指定[ *DxEnableIRQ*](https://docs.microsoft.com/windows/desktop/api/dxmini/nc-dxmini-pdx_enableirq)。 在此**IRQCallback**调用，微型端口驱动程序指定 DDIRQ\_总线主控标志。 然后调用 DirectDraw [ *DxGetTransferStatus* ](https://docs.microsoft.com/windows/desktop/api/dxmini/nc-dxmini-pdx_gettransferstatus)函数来确定哪些总线 master 已完成。 微型端口驱动程序必须返回传输 ID (**dwTransferID**) 中早期传递给驱动程序的 DirectDraw *DxTransfer*调用。 这样一来，如果该驱动程序在队列中，有五个总线主机 DirectDraw 可以确定哪一个最近完成。

 

 





