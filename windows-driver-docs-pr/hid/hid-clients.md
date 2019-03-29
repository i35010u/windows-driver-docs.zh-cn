---
title: HID 客户端
description: HID 客户端是设备的驱动程序、 服务或应用程序使用 HID API 进行通信，通常表示特定类型 （例如传感器、 键盘或鼠标）。
ms.assetid: C97E1F63-0CA5-42F3-A139-48E830F2E2B7
keywords:
- HID 客户端
- “驱动程序”
- 服务
- HID API
- HID 的集合
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 01d8aff5e988702bd2b133ec0488632ee7cb312c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563352"
---
# <a name="hid-clients"></a>HID 客户端


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
<td><p><a href="hid-usages.md" data-raw-source="[HID Usages](hid-usages.md)">HID 的用法</a></p></td>
<td><p><em>HID 的用法</em>标识 HID 控件和控件的实际测量的预期的用途。</p></td>
</tr>
<tr class="even">
<td><p><a href="hid-collections.md" data-raw-source="[HID Collections](hid-collections.md)">HID 的集合</a></p></td>
<td><p>一个<em>HID 集合</em>是有意义的 HID 控件和其各自分组<a href="hid-usages.md" data-raw-source="[HID usages](hid-usages.md)">HID 用法</a>。</p></td>
</tr>
<tr class="odd">
<td><p><a href="opening-hid-collections.md" data-raw-source="[Opening HID collections](opening-hid-collections.md)">打开 HID 集合</a></p></td>
<td><p>本部分介绍 HID 客户端之间的通信方式的 HID 类驱动程序 (HIDClass) 运行 HID 设备的集合。</p></td>
</tr>
<tr class="even">
<td><p><a href="handling-hid-reports.md" data-raw-source="[Handling HID Reports](handling-hid-reports.md)">处理 HID 报表</a></p></td>
<td><p>本部分介绍了用户模式应用程序和内核模式驱动程序用于处理的机制<a href="introduction-to-hid-concepts.md" data-raw-source="[HID reports](introduction-to-hid-concepts.md)">HID 报表</a>。</p></td>
</tr>
<tr class="odd">
<td><p><a href="freeing-resources.md" data-raw-source="[Freeing Resources](freeing-resources.md)">释放资源</a></p></td>
<td><p>用户模式应用程序和内核模式驱动程序的 HID 客户端应始终释放不再需要的任何资源。</p></td>
</tr>
<tr class="even">
<td><p><a href="installing-hid-clients.md" data-raw-source="[Installing HID clients](installing-hid-clients.md)">安装 HID 客户端</a></p></td>
<td><p>本部分介绍在 Microsoft Windows 中安装 HIDClass 设备的以下要求。</p></td>
</tr>
<tr class="odd">
<td><p><a href="hidclass-hardware-ids-for-top-level-collections.md" data-raw-source="[HIDClass Hardware IDs for Top-Level Collections](hidclass-hardware-ids-for-top-level-collections.md)">顶级集合的 HIDClass 硬件 Id</a></p></td>
<td><p>本部分中指定的硬件的 HID 类驱动程序生成为顶级集合的 Id。</p></td>
</tr>
<tr class="even">
<td><p><a href="keyboard-and-mouse-hid-client-drivers.md" data-raw-source="[Keyboard and mouse HID client drivers](keyboard-and-mouse-hid-client-drivers.md)">键盘和鼠标 HID 客户端驱动程序</a></p></td>
<td><p>本主题讨论键盘和鼠标 HID 客户端驱动程序。 键盘和鼠标表示 HID 客户端已标准化 HID 用法表中并在 Windows 操作系统中实现的第一个集。</p></td>
</tr>
<tr class="odd">
<td><p><a href="sensor-hid-class-driver.md" data-raw-source="[Sensor HID class driver](sensor-hid-class-driver.md)">传感器 HID 类驱动程序</a></p></td>
<td><p>Windows 操作系统从 Windows 8 开始，包括支持十一种类型的传感器，使用 HID 传输进行通信的内置传感器 HID 类驱动程序 (SensorsHIDClassDriver.dll)。</p></td>
</tr>
<tr class="even">
<td><p><a href="airplane-mode-radio-management.md" data-raw-source="[Airplane mode radio management](airplane-mode-radio-management.md)">飞行模式无线管理</a></p></td>
<td><p>从 Windows 8 开始，Windows 操作系统提供了通过 HID，对飞行模式单选管理控件的支持。</p></td>
</tr>
<tr class="odd">
<td><p><a href="display-brightness-control.md" data-raw-source="[Display brightness control](display-brightness-control.md)">显示的亮度控制</a></p></td>
<td><p>从 Windows 8 开始，已对标准化的解决方案已添加为允许键盘 （外部或嵌入在便携式计算机上），来控制通过 HID 的便携式计算机或平板电脑的屏幕亮度。</p></td>
</tr>
</tbody>
</table>

 

 

 




