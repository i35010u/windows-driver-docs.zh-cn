---
title: 内核模式视频传输回调函数
description: 内核模式视频传输回调函数
ms.assetid: 1edd5b68-91da-4846-87bd-6fcabb9e5abf
keywords:
- DxApi 微型端口驱动程序 WDK DirectDraw，内核模式视频传输回调函数
- 内核模式视频传输 WDK DirectDraw，回调函数
- 回调函数 WDK 内核模式视频传输
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e654c2248c786d03963de02111ce2635cd726175
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372899"
---
# <a name="kernel-mode-video-transport-callback-functions"></a>内核模式视频传输回调函数


## <span id="ddk_kernel_mode_video_transport_callback_functions_gg"></span><span id="DDK_KERNEL_MODE_VIDEO_TRANSPORT_CALLBACK_FUNCTIONS_GG"></span>


下表列出了内核模式视频传输回叫函数，在视频的微型端口驱动程序中实现。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">DxApi 回调函数</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/dxmini/nc-dxmini-pdx_bobnextfield" data-raw-source="[&lt;em&gt;DxBobNextField&lt;/em&gt;](https://docs.microsoft.com/windows/desktop/api/dxmini/nc-dxmini-pdx_bobnextfield)"><em>DxBobNextField</em></a></p></td>
<td align="left"><p>Bobs 交错数据的下一个字段。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/dxmini/nc-dxmini-pdx_enableirq" data-raw-source="[&lt;em&gt;DxEnableIRQ&lt;/em&gt;](https://docs.microsoft.com/windows/desktop/api/dxmini/nc-dxmini-pdx_enableirq)"><em>DxEnableIRQ</em></a></p></td>
<td align="left"><p>指示应启用或禁用的 Irq 的微型端口驱动程序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/dxmini/nc-dxmini-pdx_flipoverlay" data-raw-source="[&lt;em&gt;DxFlipOverlay&lt;/em&gt;](https://docs.microsoft.com/windows/desktop/api/dxmini/nc-dxmini-pdx_flipoverlay)"><em>DxFlipOverlay</em></a></p></td>
<td align="left"><p>翻转在覆盖区。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/dxmini/nc-dxmini-pdx_flipvideoport" data-raw-source="[&lt;em&gt;DxFlipVideoPort&lt;/em&gt;](https://docs.microsoft.com/windows/desktop/api/dxmini/nc-dxmini-pdx_flipvideoport)"><em>DxFlipVideoPort</em></a></p></td>
<td align="left"><p>翻转的视频端口扩展 (VPE) 对象。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/dxmini/nc-dxmini-pdx_getcurrentautoflip" data-raw-source="[&lt;em&gt;DxGetCurrentAutoflip&lt;/em&gt;](https://docs.microsoft.com/windows/desktop/api/dxmini/nc-dxmini-pdx_getcurrentautoflip)"><em>DxGetCurrentAutoflip</em></a></p></td>
<td align="left"><p>确定哪些面正在接收的视频数据，以便进行捕获当前字段。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/dxmini/nc-dxmini-pdx_getirqinfo" data-raw-source="[&lt;em&gt;DxGetIRQInfo&lt;/em&gt;](https://docs.microsoft.com/windows/desktop/api/dxmini/nc-dxmini-pdx_getirqinfo)"><em>DxGetIRQInfo</em></a></p></td>
<td align="left"><p>指示该驱动程序管理中断请求。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/dxmini/nc-dxmini-pdx_getpolarity" data-raw-source="[&lt;em&gt;DxGetPolarity&lt;/em&gt;](https://docs.microsoft.com/windows/desktop/api/dxmini/nc-dxmini-pdx_getpolarity)"><em>DxGetPolarity</em></a></p></td>
<td align="left"><p>返回当前由 vpe 数据对象写入的字段的极性 （偶数还是奇数）。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/dxmini/nc-dxmini-pdx_getpreviousautoflip" data-raw-source="[&lt;em&gt;DxGetPreviousAutoflip&lt;/em&gt;](https://docs.microsoft.com/windows/desktop/api/dxmini/nc-dxmini-pdx_getpreviousautoflip)"><em>DxGetPreviousAutoflip</em></a></p></td>
<td align="left"><p>确定在哪一个表面收到上一个视频数据，以便进行捕获的字段。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/dxmini/nc-dxmini-pdx_gettransferstatus" data-raw-source="[&lt;em&gt;DxGetTransferStatus&lt;/em&gt;](https://docs.microsoft.com/windows/desktop/api/dxmini/nc-dxmini-pdx_gettransferstatus)"><em>DxGetTransferStatus</em></a></p></td>
<td align="left"><p>确定哪些硬件总线 master 已完成。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/dxmini/nc-dxmini-pdx_lock" data-raw-source="[&lt;em&gt;DxLock&lt;/em&gt;](https://docs.microsoft.com/windows/desktop/api/dxmini/nc-dxmini-pdx_lock)"><em>DxLock</em></a></p></td>
<td align="left"><p>锁定帧缓冲区，以便对其进行访问。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/dxmini/nc-dxmini-pdx_setstate" data-raw-source="[&lt;em&gt;DxSetState&lt;/em&gt;](https://docs.microsoft.com/windows/desktop/api/dxmini/nc-dxmini-pdx_setstate)"><em>DxSetState</em></a></p></td>
<td align="left"><p>从 bob 模式将模式中，切换，反之亦然。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/dxmini/nc-dxmini-pdx_skipnextfield" data-raw-source="[&lt;em&gt;DxSkipNextField&lt;/em&gt;](https://docs.microsoft.com/windows/desktop/api/dxmini/nc-dxmini-pdx_skipnextfield)"><em>DxSkipNextField</em></a></p></td>
<td align="left"><p>将跳过或重新启用下一个字段。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/dxmini/nc-dxmini-pdx_transfer" data-raw-source="[&lt;em&gt;DxTransfer&lt;/em&gt;](https://docs.microsoft.com/windows/desktop/api/dxmini/nc-dxmini-pdx_transfer)"><em>DxTransfer</em></a></p></td>
<td align="left"><p>总线母版将数据从一个面到内存描述符列表 (MDL) 中指定的缓冲区。</p></td>
</tr>
</tbody>
</table>

 

 

 





