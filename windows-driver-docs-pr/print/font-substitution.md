---
title: 字体替换
description: 字体替换
keywords:
- 打印机字体说明 WDK Unidrv，替换
- 替换字体表 WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fdb7166a70c92c5255469aa8bd3273e1ac1e5b19
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836039"
---
# <a name="font-substitution"></a>字体替换





对于提供硬件驻留或墨盒字体的打印机，可以指定字体替换表。 通过提供字体替换表，你可以指定可替换必须下载的 TrueType 字体的硬件驻留或字体盒字体。 当 Unidrv 以这种 TrueType 字体接收文本时，它首先检查字体替换表是否包含字体的硬件驻留替换。 如果 Unidrv 发现替换的常驻字体，并且) 的字体指标 (（如字符集、粗细、斜体、方向等）兼容，则使用驻留字体。

可以通过使用一系列 TTFS 项来创建默认字体替换表 \* 。 每个条目的格式为：

<table>
<colgroup>
<col width="100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p></p>
* TTFS： <em>FontName</em> {* TTFontName： "<em>TTFontNameString</em>" * DevFontName： "<em>DeviceFontNameString</em>" <strong>}</strong></td>
</tr>
</tbody>
</table>

 

其中， *FontName* 是指定条目名称的符号， *TTFontNameString* 是用于标识要替换的 TrueType 字体的文本字符串，而 *DeviceFontNameString* 是用于标识要使用的硬件驻留或字体的文本字符串。 下面是一个示例表：

```cpp
*TTFS: Arial
{
    *TTFontName: "Arial"
    *DevFontName "Arial"
}
*TTFS: TNR
{
    *TTFontName: "Times New Roman"
    *DevFontName: "Times New Roman"
}
*TTFS: CurrierNew 
{
    *TTFontName:  "Courier New"
    *DevFontName: "Courier New"
}
```

如果有重复的 \* TTFS 条目具有相同的 *FontName* 值，则分析器读取的最后一个条目将取代上一个条目。

指定的替换表是一个默认表，因为 Unidrv 允许用户修改替换。

所有 \* TTFS 条目都必须位于 GPD 文件的根级别 (即，不在大括号) 内。

若要控制默认情况下是否启用字体替换，请使用 \* TTFSEnabled？条目。 此项的格式为：

<table>
<colgroup>
<col width="100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>* TTFSEnabled？： <em>BooleanValue</em></p></td>
</tr>
</tbody>
</table>

 

其中， *BooleanValue* 为 **TRUE** 或 **FALSE**。 如果 *BooleanValue* 为 **TRUE**，则 Unidrv 启用字体替换。 如果 *BooleanValue* 为 **FALSE**，或 \* 在 GPD 文件中未包含 TTFSEnabled？条目，则 Unidrv 将禁用字体替换，直到用户启用它。

\*TTFSEnable？项可重定位，但 \* TTFS 条目不能。  (有关可重定位条目的信息，请参阅 \*) 的 Switch、 \* Case 和 \* Default 语句中的位置。

### <a name="default-truetype-font-substitutions"></a>默认 TrueType 字体替换

在名为 ttfsub. gpd 的文件中提供了 TrueType 字体替换的默认表。 若要使用它，请在 GPD 文件的根级别添加以下条目 (即，不在大括号) ：

```cpp
*Include: "ttfsub.gpd"
```

此外，必须安装此文件。 有关详细信息，请参阅 [打印机 INF 文件安装部分](printer-inf-file-install-sections.md)。

 

 




