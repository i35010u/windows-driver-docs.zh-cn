---
title: UVC 1.0 与 UVC 1.1 之间的差异
description: UVC 1.0 与 UVC 1.1 之间的差异
keywords:
- USB 视频类驱动程序 WDK AVStream，版本差异
- USB 视频类驱动程序 WDK AVStream，UVC 1.0 和 UVC 1.1 之间的差异
- 视频类驱动程序 WDK USB，UVC 1.0 和 UVC 1.1 之间的差异
- UVC 驱动程序 WDK AVStream，UVC 1.0 与 UVC 1.1 之间的差异
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c27d5dfb799ef95604079d0f1868eecd1c729c1a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96830871"
---
# <a name="differences-between-uvc-10-and-uvc-11"></a>UVC 1.0 与 UVC 1.1 之间的差异


当你设计 UVC 兼容硬件以使用 Windows 7 或更早版本的 Windows 时，必须在支持 UVC 1.0 与1.1 之间进行决定。

与 UVC 1.1 兼容的设备应将 Class-Specific VC 接口中的 **bcdUVC** 标志设置为0x110。 此外，如果存在可选的处理单元描述符，则与1.1 兼容的设备应执行以下操作：

1.  向处理单元描述符添加一个 **bmVideoStandards** 字段。

2.  更新处理单元中的 **bLength** 字段。

3.  更新 **wTotalLength** ，以反映处理单元的更大 PU 大小。

