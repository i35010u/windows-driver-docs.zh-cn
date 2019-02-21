---
title: UVC 1.0 和 1.1 UVC 之间的差异
description: UVC 1.0 和 1.1 UVC 之间的差异
ms.assetid: 5199fc4f-7bc2-4edb-bb52-cd2028756f64
keywords:
- USB 视频类驱动程序 WDK AVStream，版本差异
- USB 视频类驱动程序 WDK AVStream UVC 1.0 和 UVC 1.1 之间的差异
- 视频的类驱动程序 WDK USB UVC 1.0 和 UVC 1.1 之间的差异
- UVC 驱动程序 WDK AVStream UVC 1.0 和 UVC 1.1 之间的差异
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7c8113d17cc94d9464d63da905122cf10f0c03df
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56540970"
---
# <a name="differences-between-uvc-10-and-uvc-11"></a>UVC 1.0 和 1.1 UVC 之间的差异


在设计符合 UVC 的硬件，以使用 Windows 7 或更早版本的 Windows 时，您必须决定之间支持 UVC 1.0 和 1.1 版。

符合 UVC 1.1 的设备应设置**bcdUVC** 0x110 类特定于 VC 接口中的标志。 此外，如果存在可选的处理单元描述符，应执行以下 1.1 兼容的设备：

1.  添加**bmVideoStandards**处理部门描述符字段。

2.  更新**bLength**字段中处理单元。

3.  更新**wTotalLength**以反映处理单元的大小更大 PU。

