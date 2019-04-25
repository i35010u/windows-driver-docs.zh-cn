---
title: HID 驱动程序
description: 本部分介绍了人机接口设备（或 HID）。 通常情况下，这些设备是人们用来直接控制计算机系统操作的设备。
ms.assetid: 19aefe5f-d82a-411f-86ab-5d1d53191524
keywords:
- 指针设备 WDK
- 输入设备 WDK
- 人机接口设备 WDK
- HID WDK
ms.date: 04/20/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
ms.openlocfilehash: d6f8184fada8c5b4982a205d3f2d4541c6468061
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63365073"
---
# <a name="hid-drivers"></a>HID 驱动程序


本部分介绍了人机接口设备（或 HID）。 有关 HID 概念的详细信息，请参阅官方 [HID 规范](https://www.usb.org/hid)。 

## <a name="in-this-section"></a>本部分内容


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>主题</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="what-s-new-in-hid.md" data-raw-source="[What's New in HID](what-s-new-in-hid.md)">HID 中的新增功能</a></p></td>
<td></td>
</tr>
<tr class="even">
<td><p><a href="introduction-to-hid-concepts.md" data-raw-source="[Introduction to HID Concepts](introduction-to-hid-concepts.md)">HID 概念简介</a></p></td>
<td><p>本部分介绍了人机接口设备（或 HID）。 通常情况下，这些设备是人们用来直接控制计算机系统操作的设备。</p></td>
</tr>
<tr class="odd">
<td><p><a href="hid-architecture.md" data-raw-source="[HID Architecture](hid-architecture.md)">HID 体系结构</a></p></td>
<td><p>Windows 中的 HID 驱动程序堆栈的体系结构基于名为 <em>hidclass.sys</em> 的类驱动程序。</p></td>
</tr>
<tr class="even">
<td><p><a href="hid-clients-supported-in-windows.md" data-raw-source="[HID Clients Supported in Windows](hid-clients-supported-in-windows.md)">Windows 中支持的 HID 客户端</a></p></td>
<td><p>Windows 支持以下顶级集合：</p></td>
</tr>
<tr class="odd">
<td><p><a href="hid-transports-supported-in-windows.md" data-raw-source="[HID Transports Supported in Windows](hid-transports-supported-in-windows.md)">Windows 中支持的 HID 传输方式</a></p></td>
<td><p>Windows 支持以下传输方式。</p></td>
</tr>
<tr class="even">
<td><p><a href="hid-clients.md" data-raw-source="[HID Clients](hid-clients.md)">HID 客户端</a></p></td>
<td><p>HID 客户端是使用 HID API 进行通信的驱动程序、服务或应用程序，通常表示特定类型的设备（例如：传感器、键盘或鼠标）。 它们通过硬件 ID 或特定的 HID 集合来识别设备，并通过HID API 与 HID 集合进行通信。</p></td>
</tr>
<tr class="odd">
<td><p><a href="hid-transports.md" data-raw-source="[HID Transports](hid-transports.md)">HID 传输方式</a></p></td>
<td><p>在当前和以前版本的 Windows 中受支持的 HID 传输方式的说明。</p></td>
</tr>
<tr class="even">
<td><p><a href="non-hid-legacy-devices.md" data-raw-source="[Non-HID legacy devices](non-hid-legacy-devices.md)">非 HID 旧设备</a></p></td>
<td><p>本部分介绍了非 HID 键盘和鼠标的驱动程序、传输方式和筛选器驱动程序。 这些设备主要以 PS/2 传输方式运行。</p></td>
</tr>
</tbody>
</table>

 

 

 




