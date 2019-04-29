---
title: 视频微型端口驱动程序标头文件（Windows 2000 模型）
description: 视频微型端口驱动程序标头文件（Windows 2000 模型）
ms.assetid: 7ce0df41-ce1e-4d76-b7e8-6d0a3576a58d
keywords:
- 微型端口驱动程序 WDK Windows 2000 中，标头文件
- 标头文件 WDK 微型端口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 67c8035c69d2cd8b42e5332b68ec7ab783685c81
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63389685"
---
# <a name="video-miniport-driver-header-files-windows-2000-model"></a>视频微型端口驱动程序标头文件（Windows 2000 模型）


## <span id="ddk_video_miniport_driver_header_files_windows_2000_model__gg"></span><span id="DDK_VIDEO_MINIPORT_DRIVER_HEADER_FILES_WINDOWS_2000_MODEL__GG"></span>


在 Windows 2000 显示器驱动程序模型中的微型端口驱动程序包括以下标头文件：

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
<td align="left"><p><em>dderror.h</em></p></td>
<td align="left"><p>包含微型端口驱动程序返回到的视频端口驱动程序，它也会返回到微型端口驱动程序的相应内核模式显示驱动程序的 Win32 状态常量。</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>devioctl.h</em></p></td>
<td align="left"><p>包含的宏和常量用于定义 I/O 控制代码。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>miniport.h</em></p></td>
<td align="left"><p>包含基本类型、 常量和结构的视频 （和 SCSI） 微型端口驱动程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>ntddvdeo.h</em></p></td>
<td align="left"><p>包含的系统定义的 I/O 控制代码 (Ioctl) 和在进行视频请求数据包中发送的相应结构 (<a href="https://msdn.microsoft.com/library/windows/hardware/ff556344#wdkgloss-video-request-packet--vrp-" data-raw-source="&lt;em&gt;VRPs&lt;/em&gt;"><em>VRPs</em></a>) 微型端口驱动程序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>tvout.h</em></p></td>
<td align="left"><p>包含<a href="https://msdn.microsoft.com/library/windows/hardware/ff570173" data-raw-source="[&lt;strong&gt;VIDEOPARAMETERS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff570173)"> <strong>VIDEOPARAMETERS</strong> </a>结构用于实现电视连接器和复制保护支持和使用此结构中的常量。</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>video.h</em></p></td>
<td align="left"><p>包含<strong>视频端口</strong><em>Xxx</em>并<em>SvgaHwIoPortXxx</em>视频端口函数声明，特定于视频的结构，如<a href="https://msdn.microsoft.com/library/windows/hardware/ff570547" data-raw-source="[&lt;strong&gt;VIDEO_REQUEST_PACKET&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff570547)"> <strong>VIDEO_REQUEST_PACKET</strong></a>，并<em>HwVidXxx</em>微型端口函数原型。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>videoagp.h</em></p></td>
<td align="left"><p>包含特定于 AGP 的结构<em>AgpXxx</em>微型端口驱动程序函数原型，并<strong>视频端口</strong><em>Xxx</em>函数实现 AGP 支持所需的声明在视频的微型端口驱动程序。</p></td>
</tr>
</tbody>
</table>

 

这些标头被提供与 Windows Driver Kit (WDK)。 有关详细信息函数、 结构、 系统定义的 I/O 控制代码，以及这些标头文件中的常量，请参阅[GDI 函数](https://msdn.microsoft.com/library/windows/hardware/ff566543)。

 

 





