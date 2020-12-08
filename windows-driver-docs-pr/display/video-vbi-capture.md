---
title: 视频 VBI 捕获
description: 视频 VBI 捕获
keywords:
- 视频 VBI 捕获 WDK DirectDraw
- 垂直消隐间隔 WDK DirectDraw
- VBI WDK DirectDraw
- DxTransfer
- DxApi 微型端口驱动程序 WDK DirectDraw，VBI 捕获
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ce5bad545452b12a94311570e09fce4dc001ffa0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96806351"
---
# <a name="video-vbi-capture"></a>视频 VBI 捕获


## <span id="ddk_video_vbi_capture_gg"></span><span id="DDK_VIDEO_VBI_CAPTURE_GG"></span>


DirectX 5.2 引入了两个 DirectDraw 驱动程序函数用于视频垂直消隐间隔 (VBI) 捕获。 这些函数是 [*DxTransfer*](/windows/win32/api/dxmini/nc-dxmini-pdx_transfer) 和 [*DxGetTransferStatus*](/windows/win32/api/dxmini/nc-dxmini-pdx_gettransferstatus)。

*DxTransfer* 函数便于视频和 VBI 捕获。 由于在 IRQ 时间调用此函数，因此它必须尽快返回。 如果在调用 *DxTransfer* 时，显示硬件未准备好执行总线主机，则视频微型端口驱动程序应保留多个总线主机的内部队列， (队列中保存的总线主机的实际数目取决于驱动程序开发人员) 。 这允许硬件在硬件就绪时执行总线主机。 换句话说，驱动程序不应轮询并等待总线主机完成。

当 DirectDraw 调用 *DxTransfer* 函数时，它将在 [**DDTRANSFERININFO**](/windows/win32/api/dxmini/ns-dxmini-ddtransferininfo)结构的 **dwTransferID** 成员中提供一个传输 ID。 然后，在调用 *DxGetTransferStatus* 函数时，视频微型端口驱动程序可以使用此标识。

总线主机完成后，显示硬件必须生成 IRQ。 然后，视频微型端口驱动程序必须调用 [*DxEnableIRQ*](/windows/win32/api/dxmini/nc-dxmini-pdx_enableirq)中指定的 [**IRQCallback**](/windows/win32/api/dxmini/nc-dxmini-pdx_irqcallback)函数。 在此 **IRQCallback** 调用中，视频微型端口驱动程序指定 DDIRQ \_ BUSMASTER 标志。 DirectDraw 随后将调用 [*DxGetTransferStatus*](/windows/win32/api/dxmini/nc-dxmini-pdx_gettransferstatus) 函数来确定已完成的总线主节点。 视频微型端口驱动程序必须返回 DirectDraw 传递到 *DxTransfer* 调用中的驱动程序的 (**dwTransferID**) 的传输 ID。 这样一来，如果驱动程序在队列中有五个总线主机，则 DirectDraw 可以确定最近完成了哪一个。

 