下表总结了 UVC 1.0 与1.1 之间的差异。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>状态</th>
<th>描述符/请求/控制</th>
<th>字段</th>
<th>备注</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>更改</p></td>
<td><p>Class-Specific VC 接口</p></td>
<td><p><strong>bcdUVC</strong></p></td>
<td><p>0x110 for 1.1，0x100 1。0</p></td>
</tr>
<tr class="even">
<td><p>已过时</p></td>
<td><p>Class-Specific VC 接口</p></td>
<td><p><strong>dwClockFrequency</strong></p></td>
<td><p>未使用1。1</p></td>
</tr>
<tr class="odd">
<td><p>更改</p></td>
<td><p>处理单元</p></td>
<td><p><strong>bLength</strong></p></td>
<td><p>10 + n 表示1.1，9 + n 表示1。0</p></td>
</tr>
<tr class="even">
<td><p>new</p></td>
<td><p>处理单元</p></td>
<td><p><strong>bmVideoStandards</strong></p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>更改</p></td>
<td><p>Class-Specific VS 接口输入标头</p></td>
<td><p><strong>bmaControls (n) </strong></p></td>
<td><p>1.1 在 "探测和提交" 中采用不同的方式</p></td>
</tr>
<tr class="even">
<td><p>更改</p></td>
<td><p>Class-Specific VS Interface Output 标头</p></td>
<td><p><strong>bLength</strong></p></td>
<td><p>9 + (p * n) 用于1.1，8表示1。0</p></td>
</tr>
<tr class="odd">
<td><p>new</p></td>
<td><p>Class-Specific VS Interface Output 标头</p></td>
<td><p><strong>bControlSize</strong></p></td>
<td></td>
</tr>
<tr class="even">
<td><p>new</p></td>
<td><p>Class-Specific VS Interface Output 标头</p></td>
<td><p><strong>bmaControls (n) </strong></p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>已过时</p></td>
<td><p>接口控件</p></td>
<td><p><strong>VC_REQUEST_INDICATE_HOST_CLOCK_CONTROL</strong></p></td>
<td><p>对于支持主机到使用 SCR/PT 的设备负载的1.0 设备是必需的</p></td>
</tr>
<tr class="even">
<td><p>new</p></td>
<td><p>接口控件</p></td>
<td><p><strong>GET_INFO</strong></p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>new</p></td>
<td><p>处理单元</p></td>
<td><p><strong>PU_DIGITAL_MULTIPLIER_CONTROL</strong></p></td>
<td></td>
</tr>
<tr class="even">
<td><p>new</p></td>
<td><p>处理单元</p></td>
<td><p><strong>PU_ANALOG_VIDEO_STANDARD_CONTROL</strong></p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>new</p></td>
<td><p>处理单元</p></td>
<td><p><strong>PU_ANALOG_LOCK_STATUS_CONTROL</strong></p></td>
<td></td>
</tr>
<tr class="even">
<td><p>更改</p></td>
<td><p>视频探测和提交控制</p></td>
<td><p><strong>wLength</strong></p></td>
<td><p>34表示1.1，26表示1。0</p></td>
</tr>
<tr class="odd">
<td><p>new</p></td>
<td><p>视频探测和提交控制</p></td>
<td><p><strong>dwClockFrequency</strong></p></td>
<td></td>
</tr>
<tr class="even">
<td><p>new</p></td>
<td><p>视频探测和提交控制</p></td>
<td><p><strong>bmFramingInfo</strong></p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>new</p></td>
<td><p>视频探测和提交控制</p></td>
<td><p><strong>bPreferredVersion</strong></p></td>
<td></td>
</tr>
<tr class="even">
<td><p>new</p></td>
<td><p>视频探测和提交控制</p></td>
<td><p><strong>bMinVersion</strong></p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>new</p></td>
<td><p>视频探测和提交控制</p></td>
<td><p><strong>bMaxVersion</strong></p></td>
<td></td>
</tr>
<tr class="even">
<td><p>new</p></td>
<td><p>视频探测和提交控制</p></td>
<td><p>VS_PROBE_CONTROL 的<strong>GET_INFO</strong></p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>new</p></td>
<td><p>视频探测和提交控制</p></td>
<td><p>VS_COMMIT_CONTROL 的<strong>GET_INFO</strong></p></td>
<td></td>
</tr>
<tr class="even">
<td><p>已过时</p></td>
<td><p>Class-Specific VS 接口</p></td>
<td><p><strong>VS_FORMAT_MPEG1</strong></p></td>
<td><p>不受任何 Windows 操作系统的支持</p></td>
</tr>
<tr class="odd">
<td><p>已过时</p></td>
<td><p>Class-Specific VS 接口</p></td>
<td><p><strong>VS_FORMAT_MPEG2PS</strong></p></td>
<td><p>不受任何 Windows 操作系统的支持</p></td>
</tr>
<tr class="even">
<td><p>已过时</p></td>
<td><p>Class-Specific VS 接口</p></td>
<td><p><strong>VS_FORMAT_MPEG4SL</strong></p></td>
<td><p>不受任何 Windows 操作系统的支持</p></td>
</tr>
<tr class="odd">
<td><p>已过时</p></td>
<td><p>Class-Specific VS 接口</p></td>
<td><p><strong>VS_FORMAT_VENDOR</strong></p></td>
<td><p>不受任何 Windows 操作系统的支持</p></td>
</tr>
<tr class="even">
<td><p>已过时</p></td>
<td><p>Class-Specific VS 接口</p></td>
<td><p><strong>VS_FRAME_VENDOR</strong></p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>new</p></td>
<td><p>Class-Specific VS 接口</p></td>
<td><p><strong>VS_FORMAT_FRAME_BASED</strong></p></td>
<td></td>
</tr>
<tr class="even">
<td><p>new</p></td>
<td><p>Class-Specific VS 接口</p></td>
<td><p><strong>VS_FRAME_FRAME_BASED</strong></p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>new</p></td>
<td><p>Class-Specific VS 接口</p></td>
<td><p><strong>VS_FORMAT_STREAM_BASED</strong></p></td>
<td></td>
</tr>
</tbody>
</table>

 

对于 UVC 1.0 设备，MPEG2TS 格式描述符的长度为7。 由于 UVC 1.1 包含一个新的16字节 GUID 字段，MPEG2TS 格式描述符的长度是23。

相应地，如果将 MPEG2TS 描述符更新为23个字节，则还必须将 Class-Specific VC 接口中的 **bcdUVC** 标志设置为0x110。

 

 




