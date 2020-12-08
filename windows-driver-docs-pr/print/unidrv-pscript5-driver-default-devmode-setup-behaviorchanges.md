---
title: Unidrv/PScript5 驱动程序的默认 DEVMODE 设置行为更改
description: Unidrv/PScript5 驱动程序的默认 DEVMODE 设置行为更改
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 28ec6bada0dd2aae9fd6f1680925ac2baeae6f8c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96820555"
---
# <a name="unidrvpscript5-driver-default-devmode-setup-behavior-changes"></a>Unidrv/PScript5 驱动程序的默认 DEVMODE 设置行为更改


在 XPSDrv 模式下运行的 Unidrv/PScript5 驱动程序会创建以下驱动程序默认 DEVMODE 设置行为更改。

下表中 ("仅 PS" 表示行为更改特定于 PScript5 驱动程序。 "仅 Unidrv" 表示行为更改特定于 Unidrv 驱动程序。 如果这两个短语都未出现，则行为更改适用于 Unidrv 和 PScript5 驱动程序。 ) 

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>受影响的默认 DEVMODE 字段</th>
<th>非 XPSDrv 行为</th>
<th>XPSDrv 行为</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>dmFields</strong>：</p>
<p>DM_ORIENTATION</p>
<p><strong>dmOrientation</strong></p></td>
<td><p>硬编码为在 <strong>dmFields</strong>中始终设置 DM_ORIENTATION 标志，并设置 <strong>dmOrientation</strong> = DMORIENT_PORTRAIT。</p></td>
<td><p>仅当 GPD 文件支持 "方向" GPD 功能时， (Unidrv 仅) 在 <strong>dmFields</strong> 中设置 DM_ORIENTATION 标志。 <strong>dmOrientation</strong> 是根据 GPD 文件中指定的 "取向" GPD 功能的默认选项设置的。</p>
<p>仅当 PPD 文件支持带有 "PageOrientation" Print Schema 关键字的功能时， (PS 仅) 在 <strong>dmFields</strong> 中设置 DM_ORIENTATION 标志。</p>
<p>如果<strong>dmOrientation</strong>设置为 "横向" 或 "ReverseLandscape" Print Schema 关键字，则将其设置为<strong>DMORIENT_LANDSCAPE</strong> 。 否则， <strong>dmOrientation</strong> 设置为 <strong>DMORIENT_PORTRAIT</strong>。</p></td>
</tr>
<tr class="even">
<td><p><strong>dmFields</strong>：</p>
<p>DM_SCALE</p></td>
<td><p> (Unidrv 仅) 硬编码，以便从不在 <strong>dmFields</strong>中设置 DM_SCALE 标志。</p>
<p> (PS 仅) 硬编码，始终在 <strong>dmFields</strong>中设置 DM_SCALE 标志。</p></td>
<td><p>仅当 GPD 或 PPD 支持带有 "PageScaling" Print Schema 关键字的功能时，才在 <strong>dmFields</strong> 中设置 DM_SCALE 标志。</p></td>
</tr>
<tr class="odd">
<td><p><strong>dmFields</strong>：</p>
<p>DM_TTOPTION</p>
<p><strong>dmTTOption</strong></p></td>
<td><p>硬编码为在 dmFields 中始终设置 DM_TTOPTION 标志，并设置 dmTTOption = DMTT_SUBDEV。</p></td>
<td><p>如果 GPD 或 PPD 支持带有 "PageDeviceFontSubstitution" print schema 关键字的功能，并且该功能具有 "打开" 打印架构关键字的默认选项，请设置 DM_TTOPTION 标志并设置<strong>dmTTOption</strong>  =  <strong>DMTT_SUBDEV</strong>。</p>
<p>否则，如果 GPD 或 PPD 支持带有 "PageTrueTypeFontMode" Print Schema 关键字的功能和以下之一：</p>
<ul>
<li><p>如果该功能具有 "DownloadAsOutlineFont" 打印架构关键字的默认选项，请设置 DM_TTOPTION 标志并设置<strong>dmTTOption</strong>  =  <strong>DMTT_DOWNLOAD_OUTLINE</strong>。</p></li>
<li><p>如果该功能具有 "RenderAsBitmap" 打印架构关键字的默认选项，请设置 DM_TTOPTION 标志并设置<strong>dmTTOption</strong>  =  <strong>DMTT_BITMAP</strong>;</p></li>
<li><p>如果该功能具有 "自动"、"DownloadAsRasterFont" 或 "DownloadAsNativeTrueTypeFont" 打印架构关键字的默认选项，请设置 DM_TTOPTION 标志并设置<strong>dmTTOption</strong>  =  <strong>DMTT_DOWNLOAD</strong>。</p></li>
</ul>
<p>否则，将在 <strong>dmFields</strong> 中清除 DM_TTOPTION 标志，因为打印机不会指示它支持 TrueType 字体替换或下载。</p></td>
</tr>
<tr class="even">
<td><p><strong>dmFields</strong>：</p>
<p>DM_NUP</p></td>
<td><p>硬编码为始终在 <strong>dmFields</strong>中设置 DM_NUP 标志。</p></td>
<td><p>仅当 GPD 或 PPD 支持带有 "JobNUpAllDocumentsContiguously" 或 "DocumentNUp" 打印架构关键字的功能时，才在 <strong>dmFields</strong> 中设置 DM_NUP 标志。</p></td>
</tr>
<tr class="odd">
<td><p><strong>dmFields</strong>：</p>
<p>DM_COLOR</p></td>
<td><p>硬编码为始终在 <strong>dmFields</strong>中设置 DM_COLOR 标志。</p></td>
<td><p>仅当 GPD 或 PPD 指定打印机为彩色打印机时，才在 <strong>dmFields</strong> 中设置 DM_COLOR 标志。</p></td>
</tr>
<tr class="even">
<td><p><strong>dmFields</strong>：</p>
<p>DM_PRINTQUALITY，DM_YRESOLUTION</p></td>
<td><p> (Unidrv 仅) 硬编码，以便始终在 <strong>dmFields</strong>中设置 DM_PRINTQUALITY 标志。</p>
<p> (PS 仅) 硬编码，始终在 <strong>dmFields</strong>中设置 DM_PRINTQUALITY 和 DM_YRESOLUTION 标志。</p></td>
<td><p>仅当 GPD 或 PPD 支持 "解决" GPD 或 PPD 功能时，才在 <strong>dmFields</strong> 中设置 DM_PRINTQUALITY 和 DM_YRESOLUTION 标志。</p></td>
</tr>
<tr class="odd">
<td><p><strong>dmFields</strong>：</p>
<p>DM_COLLATE</p>
<p><strong>dmCollate</strong></p></td>
<td><p>硬编码为在 <strong>dmFields</strong>中始终设置 DM_COLLATE 标志，并设置 <strong>dmCollate</strong> = DMCOLLATE_TRUE。</p></td>
<td><p>仅当 GPD 或 PPD 支持 "Collate" GPD 或 PPD 功能时，才在 <strong>dmFields</strong> 中设置 DM_COLLATE 标志。 <strong>dmCollate</strong> 是基于在 GPD 或 ppd 中指定的 "COLLATE" GPD 或 ppd 功能的默认选项设置的。</p></td>
</tr>
<tr class="even">
<td><p><strong>dmFields</strong>：</p>
<p>DM_ICMMETHOD，DM_ICMINTENT</p></td>
<td><p> (Unidrv 仅) 硬编码，以便始终在 <strong>dmFields</strong>中设置 DM_ICMMETHOD 和 DM_ICMINTENT 标志。</p>
<p>仅 (PS) 如果 PPD 指定打印机是彩色打印机，请在 <strong>dmFields</strong>中设置 DM_ICMMETHOD 和 DM_ICMINTENT 标志。</p></td>
<td><p>切勿在 <strong>dmFields</strong>中设置 DM_ICMMETHOD 或 DM_ICMINTENT 标志。</p></td>
</tr>
<tr class="odd">
<td><p><strong>dmFields</strong>：</p>
<p>DM_DITHERTYPE</p></td>
<td><p> (Unidrv 仅) 硬编码，以便始终在 <strong>dmFields</strong>中设置 DM_DITHERTYPE 标志。</p></td>
<td><p> (Unidrv 仅) 从不在 <strong>dmFields</strong>中设置 DM_DITHERTYPE 标志。</p></td>
</tr>
</tbody>
</table>

 

 

 




