---
title: Win32 DeviceCapabilities API 行为更改
description: Win32 DeviceCapabilities API 行为更改
ms.assetid: 44745e33-2bd8-4200-be29-b3ddb0e30de4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9631053a57ee794600b353d06f4bcbce48bcbe52
ms.sourcegitcommit: d334150abe0b189faf33049908af7aab1458c13d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57463902"
---
# <a name="win32-devicecapabilities-api-behavior-changes"></a>Win32 DeviceCapabilities API 行为更改


在 XPSDrv 模式下运行的 Unidrv/PScript5 驱动程序创建 Microsoft Win32 中的以下更改**DeviceCapabilities**函数。

当 GPD/PPD 功能或选项使用映射到打印架构关键字 GPD 的**PrintSchemaKeywordMap**或 PPD 的**MSPrintSchemaKeywordMap**关键字、 GPD 或 PPD 打印架构关键字的支持。

（在下表中，"仅 PS"方法的行为更改为特定于 PScript5 驱动程序。 "仅 Unidrv"平均值的行为更改是特定于 Unidrv 驱动程序。 如果未显示这两个这些短语，行为更改适用于 Unidrv 和 PScript5 驱动程序。）

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>功能</th>
<th>非 XPSDrv 行为</th>
<th>XPSDrv 行为</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>DC_COPIES</p></td>
<td><p>(仅 Unidrv)启用 EMF 后， <strong>DeviceCapabilitiesreturns</strong>是 9999 的最大值或 GPD 文件硬编码值的指定 * MaxCopies 值。</p>
<p>当禁用 EMF 时， <strong>DeviceCapabilities</strong>返回 GPD * MaxCopies 值。</p>
<p>(仅 PS)<strong>DeviceCapabilities</strong>返回 9999 硬编码值。</p></td>
<td><p>(仅 Unidrv)<strong>DeviceCapabilities</strong>返回 GPD * MaxCopies 值。</p>
<p>(仅 PS)<strong>DeviceCapabilities</strong>返回 PPD 文件 * MSXPSMaxCopies 值或如果未在 PPD 文件中指定的值为 1。</p></td>
</tr>
<tr class="even">
<td><p>DC_TRUETYPE</p></td>
<td><p>有关 Unidrv，如果 * 指定 FontFormat GPD 关键字，则<strong>DeviceCapabilities</strong>返回 (DCTT_BITMAP |DCTT_DOWNLOAD);否则为<strong>DeviceCapabilities</strong>返回 DCTT_BITMAP。</p>
<p>用于 PS <strong>DeviceCapabilities</strong>始终返回 (DCTT_DOWNLOAD |DCTT_SUBDEV)。</p></td>
<td><p>如果 GPD 或 PPD 支持具有"PageDeviceFontSubstitution"打印架构关键字的功能，将返回值中设置 DCTT_SUBDEV 标志。</p>
<p>如果 GPD 或 PPD 支持具有"PageTrueTypeFontMode"打印架构关键字的功能，请执行以下操作：</p>
<ul>
<li><p>如果该功能支持使用"DownloadAsOutlineFont"打印架构关键字选项，将返回值中设置 DCTT_DOWNLOAD 和 DCTT_DOWNLOAD_OUTLINE 标志。</p></li>
<li><p>如果该功能支持使用"自动"、"DownloadAsRasterFont"或"DownloadAsNativeTrueTypeFont"打印架构关键字选项，将返回值中设置 DCTT_DOWNLOAD 标志。</p></li>
<li><p>如果该功能支持使用"RenderAsBitmap"打印架构关键字选项，将返回值中设置 DCTT_BITMAP 标志。</p></li>
</ul>
<p>如果没有 DCTT_<em>Xxx</em>设置标志， <strong>DeviceCapabilities</strong>返回 0。</p></td>
</tr>
<tr class="odd">
<td><p>DC_ORIENTATION</p></td>
<td><p>(仅 PS)<strong>DeviceCapabilities</strong>返回 90 或 270 基于 PPD 的 * LandscapeOrientation 值和设置硬编码旋转横向方向的选项输入 DEVMODE 结构中。</p></td>
<td><p>(仅 PS)默认返回值为 0，这意味着没有横向方向。</p>
<p>如果 PPD 支持具有"PageOrientation"打印架构关键字的功能，会发生以下情况：</p>
<ul>
<li><p>如果该功能支持使用"横向"Print Schema 关键字，选项<strong>DeviceCapabilities</strong>返回 90。</p></li>
<li><p>如果该功能支持使用"ReverseLandscape"Print Schema 关键字，选项<strong>DeviceCapabilities</strong>返回 270。</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>DC_COLLATE</p></td>
<td><p>启用 EMF 后， <strong>DeviceCapabilities</strong>是硬编码返回 1 （这意味着，支持排序规则）。</p>
<p>当禁用 EMF 时， <strong>DeviceCapabilities</strong>如果 GPD 或 PPD 指定 Collate 作为受支持的功能和逐份打印 GPD 或 PPD 功能不受任何设备设置功能，则返回 1。 否则为<strong>DeviceCapabilities</strong>返回 0。</p></td>
<td><p>行为是使用 EMF 禁用非 XPSDrv 驱动程序的一样。</p></td>
</tr>
<tr class="odd">
<td><p>DC_NUP</p></td>
<td><p><strong>DeviceCapabilities</strong>返回硬编码的值，以指示对 1、 2、 4、 6、 9 或 16 ups 的支持。</p></td>
<td><p>如果 GPD 或 PPD 定义了一项功能与"DocumentNUp"Print Schema 关键字 （仅如果没有"JobNUpAllDocumentsContiguously"的功能存在，则使用"DocumentNUp"功能），然后，对于该功能的任何具有数字形式的选项 GPD/PPD 关键字名称的选项数字 （即 1、 2、 6 和等等），数值的数字将被报告为每个表值的支持页面之一。</p>
<p>否则，将报告 XPSDrv NUp 不受支持。</p></td>
</tr>
<tr class="even">
<td><p>DC_PERSONALITY</p></td>
<td><p>Unidrv 返回字符串由定义 * 个性或 * rcPersonalityID GPD 关键字。</p>
<p>PS 始终返回"PostScript"。</p></td>
<td><p>保留行为相同按原样非 XPSDrv 驱动程序。</p></td>
</tr>
<tr class="odd">
<td><p>DC_MEDIAREADY</p></td>
<td><p>如果曾经创建窗体的送纸器分配表， <strong>DeviceCapabilities</strong>返回具有分配的送纸器的表中唯一的窗体名称列出。</p>
<p>如果尚未创建窗体的送纸器分配表， <strong>DeviceCapabilities</strong>指标系统默认区域设置、"A4"的指标系统默认区域设置，或 GPD 或 PPD 定义默认纸张大小，如果打印机返回"号"支持"字母"和"A4"。</p></td>
<td><p>行为是与非 XPSDrv 创建含窗体的送纸器分配表相同。</p></td>
</tr>
<tr class="even">
<td><p>DC_STAPLE</p></td>
<td><p>(仅 PS)PPD 作用 o't 有单个"装订"功能。 PScript5 驱动程序检查是否以下 PPD 功能 PPD 中定义，且不受设备设置来确定设备是否可以支持装订。</p>
<ul>
<li><p>"StapleLocation"</p></li>
<li><p>"StapleX", "StapleY"</p></li>
<li><p>"StapleWhen"</p></li>
<li><p>"StapleOrientation"</p></li>
</ul></td>
<td><p>(仅 PS)如果 PPD 支持具有"JobStapleAllDocuments"或"DocumentStaple"打印架构关键字的功能<strong>DeviceCapabilities</strong>返回 1，表示支持装订。 否则为<strong>DeviceCapabilities</strong>返回 0。</p></td>
</tr>
</tbody>
</table>

 

 

 




