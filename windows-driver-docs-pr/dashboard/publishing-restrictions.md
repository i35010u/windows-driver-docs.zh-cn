---
title: 发布限制
description: 以下各项在发布期间受限制。 仍可以为它们创建发货标签，但请求需要额外的 Microsoft 审查。
ms.topic: article
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c4560add393947861e94270dfe93ad73b63b781b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96800315"
---
# <a name="publishing-restrictions"></a>发布限制

以下各项在发布期间受限制。 仍可以为它们创建发货标签，但请求需要额外的 Microsoft 审查。

合作伙伴中心强制执行这些发布限制。 发布限制确保合作伙伴无法发布会覆盖 Microsoft 类驱动程序或通用总线 HWID 字符串的驱动程序。 这些限制还确保设备不会收到因通用第三方或重复使用的 HWID 导致的不正确驱动程序。

这些限制的示例包括，但不限于下表中的列表。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>限制类型</th>
<th>附加信息</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>无效的驱动程序提交类别类型</p></td>
<td><p>UNCLASSIFIED</p></td>
</tr>
<tr class="even">
<td><p>无效的体系结构</p></td>
<td><p>ia64</p></td>
</tr>
<tr class="odd">
<td><p>不带有总线枚举器的 HWID</p></td>
<td><p>N/A</p></td>
</tr>
<tr class="even">
<td><p>无效的总线枚举器</p></td>
<td><p>ActivCardBus</p>
<p>CIRCLASS</p>
<p>Hid\irdevice</p>
<p>Irbus</p>
<p>PS2_</p>
<p>MIDI</p>
<p>PNP</p>
<p>ACP</p>
<p>IAN</p>
<p>AVM</p>
<p>STREAM</p>
<p>DISPLAY</p></td>
</tr>
<tr class="odd">
<td><p>类代码声明</p></td>
<td><p>\CLASS</p>
<p>\CC</p>
<p>&</p></td>
</tr>
<tr class="even">
<td><p>分为两部分的 HWID</p></td>
<td><p>在 PCI 和 HDAUDIO 总线上强制执行</p></td>
</tr>
<tr class="odd">
<td><p>蓝牙 HWID（带有服务 UUID，没有供应商 ID 或产品 ID）</p></td>
<td><p>N/A</p></td>
</tr>
<tr class="even">
<td><p>无效的 PCI 供应商代码</p></td>
<td><p>0000</p>
<p>FFFF</p></td>
</tr>
<tr class="odd">
<td><p>缺少设备代码或产品 ID 代码</p></td>
<td><p>在 PCI 和 USB 总线上强制执行</p></td>
</tr>
<tr class="even">
<td><p>无效的 HWID 字符串开头</p></td>
<td><p>HID_DEVI</p>
<p>SERIAL_M</p>
<p>ISAPNP\PNP</p>
<p>SERENUM\PNP</p>
<p>PNP</p>
<p><em>PNP</p>
<p>BIOS\PNP</p>
<p>ACPI\PNP</p></td>
</tr>
<tr class="odd">
<td><p>系统保留的 HWID</p></td>
<td><p>BIOS\PNP</p>
<p>ACPI\PNP</p></td>
</tr>
<tr class="even">
<td><p>无效的 HWID</p></td>
<td><p></em>DONTUSE</p>
<p>SERIAL_MOUSE</p>
<p>Root\circlass</p>
<p>Hid\irdevice</p>
<p>Storage\VolumeSnapshot</p>
<p>Storage\Volume</p></td>
</tr>
</tbody>
</table>

有关驱动程序发布工作流的详细信息，请参阅 [Windows 10 驱动程序发布工作流](https://go.microsoft.com/fwlink/p/?LinkId=617374)。
