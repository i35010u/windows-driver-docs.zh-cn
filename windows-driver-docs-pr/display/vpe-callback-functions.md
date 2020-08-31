---
title: VPE 回调函数
description: VPE 回调函数
ms.assetid: c36e99a5-0657-4945-b5e8-21d875e9d1ec
keywords:
- DirectX VPE 支持 WDK DirectDraw，初始化
- 绘制 VPEs WDK DirectDraw，初始化
- DirectDraw VPEs WDK Windows 2000 显示，初始化
- 视频端口扩展 WDK DirectDraw，初始化
- VPEs WDK DirectDraw，初始化
- 正在初始化 DirectX VPE 功能
- 回调函数 WDK 视频端口扩展
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b9728d91436a8ab1fd9002b4c298926dc74d68b5
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89063706"
---
# <a name="vpe-callback-functions"></a>VPE 回调函数


## <span id="ddk_vpe_callback_functions_gg"></span><span id="DDK_VPE_CALLBACK_FUNCTIONS_GG"></span>


下表列出了在显示驱动程序中实现的 (VPE) 回调函数的视频端口扩展。 支持 VPE 的显示驱动程序必须实现某些 VPE 回调函数;某些选项是可选的，具体取决于硬件功能。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">VPE 回调函数</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_vportcb_cancreatevideoport" data-raw-source="[&lt;em&gt;DdVideoPortCanCreate&lt;/em&gt;](/windows/desktop/api/ddrawint/nc-ddrawint-pdd_vportcb_cancreatevideoport)"><em>DdVideoPortCanCreate</em></a></p></td>
<td align="left"><p>确定驱动程序是否可以支持指定说明的 DirectDraw VPE 对象。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_vportcb_colorcontrol" data-raw-source="[&lt;em&gt;DdVideoPortColorControl&lt;/em&gt;](/windows/desktop/api/ddrawint/nc-ddrawint-pdd_vportcb_colorcontrol)"><em>DdVideoPortColorControl</em></a></p></td>
<td align="left"><p>获取或设置 VPE 对象的颜色控件。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_vportcb_createvideoport" data-raw-source="[&lt;em&gt;DdVideoPortCreate&lt;/em&gt;](/windows/desktop/api/ddrawint/nc-ddrawint-pdd_vportcb_createvideoport)"><em>DdVideoPortCreate</em></a></p></td>
<td align="left"><p>通知驱动程序 DirectDraw 创建了 VPE 对象。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_vportcb_destroyvport" data-raw-source="[&lt;em&gt;DdVideoPortDestroy&lt;/em&gt;](/windows/desktop/api/ddrawint/nc-ddrawint-pdd_vportcb_destroyvport)"><em>DdVideoPortDestroy</em></a></p></td>
<td align="left"><p>通知驱动程序 DirectDraw 销毁了指定的 VPE 对象。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_vportcb_flip" data-raw-source="[&lt;em&gt;DdVideoPortFlip&lt;/em&gt;](/windows/desktop/api/ddrawint/nc-ddrawint-pdd_vportcb_flip)"><em>DdVideoPortFlip</em></a></p></td>
<td align="left"><p>执行物理翻转，导致 VPE 对象开始向新表面写入数据。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_vportcb_getbandwidth" data-raw-source="[&lt;em&gt;DdVideoPortGetBandwidth&lt;/em&gt;](/windows/desktop/api/ddrawint/nc-ddrawint-pdd_vportcb_getbandwidth)"><em>DdVideoPortGetBandwidth</em></a></p></td>
<td align="left"><p>基于指定的 VPE 对象输出格式报告设备帧缓冲内存的带宽限制。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_vportcb_getvportconnect" data-raw-source="[&lt;em&gt;DdVideoPortGetConnectInfo&lt;/em&gt;](/windows/desktop/api/ddrawint/nc-ddrawint-pdd_vportcb_getvportconnect)"><em>DdVideoPortGetConnectInfo</em></a></p></td>
<td align="left"><p>返回由指定的 VPE 对象支持的连接。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_vportcb_getfield" data-raw-source="[&lt;em&gt;DdVideoPortGetField&lt;/em&gt;](/windows/desktop/api/ddrawint/nc-ddrawint-pdd_vportcb_getfield)"><em>DdVideoPortGetField</em></a></p></td>
<td align="left"><p>确定交错信号的当前字段是否为偶数或奇数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_vportcb_getflipstatus" data-raw-source="[&lt;em&gt;DdVideoPortGetFlipStatus&lt;/em&gt;](/windows/desktop/api/ddrawint/nc-ddrawint-pdd_vportcb_getflipstatus)"><em>DdVideoPortGetFlipStatus</em></a></p></td>
<td align="left"><p>确定是否已在表面上出现最近请求的翻转。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_vportcb_getinputformats" data-raw-source="[&lt;em&gt;DdVideoPortGetInputFormats&lt;/em&gt;](/windows/desktop/api/ddrawint/nc-ddrawint-pdd_vportcb_getinputformats)"><em>DdVideoPortGetInputFormats</em></a></p></td>
<td align="left"><p>确定 DirectDraw VPE 对象可以接受的输入格式。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_vportcb_getline" data-raw-source="[&lt;em&gt;DdVideoPortGetLine&lt;/em&gt;](/windows/desktop/api/ddrawint/nc-ddrawint-pdd_vportcb_getline)"><em>DdVideoPortGetLine</em></a></p></td>
<td align="left"><p>返回硬件视频端口的当前行号。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_vportcb_getoutputformats" data-raw-source="[&lt;em&gt;DdVideoPortGetOutputFormats&lt;/em&gt;](/windows/desktop/api/ddrawint/nc-ddrawint-pdd_vportcb_getoutputformats)"><em>DdVideoPortGetOutputFormats</em></a></p></td>
<td align="left"><p>确定 VPE 对象支持的输出格式。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_vportcb_getsignalstatus" data-raw-source="[&lt;em&gt;DdVideoPortGetSignalStatus&lt;/em&gt;](/windows/desktop/api/ddrawint/nc-ddrawint-pdd_vportcb_getsignalstatus)"><em>DdVideoPortGetSignalStatus</em></a></p></td>
<td align="left"><p>检索当前显示到硬件视频端口的视频信号的状态。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_vportcb_update" data-raw-source="[&lt;em&gt;DdVideoPortUpdate&lt;/em&gt;](/windows/desktop/api/ddrawint/nc-ddrawint-pdd_vportcb_update)"><em>DdVideoPortUpdate</em></a></p></td>
<td align="left"><p>启动和停止 VPE 对象并修改 VPE 对象数据流。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_vportcb_waitforsync" data-raw-source="[&lt;em&gt;DdVideoPortWaitForSync&lt;/em&gt;](/windows/desktop/api/ddrawint/nc-ddrawint-pdd_vportcb_waitforsync)"><em>DdVideoPortWaitForSync</em></a></p></td>
<td align="left"><p>等待，直到下一次垂直同步发生。</p></td>
</tr>
</tbody>
</table>

 

 

