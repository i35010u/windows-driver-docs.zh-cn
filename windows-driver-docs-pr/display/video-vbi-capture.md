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
ms.openlocfilehash: ee21f6f16ba94d2977806c51fae6fbb820ec9078
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63365056"
---
# <a name="video-vbi-capture"></a>视频 VBI 捕获


## <span id="ddk_video_vbi_capture_gg"></span><span id="DDK_VIDEO_VBI_CAPTURE_GG"></span>


DirectX 5.2 引入了两个视频的垂直遮蔽间隔 (VBI) 捕获的 DirectDraw 驱动程序函数。 这些函数是[ *DxTransfer* ](https://msdn.microsoft.com/library/windows/hardware/ff562887)并[ *DxGetTransferStatus*](https://msdn.microsoft.com/library/windows/hardware/ff557438)。

*DxTransfer*函数有利于视频和 VBI 捕获。 因为在 IRQ 时调用此函数时，它必须尽快返回。 如果显示硬件未准备好时不要总线主控*DxTransfer*调用，则微型端口驱动程序应保留内部队列的总线主机数 (总线母版保存到队列中的实际数目最多是驱动程序开发人员）。 这样，硬件准备就绪后执行总线 master 的硬件。 换而言之，驱动程序不应轮询和等待总线 master 完成。

当调用 DirectDraw *DxTransfer*函数，它会提供中的传输 ID **dwTransferID**的成员[ **DDTRANSFERININFO** ](https://msdn.microsoft.com/library/windows/hardware/ff550356)结构。 微型端口驱动程序然后可以使用此标识时*DxGetTransferStatus*调用函数。

总线 master 完成后，显示硬件必须生成一个 IRQ。 然后，微型端口驱动程序必须调用[ **IRQCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff568158)函数中指定[ *DxEnableIRQ*](https://msdn.microsoft.com/library/windows/hardware/ff557413)。 在此**IRQCallback**调用，微型端口驱动程序指定 DDIRQ\_总线主控标志。 然后调用 DirectDraw [ *DxGetTransferStatus* ](https://msdn.microsoft.com/library/windows/hardware/ff557438)函数来确定哪些总线 master 已完成。 微型端口驱动程序必须返回传输 ID (**dwTransferID**) 中早期传递给驱动程序的 DirectDraw *DxTransfer*调用。 这样一来，如果该驱动程序在队列中，有五个总线主机 DirectDraw 可以确定哪一个最近完成。

 

 





