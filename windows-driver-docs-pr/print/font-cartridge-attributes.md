---
title: 字体墨盒特性
description: 字体墨盒特性
ms.assetid: d1f99322-9c77-428a-beb5-6d0ff166c3e5
keywords:
- 打印机字体说明 WDK Unidrv，盒式磁带
- 字体盒 WDK Unidrv
- 插件字体 WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d4072ce5fd3e5f6d5479f451ad6802efda50ebc5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521034"
---
# <a name="font-cartridge-attributes"></a>字体墨盒特性





下表包含属性可以包含在\*FontCartridge GPD 条目。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>属性名称</th>
<th>特性参数</th>
<th>备注</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong><em>CartridgeName</strong></p></td>
<td><p>表示插件名称的文本字符串。</p></td>
<td><p>必需的除非 *<strong>rcCartridgeNameID</strong>指定。</p></td>
</tr>
<tr class="even">
<td><p><strong></em>字体</strong></p></td>
<td><p>表示包含在插件中所提供的纵向和横向方向的字体的 RC_UFM 或 RC_FONT 资源标识符的列表。</p></td>
<td><p>在至少一个<em><strong>字体</strong>，*<strong>PortraitFonts</strong>或 *<strong>LandscapeFonts</strong>必须指定。 字体资源标识符应连续编号均为 1。</p></td>
</tr>
<tr class="odd">
<td><p><strong></em>LandscapeFonts</strong></p></td>
<td><p>表示仅适用于横向方向的字体包含在该插件的 RC_UFM 或 RC_FONT 资源标识符的列表。</p></td>
<td><p>在至少一个<em><strong>字体</strong>，*<strong>PortraitFonts</strong>或 *<strong>LandscapeFonts</strong>必须指定。 字体资源标识符应连续编号均为 1。</p></td>
</tr>
<tr class="even">
<td><p><strong></em>PortraitFonts</strong></p></td>
<td><p>表示仅适用于纵向方向的字体包含在该插件的 RC_UFM 或 RC_FONT 资源标识符的列表。</p></td>
<td><p>在至少一个<em><strong>字体</strong>，*<strong>PortraitFonts</strong>或 *<strong>LandscapeFonts</strong>必须指定。 字体资源标识符应连续编号均为 1。</p></td>
</tr>
<tr class="odd">
<td><p><strong></em>rcCartridgeNameID</strong></p></td>
<td><p>表示插件名称的字符串资源的资源标识符。</p></td>
<td><p>必需的除非 *<strong>CartridgeName</strong>指定。</p></td>
</tr>
</tbody>
</table>

 

 

 




