---
title: 字体盒属性
description: 字体盒属性
keywords:
- 打印机字体说明 WDK Unidrv、盒式磁带
- 字体盒式 WDK Unidrv
- 字体盒式 WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7f4021a3dce7251a7031117242a0fea00f7fc533
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836041"
---
# <a name="font-cartridge-attributes"></a>字体盒属性





下表包含可包含在 \* FONTCARTRIDGE GPD 条目中的属性。

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
<th>注释</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong><em>CartridgeName</strong></p></td>
<td><p>表示磁带盒名称的文本字符串。</p></td>
<td><p>必需，除非指定 *<strong>rcCartridgeNameID</strong> 。</p></td>
</tr>
<tr class="even">
<td><p><strong></em>字体</strong></p></td>
<td><p>RC_UFM 或 RC_FONT 资源标识符的列表，它们表示磁带盒中包含的、纵向和横向方向可用的字体。</p></td>
<td><p>至少必须指定一种 <em> <strong>字体</strong>，*<strong>PortraitFonts</strong>或 *<strong>LandscapeFonts</strong> 。 字体资源标识符应连续从1开始编号。</p></td>
</tr>
<tr class="odd">
<td><p><strong></em>LandscapeFonts</strong></p></td>
<td><p>RC_UFM 或 RC_FONT 资源标识符的列表，这些标识符表示盒中包含的字体，这些字体仅适用于横向打印。</p></td>
<td><p>至少必须指定一种 <em> <strong>字体</strong>，*<strong>PortraitFonts</strong>或 *<strong>LandscapeFonts</strong> 。 字体资源标识符应连续从1开始编号。</p></td>
</tr>
<tr class="even">
<td><p><strong></em>PortraitFonts</strong></p></td>
<td><p>RC_UFM 或 RC_FONT 资源标识符的列表，它们代表盒中包含的字体，这些字体仅可用于纵向显示。</p></td>
<td><p>至少必须指定一种 <em> <strong>字体</strong>，*<strong>PortraitFonts</strong>或 *<strong>LandscapeFonts</strong> 。 字体资源标识符应连续从1开始编号。</p></td>
</tr>
<tr class="odd">
<td><p><strong></em>rcCartridgeNameID</strong></p></td>
<td><p>表示磁带盒名称的字符串资源的资源标识符。</p></td>
<td><p>必需，除非指定 *<strong>CartridgeName</strong> 。</p></td>
</tr>
</tbody>
</table>

 

 

 




