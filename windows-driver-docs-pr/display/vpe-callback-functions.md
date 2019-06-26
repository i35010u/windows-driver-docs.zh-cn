---
title: VPE 回调函数
description: VPE 回调函数
ms.assetid: c36e99a5-0657-4945-b5e8-21d875e9d1ec
keywords:
- DirectX VPE 支持 WDK DirectDraw、 初始化
- 绘制 VPEs WDK DirectDraw 初始化
- DirectDraw VPEs WDK Windows 2000 显示初始化
- 视频端口扩展 WDK DirectDraw、 初始化
- VPEs WDK DirectDraw 初始化
- 初始化 DirectX VPE 功能
- 回调函数 WDK 的视频端口扩展
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 112d04c4bfd61d05bf704e063ab8aaf451d87ad3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376015"
---
# <a name="vpe-callback-functions"></a>VPE 回调函数


## <span id="ddk_vpe_callback_functions_gg"></span><span id="DDK_VPE_CALLBACK_FUNCTIONS_GG"></span>


下表列出了在显示器驱动程序中实现的视频端口扩展 (VPE) 回调函数。 支持 VPE 显示器驱动程序必须实现某些 VPE 回调函数;有些选项，取决于硬件功能。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">VPE 回调函数</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_vportcb_cancreatevideoport" data-raw-source="[&lt;em&gt;DdVideoPortCanCreate&lt;/em&gt;](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_vportcb_cancreatevideoport)"><em>DdVideoPortCanCreate</em></a></p></td>
<td align="left"><p>确定驱动程序是否可以支持指定的说明的 DirectDraw VPE 对象。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_vportcb_colorcontrol" data-raw-source="[&lt;em&gt;DdVideoPortColorControl&lt;/em&gt;](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_vportcb_colorcontrol)"><em>DdVideoPortColorControl</em></a></p></td>
<td align="left"><p>获取或设置颜色控件的 VPE 对象。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_vportcb_createvideoport" data-raw-source="[&lt;em&gt;DdVideoPortCreate&lt;/em&gt;](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_vportcb_createvideoport)"><em>DdVideoPortCreate</em></a></p></td>
<td align="left"><p>DirectDraw 创建 VPE 对象将通知驱动程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_vportcb_destroyvport" data-raw-source="[&lt;em&gt;DdVideoPortDestroy&lt;/em&gt;](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_vportcb_destroyvport)"><em>DdVideoPortDestroy</em></a></p></td>
<td align="left"><p>通知该驱动程序 DirectDraw 销毁指定的 VPE 对象。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_vportcb_flip" data-raw-source="[&lt;em&gt;DdVideoPortFlip&lt;/em&gt;](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_vportcb_flip)"><em>DdVideoPortFlip</em></a></p></td>
<td align="left"><p>执行物理翻转，从而导致 VPE 对象以开始向新的图面中写入数据。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_vportcb_getbandwidth" data-raw-source="[&lt;em&gt;DdVideoPortGetBandwidth&lt;/em&gt;](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_vportcb_getbandwidth)"><em>DdVideoPortGetBandwidth</em></a></p></td>
<td align="left"><p>报告指定 VPE 对象输出格式的设备的帧缓冲区内存的带宽限制。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_vportcb_getvportconnect" data-raw-source="[&lt;em&gt;DdVideoPortGetConnectInfo&lt;/em&gt;](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_vportcb_getvportconnect)"><em>DdVideoPortGetConnectInfo</em></a></p></td>
<td align="left"><p>返回由指定的 VPE 对象支持的连接。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_vportcb_getfield" data-raw-source="[&lt;em&gt;DdVideoPortGetField&lt;/em&gt;](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_vportcb_getfield)"><em>DdVideoPortGetField</em></a></p></td>
<td align="left"><p>确定当前交错信号的字段是否为偶数还是奇数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_vportcb_getflipstatus" data-raw-source="[&lt;em&gt;DdVideoPortGetFlipStatus&lt;/em&gt;](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_vportcb_getflipstatus)"><em>DdVideoPortGetFlipStatus</em></a></p></td>
<td align="left"><p>确定是否在最近请求翻转发生图面。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_vportcb_getinputformats" data-raw-source="[&lt;em&gt;DdVideoPortGetInputFormats&lt;/em&gt;](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_vportcb_getinputformats)"><em>DdVideoPortGetInputFormats</em></a></p></td>
<td align="left"><p>确定 DirectDraw VPE 对象可接受的输入的格式。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_vportcb_getline" data-raw-source="[&lt;em&gt;DdVideoPortGetLine&lt;/em&gt;](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_vportcb_getline)"><em>DdVideoPortGetLine</em></a></p></td>
<td align="left"><p>返回当前行号的硬件的视频端口。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_vportcb_getoutputformats" data-raw-source="[&lt;em&gt;DdVideoPortGetOutputFormats&lt;/em&gt;](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_vportcb_getoutputformats)"><em>DdVideoPortGetOutputFormats</em></a></p></td>
<td align="left"><p>确定 VPE 对象支持的输出格式。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_vportcb_getsignalstatus" data-raw-source="[&lt;em&gt;DdVideoPortGetSignalStatus&lt;/em&gt;](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_vportcb_getsignalstatus)"><em>DdVideoPortGetSignalStatus</em></a></p></td>
<td align="left"><p>检索当前提供给硬件视频端口的视频信号的状态。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_vportcb_update" data-raw-source="[&lt;em&gt;DdVideoPortUpdate&lt;/em&gt;](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_vportcb_update)"><em>DdVideoPortUpdate</em></a></p></td>
<td align="left"><p>启动和停止 VPE 对象并修改 VPE 对象数据流。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_vportcb_waitforsync" data-raw-source="[&lt;em&gt;DdVideoPortWaitForSync&lt;/em&gt;](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_vportcb_waitforsync)"><em>DdVideoPortWaitForSync</em></a></p></td>
<td align="left"><p>等待，直到下一步的垂直同步发生。</p></td>
</tr>
</tbody>
</table>

 

 

 





