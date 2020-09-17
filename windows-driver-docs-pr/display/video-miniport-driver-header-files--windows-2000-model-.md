---
title: 视频微型端口驱动程序标头文件（Windows 2000 模型）
description: 视频微型端口驱动程序标头文件（Windows 2000 模型）
ms.assetid: 7ce0df41-ce1e-4d76-b7e8-6d0a3576a58d
keywords:
- 视频微型端口驱动程序 WDK Windows 2000，头文件
- 标头文件 WDK 视频微型端口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8e241b5de931f07ffc1747663e721e447d169394
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90717328"
---
# <a name="video-miniport-driver-header-files-windows-2000-model"></a>视频微型端口驱动程序标头文件（Windows 2000 模型）


## <span id="ddk_video_miniport_driver_header_files_windows_2000_model__gg"></span><span id="DDK_VIDEO_MINIPORT_DRIVER_HEADER_FILES_WINDOWS_2000_MODEL__GG"></span>


Windows 2000 显示器驱动程序模型中的视频微型端口驱动程序包括以下头文件：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">文件名</th>
<th align="left">目录</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><em>dderror</em></p></td>
<td align="left"><p>包含微型端口驱动程序返回到视频端口驱动程序的 Win32 状态常量，该驱动程序也返回到微型端口驱动程序的对应内核模式显示驱动程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>devioctl</em></p></td>
<td align="left"><p>包含用于定义 i/o 控制代码的宏和常量。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>小型端口。h</em></p></td>
<td align="left"><p>包含用于视频 (和 SCSI) 微型端口驱动程序的基本类型、常量和结构。</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>ntddvdeo</em></p></td>
<td align="left"><p>包含系统定义的 i/o 控制代码 (IOCTLs) 和 (<a href="/windows-hardware/drivers/#wdkgloss-video-request-packet--vrp-" data-raw-source="&lt;em&gt;VRPs&lt;/em&gt;"><em>VRPs</em></a>) 视频微型端口驱动程序的视频请求数据包中发送的相应结构。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>tvout</em></p></td>
<td align="left"><p>包含用于实现电视连接器和副本保护支持以及此结构中使用的常量的 <a href="/windows/win32/api/tvout/ns-tvout-_videoparameters" data-raw-source="[&lt;strong&gt;VIDEOPARAMETERS&lt;/strong&gt;](/windows/win32/api/tvout/ns-tvout-_videoparameters)"><strong>VIDEOPARAMETERS</strong></a> 结构。</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>视频。h</em></p></td>
<td align="left"><p>包含 <strong>VideoPort</strong><em>Xxx</em> 和 <em>SvgaHwIoPortXxx</em> 视频端口函数声明、特定于视频的结构，如 <a href="/windows-hardware/drivers/ddi/video/ns-video-_video_request_packet" data-raw-source="[&lt;strong&gt;VIDEO_REQUEST_PACKET&lt;/strong&gt;](/windows-hardware/drivers/ddi/video/ns-video-_video_request_packet)"><strong>VIDEO_REQUEST_PACKET</strong></a>和 <em>HwVidXxx</em> 视频微型端口函数原型。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>videoagp</em></p></td>
<td align="left"><p>包含 AGP 特定的结构、 <em>AgpXxx</em> 微型端口驱动程序函数原型，以及在视频微型端口驱动程序中实现 AGP 支持所需的 <strong>VideoPort</strong><em>Xxx</em> 函数声明。</p></td>
</tr>
</tbody>
</table>

 

这些标头附带了 Windows 驱动程序工具包 (WDK) 。 有关这些标头文件中的函数、结构、系统定义的 i/o 控制代码和常量的详细信息，请参阅 [GDI 函数](/windows-hardware/drivers/ddi/index)。

