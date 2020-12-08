---
title: Win32 DeviceCapabilities API 行为更改
description: Win32 DeviceCapabilities API 行为更改
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bdb1d084c247e08c3777ad66adc4144cf637f92e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96831189"
---
# <a name="win32-devicecapabilities-api-behavior-changes"></a>Win32 DeviceCapabilities API 行为更改


在 XPSDrv 模式下运行的 Unidrv/PScript5 驱动程序在 Microsoft Win32 **DeviceCapabilities** 函数中创建了以下更改。

使用 GPD 的 **PrintSchemaKeywordMap** 或 Ppd 的 **MSPRINTSCHEMAKEYWORDMAP** 关键字将 GPD/PPD 功能或选项映射到打印架构关键字时，GPD 或 ppd 支持该打印架构关键字。

下表中 ("仅 PS" 表示行为更改特定于 PScript5 驱动程序。 "仅 Unidrv" 表示行为更改特定于 Unidrv 驱动程序。 如果这两个短语都未出现，则行为更改适用于 Unidrv 和 PScript5 驱动程序。 ) 

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
<td><p> (Unidrv 仅) 启用了 EMF 后， <strong>DeviceCapabilitiesreturns</strong> 为最大值9999或 GPD 文件的指定 * MaxCopies 值的硬编码值。</p>
<p>禁用 EMF 后， <strong>DeviceCapabilities</strong> 将返回 GPD * MaxCopies 值。</p>
<p>仅 (PS) <strong>DeviceCapabilities</strong> 返回硬编码的值9999。</p></td>
<td><p> (Unidrv 仅) <strong>DeviceCapabilities</strong> 返回 GPD * MaxCopies 值。</p>
<p>仅 (PS) <strong>DeviceCapabilities</strong> 返回 ppd 文件的 * MSXPSMaxCopies 值; 如果未在 PPD 文件中指定该值，则返回1。</p></td>
</tr>
<tr class="even">
<td><p>DC_TRUETYPE</p></td>
<td><p>对于 Unidrv，如果指定了 * FontFormat GPD 关键字， <strong>DeviceCapabilities</strong> 将返回 (DCTT_BITMAP |DCTT_DOWNLOAD) ;否则， <strong>DeviceCapabilities</strong> 将返回 DCTT_BITMAP。</p>
<p>对于 PS， <strong>DeviceCapabilities</strong> 始终返回 (DCTT_DOWNLOAD |DCTT_SUBDEV) 。</p></td>
<td><p>如果 GPD 或 PPD 支持带有 "PageDeviceFontSubstitution" Print Schema 关键字的功能，则将在返回值中设置 DCTT_SUBDEV 标志。</p>
<p>如果 GPD 或 PPD 支持带有 "PageTrueTypeFontMode" Print Schema 关键字的功能，则会发生以下情况：</p>
<ul>
<li><p>如果该功能支持带有 "DownloadAsOutlineFont" Print Schema 关键字的选项，则会在返回值中设置 DCTT_DOWNLOAD 和 DCTT_DOWNLOAD_OUTLINE 标志。</p></li>
<li><p>如果该功能支持带有 "Automatic"、"DownloadAsRasterFont" 或 "DownloadAsNativeTrueTypeFont" Print Schema 关键字的选项，则将在返回值中设置 DCTT_DOWNLOAD 标志。</p></li>
<li><p>如果该功能支持带有 "RenderAsBitmap" Print Schema 关键字的选项，则将在返回值中设置 DCTT_BITMAP 标志。</p></li>
</ul>
<p>如果未设置 DCTT_<em>Xxx</em> 标志，则 <strong>DeviceCapabilities</strong> 将返回0。</p></td>
</tr>
<tr class="odd">
<td><p>DC_ORIENTATION</p></td>
<td><p>仅 (PS) <strong>DeviceCapabilities</strong> 基于 PPD 的 * LandscapeOrientation 值返回90或270，并为输入 DEVMODE 结构中的硬编码旋转横向方向选项设置。</p></td>
<td><p>仅 (PS) 默认返回值为0，这意味着没有横向方向。</p>
<p>如果 PPD 支持带有 "PageOrientation" Print Schema 关键字的功能，则会发生以下情况：</p>
<ul>
<li><p>如果该功能支持带有 "横向" Print Schema 关键字的选项，则 <strong>DeviceCapabilities</strong> 将返回90。</p></li>
<li><p>如果该功能支持带有 "ReverseLandscape" Print Schema 关键字的选项，则 <strong>DeviceCapabilities</strong> 将返回270。</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>DC_COLLATE</p></td>
<td><p>启用 EMF 后， <strong>DeviceCapabilities</strong> 会硬编码为返回 1 (这意味着将支持对) 进行排序。</p>
<p>禁用 EMF 后，如果 GPD 或 PPD 将 Collate 指定为支持的功能，并且逐份打印 GPD 或 PPD 功能不受任何设备设置功能的约束，则 <strong>DeviceCapabilities</strong> 返回1。 否则， <strong>DeviceCapabilities</strong> 将返回0。</p></td>
<td><p>此行为与禁用 EMF 的非 XPSDrv 驱动程序的行为相同。</p></td>
</tr>
<tr class="odd">
<td><p>DC_NUP</p></td>
<td><p><strong>DeviceCapabilities</strong> 返回硬编码值，以指示支持1、2、4、6、9或16个 ups。</p></td>
<td><p>如果 GPD 或 PPD 使用 "DocumentNUp" 打印架构关键字定义了一项功能 (仅当不存在 "JobNUpAllDocumentsContiguously" 功能时才使用 "DocumentNUp" 功能) 然后，对于该功能的任何选项，该功能的选项 GPD/PPD 关键字 name 作为数字编号 (即1、2、6等) ，该数字将报告为每个工作表值支持的页面之一。</p>
<p>否则，XPSDrv 将报告不支持 NUp。</p></td>
</tr>
<tr class="even">
<td><p>DC_PERSONALITY</p></td>
<td><p>Unidrv 返回由 * 个性或 * rcPersonalityID GPD 关键字定义的字符串。</p>
<p>PS 始终返回 "PostScript"。</p></td>
<td><p>使行为与非 XPSDrv 驱动程序的行为相同。</p></td>
</tr>
<tr class="odd">
<td><p>DC_MEDIAREADY</p></td>
<td><p>如果已创建 Form-Tray 分配表，则 <strong>DeviceCapabilities</strong> 将返回表中列出的具有分配的托盘的唯一窗体名称。</p>
<p>如果尚未创建 Form-Tray 分配表，则对于非指标系统默认区域设置， <strong>DeviceCapabilities</strong> 将返回 "letter"; 对于指标系统默认区域设置，则返回 GPD 或 PPD 定义的默认纸张大小（如果打印机不支持 "Letter" 和 "A4"。</p></td>
<td><p>此行为与未创建窗体托盘分配表的非 XPSDrv 相同。</p></td>
</tr>
<tr class="even">
<td><p>DC_STAPLE</p></td>
<td><p>仅 (PS) 使用 PPD 时，o't 只有一个 "装订" 功能。 PScript5 驱动程序将检查 PPD 中是否定义了以下任一 PPD 功能，并且这些功能是否不受设备设置的约束，以确定设备是否可以支持装订。</p>
<ul>
<li><p>"StapleLocation"</p></li>
<li><p>"StapleX", "StapleY"</p></li>
<li><p>"StapleWhen"</p></li>
<li><p>"StapleOrientation"</p></li>
</ul></td>
<td><p>仅 (PS) 如果 PPD 支持带有 "JobStapleAllDocuments" 或 "DocumentStaple" 打印架构关键字的功能，则 <strong>DeviceCapabilities</strong> 返回1以指示支持装订。 否则， <strong>DeviceCapabilities</strong> 将返回0。</p></td>
</tr>
</tbody>
</table>

 

 

 




