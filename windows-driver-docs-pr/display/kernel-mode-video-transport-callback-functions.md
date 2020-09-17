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
ms.openlocfilehash: a10fd42b3453521dc8b25e2eca273a6533534e73
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90716450"
---
# <a name="kernel-mode-video-transport-callback-functions"></a>内核模式视频传输回调函数


## <span id="ddk_kernel_mode_video_transport_callback_functions_gg"></span><span id="DDK_KERNEL_MODE_VIDEO_TRANSPORT_CALLBACK_FUNCTIONS_GG"></span>


下表列出了在视频微型端口驱动程序中实现的内核模式视频传输回调函数。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">DxApi 回调函数</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="/windows/win32/api/dxmini/nc-dxmini-pdx_bobnextfield" data-raw-source="[&lt;em&gt;DxBobNextField&lt;/em&gt;](/windows/win32/api/dxmini/nc-dxmini-pdx_bobnextfield)"><em>DxBobNextField</em></a></p></td>
<td align="left"><p>Bobs-sfpreviewcluster 交错数据的下一个字段。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/win32/api/dxmini/nc-dxmini-pdx_enableirq" data-raw-source="[&lt;em&gt;DxEnableIRQ&lt;/em&gt;](/windows/win32/api/dxmini/nc-dxmini-pdx_enableirq)"><em>DxEnableIRQ</em></a></p></td>
<td align="left"><p>向微型端口驱动程序指示应启用或禁用哪些 Irq。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/win32/api/dxmini/nc-dxmini-pdx_flipoverlay" data-raw-source="[&lt;em&gt;DxFlipOverlay&lt;/em&gt;](/windows/win32/api/dxmini/nc-dxmini-pdx_flipoverlay)"><em>DxFlipOverlay</em></a></p></td>
<td align="left"><p>翻转覆盖区。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/win32/api/dxmini/nc-dxmini-pdx_flipvideoport" data-raw-source="[&lt;em&gt;DxFlipVideoPort&lt;/em&gt;](/windows/win32/api/dxmini/nc-dxmini-pdx_flipvideoport)"><em>DxFlipVideoPort</em></a></p></td>
<td align="left"><p> (VPE) 对象翻转视频端口扩展。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/win32/api/dxmini/nc-dxmini-pdx_getcurrentautoflip" data-raw-source="[&lt;em&gt;DxGetCurrentAutoflip&lt;/em&gt;](/windows/win32/api/dxmini/nc-dxmini-pdx_getcurrentautoflip)"><em>DxGetCurrentAutoflip</em></a></p></td>
<td align="left"><p>确定接收视频数据当前字段以供捕获的图面。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/win32/api/dxmini/nc-dxmini-pdx_getirqinfo" data-raw-source="[&lt;em&gt;DxGetIRQInfo&lt;/em&gt;](/windows/win32/api/dxmini/nc-dxmini-pdx_getirqinfo)"><em>DxGetIRQInfo</em></a></p></td>
<td align="left"><p>指示驱动程序管理中断请求。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/win32/api/dxmini/nc-dxmini-pdx_getpolarity" data-raw-source="[&lt;em&gt;DxGetPolarity&lt;/em&gt;](/windows/win32/api/dxmini/nc-dxmini-pdx_getpolarity)"><em>DxGetPolarity</em></a></p></td>
<td align="left"><p>返回由 VPE 对象写入的当前字段的极性 (或奇数) 。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/win32/api/dxmini/nc-dxmini-pdx_getpreviousautoflip" data-raw-source="[&lt;em&gt;DxGetPreviousAutoflip&lt;/em&gt;](/windows/win32/api/dxmini/nc-dxmini-pdx_getpreviousautoflip)"><em>DxGetPreviousAutoflip</em></a></p></td>
<td align="left"><p>确定接收的视频数据的上一个字段以供捕获的图面。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/win32/api/dxmini/nc-dxmini-pdx_gettransferstatus" data-raw-source="[&lt;em&gt;DxGetTransferStatus&lt;/em&gt;](/windows/win32/api/dxmini/nc-dxmini-pdx_gettransferstatus)"><em>DxGetTransferStatus</em></a></p></td>
<td align="left"><p>确定完成的硬件总线主节点。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/win32/api/dxmini/nc-dxmini-pdx_lock" data-raw-source="[&lt;em&gt;DxLock&lt;/em&gt;](/windows/win32/api/dxmini/nc-dxmini-pdx_lock)"><em>DxLock</em></a></p></td>
<td align="left"><p>锁定帧缓冲区以便可以对其进行访问。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/win32/api/dxmini/nc-dxmini-pdx_setstate" data-raw-source="[&lt;em&gt;DxSetState&lt;/em&gt;](/windows/win32/api/dxmini/nc-dxmini-pdx_setstate)"><em>DxSetState</em></a></p></td>
<td align="left"><p>从 bob 模式切换到编织模式，反之亦然。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/win32/api/dxmini/nc-dxmini-pdx_skipnextfield" data-raw-source="[&lt;em&gt;DxSkipNextField&lt;/em&gt;](/windows/win32/api/dxmini/nc-dxmini-pdx_skipnextfield)"><em>DxSkipNextField</em></a></p></td>
<td align="left"><p>跳过或会下一个字段。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/win32/api/dxmini/nc-dxmini-pdx_transfer" data-raw-source="[&lt;em&gt;DxTransfer&lt;/em&gt;](/windows/win32/api/dxmini/nc-dxmini-pdx_transfer)"><em>DxTransfer</em></a></p></td>
<td align="left"><p>从图面到内存描述符列表中指定的缓冲区的总线主控数据 (MDL) 。</p></td>
</tr>
</tbody>
</table>

 

