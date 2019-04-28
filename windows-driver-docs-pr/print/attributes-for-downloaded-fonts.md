---
title: 下载字体属性
description: 下载字体属性
ms.assetid: 335413d0-cf0a-4dd9-b1a4-345945c63395
keywords:
- 下载的字体属性 WDK Unidrv
- 字体属性 WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b12c310b3089961b40335a729b68e24f5d279b0b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331197"
---
# <a name="attributes-for-downloaded-fonts"></a>下载字体属性





下表列出了属性描述对下载的字体的打印机的支持。

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
<td><p><strong><em>DLSymbolSet</strong></p></td>
<td><p>常量，表示设置下载 TrueType 字体时要使用的符号。 可以是 PC 8 或 ROMAN 8。</p></td>
<td><p>可选。 如果未指定，字形范围被假定为指定的限制范围内连续 *<strong>MinGlyphID</strong>和 *<strong>MaxGlyphID</strong>。</p></td>
</tr>
<tr class="even">
<td><p><strong></em>FontFormat</strong></p></td>
<td><p></p>
常量值，该值指示下载支持的类型。 必须是以下值之一：为 HPPCL HPPCL_RES HPPCL_OUTLINE OEM_CALLBACK</td>
<td><p>所需打印机可以下载字体。 如果指定 OEM_CALLBACK，则必须提供字体回调函数。 有关这些回叫的详细信息，请参阅<a href="customizing-microsoft-s-printer-drivers.md" data-raw-source="[Customizing Microsoft's Printer Drivers](customizing-microsoft-s-printer-drivers.md)">自定义 Microsoft 的打印机驱动程序</a>。</p></td>
</tr>
<tr class="odd">
<td><p><strong><em>MaxFontID</strong></p></td>
<td><p>表示为软字体的最大标识符的数字值。</p></td>
<td><p>可选。 如果未指定，默认值为 65535。</p></td>
</tr>
<tr class="even">
<td><p><strong></em>MaxGlyphID</strong></p></td>
<td><p>表示下载的字体标志符号的最大标识符的数字值。</p></td>
<td><p>可选。 如果未指定并<em> <strong>DLSymbolSet</strong>未指定，默认值为 255。 已忽略的如果 *<strong>DLSymbolSet</strong>指定。</p></td>
</tr>
<tr class="odd">
<td><p><strong></em>MaxNumDownFonts</strong></p></td>
<td><p>表示可以一次在打印机内存中存储的软字体的最大数目的数字值。</p></td>
<td><p>可选。 如果未指定，Unidrv 假定可以存储无限的数量的软字体。</p></td>
</tr>
<tr class="even">
<td><p><strong><em>MinFontID</strong></p></td>
<td><p>表示为软字体的最小标识符的数字值。</p></td>
<td><p>可选。 如果未指定，默认值是一个。</p></td>
</tr>
<tr class="odd">
<td><p><strong></em>MinGlyphID</strong></p></td>
<td><p>表示下载的字体标志符号的最小标识符的数字值。</p></td>
<td><p>可选。 如果未指定并<em> <strong>DLSymbolSet</strong>未指定，默认值为 32。 已忽略的如果 *<strong>DLSymbolSet</strong>指定。</p></td>
</tr>
<tr class="even">
<td><p><strong></em>TextHalftoneThreshold</strong></p></td>
<td><p>确定 Unidrv 是否执行 TrueType 字体中的文本半色调的数字值。 如果驱动程序的分辨率大于或等于此属性，Unidrv 半色调文本中指定的值。</p></td>
<td><p>可选。 默认值为 600。</p></td>
</tr>
</tbody>
</table>

 

有关示例，请参阅[示例 GPD 文件](sample-gpd-files.md)。

 

 