下表总结了 UVC 1.0 与 1.1 之间的差异。

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
<td><p>change</p></td>
<td><p>特定于类的 VC 接口</p></td>
<td><p><strong>bcdUVC</strong></p></td>
<td><p>1.1，0x110 0x100 1.0</p></td>
</tr>
<tr class="even">
<td><p>已过时</p></td>
<td><p>特定于类的 VC 接口</p></td>
<td><p><strong>dwClockFrequency</strong></p></td>
<td><p>未使用 1.1</p></td>
</tr>
<tr class="odd">
<td><p>change</p></td>
<td><p>处理单元</p></td>
<td><p><strong>bLength</strong></p></td>
<td><p>10 + n 1.1，9 + 1.0 n</p></td>
</tr>
<tr class="even">
<td><p>新</p></td>
<td><p>处理单元</p></td>
<td><p><strong>bmVideoStandards</strong></p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>change</p></td>
<td><p>特定于类的 VS 接口输入标头</p></td>
<td><p><strong>bmaControls(n)</strong></p></td>
<td><p>1.1 将使用某些以不同的方式在这些位&quot;探测并提交&quot;</p></td>
</tr>
<tr class="even">
<td><p>change</p></td>
<td><p>特定于类的 VS 接口输出标头</p></td>
<td><p><strong>bLength</strong></p></td>
<td><p>1.1，9+(p*n) 1.0 8</p></td>
</tr>
<tr class="odd">
<td><p>新</p></td>
<td><p>特定于类的 VS 接口输出标头</p></td>
<td><p><strong>bControlSize</strong></p></td>
<td></td>
</tr>
<tr class="even">
<td><p>新</p></td>
<td><p>特定于类的 VS 接口输出标头</p></td>
<td><p><strong>bmaControls(n)</strong></p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>已过时</p></td>
<td><p>界面控件</p></td>
<td><p><strong>VC_REQUEST_INDICATE_HOST_CLOCK_CONTROL</strong></p></td>
<td><p>必须为 1.0 的设备支持承载使用 SCR/PTS 的设备负载</p></td>
</tr>
<tr class="even">
<td><p>新</p></td>
<td><p>界面控件</p></td>
<td><p><strong>GET_INFO</strong></p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>新</p></td>
<td><p>处理单元</p></td>
<td><p><strong>PU_DIGITAL_MULTIPLIER_CONTROL</strong></p></td>
<td></td>
</tr>
<tr class="even">
<td><p>新</p></td>
<td><p>处理单元</p></td>
<td><p><strong>PU_ANALOG_VIDEO_STANDARD_CONTROL</strong></p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>新</p></td>
<td><p>处理单元</p></td>
<td><p><strong>PU_ANALOG_LOCK_STATUS_CONTROL</strong></p></td>
<td></td>
</tr>
<tr class="even">
<td><p>change</p></td>
<td><p>视频探测和提交控制</p></td>
<td><p><strong>wLength</strong></p></td>
<td><p>1.1 34、 1.0 的 26</p></td>
</tr>
<tr class="odd">
<td><p>新</p></td>
<td><p>视频探测和提交控制</p></td>
<td><p><strong>dwClockFrequency</strong></p></td>
<td></td>
</tr>
<tr class="even">
<td><p>新</p></td>
<td><p>视频探测和提交控制</p></td>
<td><p><strong>bmFramingInfo</strong></p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>新</p></td>
<td><p>视频探测和提交控制</p></td>
<td><p><strong>bPreferredVersion</strong></p></td>
<td></td>
</tr>
<tr class="even">
<td><p>新</p></td>
<td><p>视频探测和提交控制</p></td>
<td><p><strong>bMinVersion</strong></p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>新</p></td>
<td><p>视频探测和提交控制</p></td>
<td><p><strong>bMaxVersion</strong></p></td>
<td></td>
</tr>
<tr class="even">
<td><p>新</p></td>
<td><p>视频探测和提交控制</p></td>
<td><p><strong>GET_INFO</strong>为 VS_PROBE_CONTROL</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>新</p></td>
<td><p>视频探测和提交控制</p></td>
<td><p><strong>GET_INFO</strong>为 VS_COMMIT_CONTROL</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>已过时</p></td>
<td><p>特定于类的 VS 接口</p></td>
<td><p><strong>VS_FORMAT_MPEG1</strong></p></td>
<td><p>不支持的任何 Windows 操作系统</p></td>
</tr>
<tr class="odd">
<td><p>已过时</p></td>
<td><p>特定于类的 VS 接口</p></td>
<td><p><strong>VS_FORMAT_MPEG2PS</strong></p></td>
<td><p>不支持的任何 Windows 操作系统</p></td>
</tr>
<tr class="even">
<td><p>已过时</p></td>
<td><p>特定于类的 VS 接口</p></td>
<td><p><strong>VS_FORMAT_MPEG4SL</strong></p></td>
<td><p>不支持的任何 Windows 操作系统</p></td>
</tr>
<tr class="odd">
<td><p>已过时</p></td>
<td><p>特定于类的 VS 接口</p></td>
<td><p><strong>VS_FORMAT_VENDOR</strong></p></td>
<td><p>不支持的任何 Windows 操作系统</p></td>
</tr>
<tr class="even">
<td><p>已过时</p></td>
<td><p>特定于类的 VS 接口</p></td>
<td><p><strong>VS_FRAME_VENDOR</strong></p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>新</p></td>
<td><p>特定于类的 VS 接口</p></td>
<td><p><strong>VS_FORMAT_FRAME_BASED</strong></p></td>
<td></td>
</tr>
<tr class="even">
<td><p>新</p></td>
<td><p>特定于类的 VS 接口</p></td>
<td><p><strong>VS_FRAME_FRAME_BASED</strong></p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>新</p></td>
<td><p>特定于类的 VS 接口</p></td>
<td><p><strong>VS_FORMAT_STREAM_BASED</strong></p></td>
<td></td>
</tr>
</tbody>
</table>

 

对于 UVC 1.0 的设备，MPEG2TS 格式说明符的长度为 7。 由于 UVC 1.1 包括新的 16 字节 GUID 字段，MPEG2TS 格式说明符的长度为 23。

相应地，如果更新 MPEG2TS 描述符到 23 个字节，则还必须设置**bcdUVC** 0x110 类特定于 VC 接口中的标志。

 

 




