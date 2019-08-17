---
title: HID 客户端概述
description: HID 客户端是使用 HID API 进行通信的驱动程序、服务或应用程序, 通常表示特定类型的设备 (例如传感器、键盘或鼠标)。
ms.assetid: C97E1F63-0CA5-42F3-A139-48E830F2E2B7
keywords:
- HID 客户端
- “驱动程序”
- 服务
- HID API
- HID 集合
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ee66f22cf9113910bd9acb908418469638e5a8ca
ms.sourcegitcommit: fec48fa5342d9cd4cd5ccc16aaa06e7c3d730112
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2019
ms.locfileid: "69565627"
---
# <a name="hid-clients-overview"></a>HID 客户端概述


HID 客户端是使用 HID API 进行通信的驱动程序、服务或应用程序，通常表示特定类型的设备（例如：传感器、键盘或鼠标）。 它们通过硬件 ID 或特定的 HID 集合来识别设备，并通过HID API 与 HID 集合进行通信。

## <a name="in-this-section"></a>本节内容


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
<td><p><a href="hid-usages.md" data-raw-source="[HID Usages](hid-usages.md)">HID 用法</a></p></td>
<td><p><em>Hid 用法</em>标识 hid 控件的用途以及控件实际度量的内容。</p></td>
</tr>
<tr class="even">
<td><p><a href="hid-collections.md" data-raw-source="[HID Collections](hid-collections.md)">HID 集合</a></p></td>
<td><p><em>Hid 集合</em>是有意义的 hid 控件和它们各自的<a href="hid-usages.md" data-raw-source="[HID usages](hid-usages.md)">hid 用法</a>的分组。</p></td>
</tr>
<tr class="odd">
<td><p><a href="opening-hid-collections.md" data-raw-source="[Opening HID collections](opening-hid-collections.md)">打开 HID 集合</a></p></td>
<td><p>本部分介绍 HID 客户端如何与 HID 类驱动程序 (HIDClass) 进行通信, 以便操作设备的 HID 集合。</p></td>
</tr>
<tr class="even">
<td><p><a href="handling-hid-reports.md" data-raw-source="[Handling HID Reports](handling-hid-reports.md)">处理 HID 报表</a></p></td>
<td><p>本部分介绍用户模式应用程序和内核模式驱动程序用于处理<a href="introduction-to-hid-concepts.md" data-raw-source="[HID reports](introduction-to-hid-concepts.md)">HID 报表</a>的机制。</p></td>
</tr>
<tr class="odd">
<td><p><a href="freeing-resources.md" data-raw-source="[Freeing Resources](freeing-resources.md)">释放资源</a></p></td>
<td><p>作为 HID 客户端的用户模式的应用程序和内核模式驱动程序应始终释放不再需要的任何资源。</p></td>
</tr>
<tr class="even">
<td><p><a href="installing-hid-clients.md" data-raw-source="[Installing HID clients](installing-hid-clients.md)">安装 HID 客户端</a></p></td>
<td><p>本部分介绍在 Microsoft Windows 中安装 HIDClass 设备的以下要求。</p></td>
</tr>
<tr class="odd">
<td><p><a href="hidclass-hardware-ids-for-top-level-collections.md" data-raw-source="[HIDClass Hardware IDs for Top-Level Collections](hidclass-hardware-ids-for-top-level-collections.md)">HIDClass 顶级集合的硬件 Id</a></p></td>
<td><p>此部分指定 HID 类驱动程序为顶级集合生成的硬件 Id。</p></td>
</tr>
<tr class="even">
<td><p><a href="keyboard-and-mouse-hid-client-drivers.md" data-raw-source="[Keyboard and mouse HID client drivers](keyboard-and-mouse-hid-client-drivers.md)">键盘和鼠标 HID 客户端驱动程序</a></p></td>
<td><p>本主题讨论键盘和鼠标 HID 客户端驱动程序。 键盘和鼠标表示在 HID 使用情况表中进行标准化并在 Windows 操作系统中实现的第一组 HID 客户端。</p></td>
</tr>
<tr class="odd">
<td><p><a href="sensor-hid-class-driver.md" data-raw-source="[Sensor HID class driver](sensor-hid-class-driver.md)">传感器 HID 类驱动程序</a></p></td>
<td><p>从 Windows 8 开始, Windows 操作系统包含一个内置的传感器 HID 类驱动程序 (SensorsHIDClassDriver), 该驱动程序支持使用 HID 传输进行通信的第11种传感器类型。</p></td>
</tr>
<tr class="even">
<td><p><a href="airplane-mode-radio-management.md" data-raw-source="[Airplane mode radio management](airplane-mode-radio-management.md)">飞行模式无线电管理</a></p></td>
<td><p>从 Windows 8 开始, Windows 操作系统将通过 HID 为飞行模式无线电管理控制提供支持。</p></td>
</tr>
<tr class="odd">
<td><p><a href="display-brightness-control.md" data-raw-source="[Display brightness control](display-brightness-control.md)">显示亮度控件</a></p></td>
<td><p>从 Windows 8 开始, 已添加标准化的解决方案, 以允许键盘 (外置或嵌入在便携式计算机上) 通过 HID 控制便携式计算机或平板电脑的屏幕亮度。</p></td>
</tr>
</tbody>
</table>

 

 

 




