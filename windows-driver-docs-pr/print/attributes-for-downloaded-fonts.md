---
title: 下载字体属性
description: 下载字体属性
keywords:
- 下载的字体属性 WDK Unidrv
- 字体属性 WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 13af54b8fea2bb9f472ed15e706e9a3aaebbfca7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836121"
---
# <a name="attributes-for-downloaded-fonts"></a>下载字体属性





下表列出了描述打印机对下载字体的支持的属性。

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
<td><p><strong><em>DLSymbolSet</strong></p></td>
<td><p>常数，表示下载 TrueType 字体时要使用的符号集。 可以是 PC 8 或罗马8。</p></td>
<td><p>可选。 如果未指定此值，则认为标志符号范围在 *<strong>MinGlyphID</strong> 和 *<strong>MaxGlyphID</strong>指定的限制内是连续的。</p></td>
</tr>
<tr class="even">
<td><p><strong></em>FontFormat</strong></p></td>
<td><p></p>
指示支持的下载类型的常量值。 必须是以下项之一： HPPCL HPPCL_RES HPPCL_OUTLINE OEM_CALLBACK</td>
<td><p>如果打印机可下载字体，则为必需。 如果指定 OEM_CALLBACK，则必须提供字体回调函数。 有关这些回调的详细信息，请参阅 <a href="customizing-microsoft-s-printer-drivers.md" data-raw-source="[Customizing Microsoft's Printer Drivers](customizing-microsoft-s-printer-drivers.md)">自定义 Microsoft 的打印机驱动程序</a>。</p></td>
</tr>
<tr class="odd">
<td><p><strong><em>MaxFontID</strong></p></td>
<td><p>表示软字体的最大标识符的数字值。</p></td>
<td><p>可选。 如果未指定，则默认值为65535。</p></td>
</tr>
<tr class="even">
<td><p><strong></em>MaxGlyphID</strong></p></td>
<td><p>表示已下载字体标志符号的最大标识符的数字值。</p></td>
<td><p>可选。 如果未指定但未 <em> 指定<strong>DLSymbolSet</strong> ，则默认值为255。 如果指定 *<strong>DLSymbolSet</strong> ，则忽略。</p></td>
</tr>
<tr class="odd">
<td><p><strong></em>MaxNumDownFonts</strong></p></td>
<td><p>数值，表示一次可以存储在打印机内存中的软字体的最大数目。</p></td>
<td><p>可选。 如果未指定，Unidrv 将假定可以存储不限数量的软字体。</p></td>
</tr>
<tr class="even">
<td><p><strong><em>MinFontID</strong></p></td>
<td><p>表示软字体的最小标识符的数字值。</p></td>
<td><p>可选。 如果未指定，则默认值为1。</p></td>
</tr>
<tr class="odd">
<td><p><strong></em>MinGlyphID</strong></p></td>
<td><p>表示已下载字体标志符号的最小标识符的数字值。</p></td>
<td><p>可选。 如果未指定但未 <em> 指定<strong>DLSymbolSet</strong> ，则默认值为32。 如果指定 *<strong>DLSymbolSet</strong> ，则忽略。</p></td>
</tr>
<tr class="even">
<td><p><strong></em>TextHalftoneThreshold</strong></p></td>
<td><p>确定 Unidrv 是否为 TrueType 字体执行文本半色调的数值。 如果驱动程序的分辨率大于或等于此属性中指定的值，则 Unidrv 的半色调文本。</p></td>
<td><p>可选。 默认值是 600秒。</p></td>
</tr>
</tbody>
</table>

 

有关示例，请参阅 [示例 GPD 文件](sample-gpd-files.md)。

 

 




