---
title: 使用 GDI 每像素 8 位 CMY 掩码模式
description: 使用 GDI 每像素 8 位 CMY 掩码模式
ms.assetid: 0631f292-c1f1-4627-b116-0b54a34ea295
keywords:
- GDI WDK Windows 2000 显示、 半色调
- 图形驱动程序 WDK Windows 2000 显示、 半色调
- 绘制 WDK GDI、 半色调
- 半色调 WDK GDI
- 每像素 8 位 CMY 掩码模式 WDK GDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 32dad429bf1ce8b92fa66ffeeb4eca5bb1e95c0f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63389031"
---
# <a name="using-gdi-8-bit-per-pixel-cmy-mask-modes"></a>使用 GDI 每像素 8 位 CMY 掩码模式


## <span id="ddk_using_gdi_8_bit_per_pixel_cmy_mask_modes_gg"></span><span id="DDK_USING_GDI_8_BIT_PER_PIXEL_CMY_MASK_MODES_GG"></span>


在 Microsoft Windows 2000 [ **HT\_Get8BPPMaskPalette** ](https://msdn.microsoft.com/library/windows/hardware/ff567320)函数返回 8 位 / 像素的单色或 CMY 调色板。 此函数在 Windows XP 及更高版本，已修改以致它还会返回倒排索引 CMY 调色板时*Use8BPPMaskPal*参数设置为**TRUE**。 返回的调色板的类型取决于存储中的值*pPaletteEntry*\[0\]时**HT\_Get8BPPMaskPalette**调用。 如果*pPaletteEntry*\[0\]设置倒排索引调色板返回到 RGB0。 如果*pPaletteEntry*\[0\]设置为 0，返回正常 CMY 调色板。

此行为的更改的原因**HT\_Get8BPPMaskPalette**是，当 Windows GDI 使用 ROPs，基于调色板中的索引而不是在调色板颜色，它假定该索引 0 的调色板的始终是黑色和最后一个索引始终为白色。 GDI 不会检查调色板条目。 在此更改**HT\_Get8BPPMaskPalette**可确保正确 ROP 输出，而不是相反的结果。

若要更正的 GDI ROP 行为，GDI 中 Windows XP 及更高版本支持特殊 CMY 调色板组合格式中的 CMY 掩码调色板条目开始时间索引 255 （白色） 和 0 （白色） 和到 25 的索引开始，逐渐到索引 0 （黑色），而不是从索引处开始工作5 （黑色）。 反转 CMY 模式还将所有 CMY 掩码颜色条目都移动到的完整 256 输入面板中，使用的开头和结尾使用等量的黑色和白色条目填充的调色板的中间。

**请注意**  中的讨论中，术语*CMY 模式*的以前的实现中支持的模式是指[ **HT\_Get8BPPMaskPalette**](https://msdn.microsoft.com/library/windows/hardware/ff567320). 术语*CMY\_结模式*仅支持 Windows XP 和更高版本的 GDI，在其中此函数反转的位掩码的模式是指索引时*pPaletteEntry*\[0\]设置为 RGB0。

 

以下步骤所需的所有 Windows XP 和更高版本的驱动程序使用 Windows GDI 半色调每像素 8 位 CMY 掩码模式。 如果正在开发用于 Windows 2000 的驱动程序，应限制为 8 位 / 像素的单色调色板的驱动程序的使用。

1.  设置**flHTFlags**的成员[ **GDIINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff566484)结构到 HT\_标志\_反转\_8BPP\_位掩码\_IDX 以便该 GDI 将呈现图像中一个 CMY\_结模式。

2.  设置*pPaletteEntry*\[0\] ，如下所示之前调用**HT\_Get8BPPMaskPalette**:

    ```cpp
    pPaletteEntry[0].peRed   = 'R';
    pPaletteEntry[0].peGreen = 'G';
    pPaletteEntry[0].peBlue  = 'B';
    pPaletteEntry[0].peFlags = '0';
    ```

    若要执行此操作，调用方应使用**HT\_设置\_BITMASKPAL2RGB**宏 (在中定义*winddi.h*)。 下面是一个示例，演示使用此宏：

    ```cpp
    HT_SET_BITMASKPAL2RGB(pPaletteEntry)
    ```

    这里*pPaletteEntry*是一个指针指向为调用中传递 PALETTEENTRY **HT\_Get8BPPMaskPalette**函数。 当此宏完成执行时， *pPaletteEntry*\[0\]将包含字符串 RGB0。

3.  检查*pPaletteEntry*参数从调用返回[ **HT\_Get8BPPMaskPalette** ](https://msdn.microsoft.com/library/windows/hardware/ff567320)使用**HT\_IS\_BITMASKPALRGB**中定义的宏*winddi.h*。 下面是一个示例，演示使用此宏。

    ```cpp
    InvCMYSupported = HT_IS_BITMASKPALRGB(pPaletteEntry)
    ```

    在此表达式中， *pPaletteEntry*是一个指针指向传递给 PALETTEENTRY **HT\_Get8BPPMaskPalette**函数。 如果此宏将返回 **，则返回 TRUE**，然后 GDI *does*支持倒排的 CMY 8 位每像素位掩码模式。 调用方必须使用转换表将转换为的墨水量的面板索引。 请参阅[转换 8 位的每像素的墨水量的半色调索引](translating-8-bit-per-pixel-halftone-indexes-to-ink-levels.md)有关生成此转换表的函数的示例。

    如果此宏将返回**FALSE**，然后当前版本的 GDI*却不*支持倒排的 CMY 8 位每像素位掩码模式。 在这种情况下，GDI 支持仅较旧 CMY noninverted 模式。

对于 GDI 版本支持每像素 8 位 CMY\_结模式的含义*CMYMask*参数值传递给[ **HT\_Get8BPPMaskPalette**](https://msdn.microsoft.com/library/windows/hardware/ff567320)函数进行了更改。 下表汇总了所做的更改：

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">CMYMask
<div>
 
</div>
值</th>
<th align="left">CMY 模式下索引
<div>
 
</div>
(pPaletteEntry[0] != 'RGB0')</th>
<th align="left">CMY_INVERTED 模式下索引
<div>
 
</div>
(pPaletteEntry[0] == 'RGB0')</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0</p></td>
<td align="left"><p>0:白色</p>
<div>
 
</div>
1 到 254 个：浅灰色-&gt;深灰色
<div>
 
</div>
255:黑色</td>
<td align="left"><p>0-黑色</p>
<div>
 
</div>
1 到 254 个：深灰色-&gt;浅灰色
<div>
 
</div>
255:白色</td>
</tr>
<tr class="even">
<td align="left"><p>1</p></td>
<td align="left"><p>0:白色</p>
<div>
 
</div>
1 到 123:123 5 x 5 x 5 种颜色
<div>
 
</div>
124 到 255:黑色</td>
<td align="left"><p>0 到 65:黑色</p>
<div>
 
</div>
66 到 189:123 5 x 5 x 5 加上一个重复进行着色。 127 索引处的项复制到索引 128。
<div>
 
</div>
190 到 255:白色
<div>
 
</div>
<div>
 
</div>
在索引 127 和 128 的值被复制，以确保 XOR ROP 正常运行。</td>
</tr>
<tr class="odd">
<td align="left"><p>2</p></td>
<td align="left"><p>0:白色</p>
<div>
 
</div>
1 到 214:214 x 6 x 6 颜色 6
<div>
 
</div>
215 到 255:黑色</td>
<td align="left"><p>0 到 20:黑色</p>
<div>
 
</div>
21 到 234:214 x 6 x 6 颜色 6
<div>
 
</div>
235 到 255:白色</td>
</tr>
<tr class="even">
<td align="left"><p>3 到 255</p></td>
<td align="left"><p>0:白色</p>
<div>
 
</div>
1 到 254 个：CxMxY 颜色位掩码
<div>
 
</div>
255:黑色
<div>
 
</div>
<div>
 
</div>
在上述产品中，C、 M 和 Y 的青、 品红和黄，级别数分别表示。
<div>
 
</div>
<div>
 
</div>
<strong>注意</strong>：对于这些模式的有效组合不得具有任何青色、 洋红色、 或黄色的墨水量等于零。 对于此类组合中， <a href="https://msdn.microsoft.com/library/windows/hardware/ff567320" data-raw-source="[&lt;strong&gt;HT_Get8BPPMaskPalette&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567320)"> <strong>HT_Get8BPPMaskPalette</strong> </a>通过返回的零计数调色板中指示的错误条件及其<em>pPaletteEntry</em>参数。</td>
<td align="left"><p>0:黑色</p>
<div>
 
</div>
1 到 254 个：居中的 CxMxY 颜色使用黑色的开头和末尾的空白填充
<div>
 
</div>
CxMxY 是否为奇数，128 索引处的项是一个的重复的索引 127 处。
<div>
 
</div>
255:白色
<div>
 
</div>
<div>
 
</div>
在上述产品中，C、 M 和 Y 的青、 品红和黄，级别数分别表示。
<div>
 
</div>
<div>
 
</div>
<strong>注意：</strong> 256 条目调色板中的操作中心 (x M x Y C) 索引。 即，有相等数量的黑色条目填充低端的调色板和白色填充的高端的条目。
<div>
 
</div>
<div>
 
</div>
<strong>注意</strong>：对于这些模式的有效组合不得具有任何青色、 洋红色、 或黄色的墨水量等于零。 对于此类组合中， <a href="https://msdn.microsoft.com/library/windows/hardware/ff567320" data-raw-source="[&lt;strong&gt;HT_Get8BPPMaskPalette&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567320)"> <strong>HT_Get8BPPMaskPalette</strong> </a>通过返回的零计数调色板中指示的错误条件及其<em>pPaletteEntry</em>参数。</td>
</tr>
</tbody>
</table>

 

-   值*CMYMask*为 0 （灰度） 时，调用方可以处理 CMY 模式或 CMY\_结模式。 但请注意，仅在 CMY 中被正确处理了 GDI ROPs\_结模式。

    CMY 模式：索引 0 到 255 表示从白色到黑色灰度。

    CMY\_结模式：索引 0 到 255 表示灰色刻度范围从黑色到白色。

-   有关的任何有效值*CMYMask*从 1 到 255，调用方应使用示例函数中所示[转换 8 位的每像素的墨水量的半色调索引](translating-8-bit-per-pixel-halftone-indexes-to-ink-levels.md)转换到的墨水量的索引。

-   有关的任何有效值*CMYMask*从 1 到 255，CMY\_结模式填充数组的开头和相同数量的数组的末尾的白色条目的黑色项调色板。 在数组中间使用其他颜色进行填充。 这会确保所有 256 色调色板条目的平衡地都分布因此该 GDI ROPs，这是基于索引的、 不基于颜色的工作正常。 颜色是平衡地分布时索引处的颜色*N*就是索引处的颜色 (256 个字符- *N*)。 一种颜色和及其反转打印在一起，则结果为黑色。 换而言之，对于给定的颜色和及其反转，两个的青色墨水量添加到最大青色墨迹级别中，两个的洋红色墨水量和两个的黄色墨水量一样。 生成的墨水量对应于黑色。

    例如，共有的 27 (3 x 3 x 3) 具有三个级别每个的青、 品红和黄 CMY 调色板的颜色，包括黑色和白色的索引。 因为 27 数为奇数并且 GDI 需要 CMY\_结模式面板将填充以黑色或白色条目数相等，GDI 重复中间索引 （索引 13 为 27 颜色） 处的项。 在索引 13 和 14 现在的条目相同的现在调色板将具有 28 的颜色。 若要填充调色板，GDI 调色板 （索引 0 到 113） 的开始处放置 114 黑色条目、 会放到 28 颜色索引 114 （黑色） 通过 141 （白色），并使用白色 （索引 142 到 255） 填充剩余 114 项。 这样，总共 256 条目 (114 + 28 + 114 = 256 个条目)。 索引此布局可确保所有 ROPs 将正确都呈现。 中的示例函数[转换 8 位的每像素的墨水量的半色调索引](translating-8-bit-per-pixel-halftone-indexes-to-ink-levels.md)说明了如何生成墨水量，以及 Windows 2000 CMY332 索引转换表。

    下表列出了对 3 x 3 个调色板中前面段落所述的 3 倍的青色、 洋红色和黄色级别。 256 色调色板，中间使用等量的黑色填充内容的开头和末尾的白色填充内容嵌入 28 颜色 （27 原始调色板颜色加上一个重复）。 是对称的这意味着，如果索引处的墨水量的调色板*N*添加到这些索引处 (256 个字符- *N*)，结果将显示为黑色 (青色、 洋红色和黄色级别 = 2)。

    <table>
    <colgroup>
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th align="left">调色板索引 (3 x 3 x 3 个索引)</th>
    <th align="left">青色级别 0 到 2</th>
    <th align="left">洋红色级别 0 到 2</th>
    <th align="left">黄色级别 0 到 2</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td align="left"><p>0 到 113</p>
    <p>黑色</p></td>
    <td align="left"><p>2</p></td>
    <td align="left"><p>2</p></td>
    <td align="left"><p>2</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>114 (0)</p>
    <p>黑色</p></td>
    <td align="left"><p>2</p></td>
    <td align="left"><p>2</p></td>
    <td align="left"><p>2</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>115 (1)</p></td>
    <td align="left"><p>2</p></td>
    <td align="left"><p>2</p></td>
    <td align="left"><p>1</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>116 (2)</p></td>
    <td align="left"><p>2</p></td>
    <td align="left"><p>2</p></td>
    <td align="left"><p>0</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>117 (3)</p></td>
    <td align="left"><p>2</p></td>
    <td align="left"><p>1</p></td>
    <td align="left"><p>2</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>118 (4)</p></td>
    <td align="left"><p>2</p></td>
    <td align="left"><p>1</p></td>
    <td align="left"><p>1</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>119 (5)</p></td>
    <td align="left"><p>2</p></td>
    <td align="left"><p>1</p></td>
    <td align="left"><p>0</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>120 (6)</p></td>
    <td align="left"><p>2</p></td>
    <td align="left"><p>0</p></td>
    <td align="left"><p>2</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>121 (7)</p></td>
    <td align="left"><p>2</p></td>
    <td align="left"><p>0</p></td>
    <td align="left"><p>1</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>122 (8)</p></td>
    <td align="left"><p>2</p></td>
    <td align="left"><p>0</p></td>
    <td align="left"><p>0</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>123 (9)</p></td>
    <td align="left"><p>1</p></td>
    <td align="left"><p>2</p></td>
    <td align="left"><p>2</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>124 (10)</p></td>
    <td align="left"><p>1</p></td>
    <td align="left"><p>2</p></td>
    <td align="left"><p>1</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>125 (11)</p></td>
    <td align="left"><p>1</p></td>
    <td align="left"><p>2</p></td>
    <td align="left"><p>0</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>126 (12)</p></td>
    <td align="left"><p>1</p></td>
    <td align="left"><p>1</p></td>
    <td align="left"><p>2</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>127 (13)</p>
    <p>复制到索引 128</p></td>
    <td align="left"><p>1</p></td>
    <td align="left"><p>1</p></td>
    <td align="left"><p>1</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>128 (14)</p>
    <p>重复的索引 127 处的项</p></td>
    <td align="left"><p>1</p></td>
    <td align="left"><p>1</p></td>
    <td align="left"><p>1</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>129 (15)</p></td>
    <td align="left"><p>1</p></td>
    <td align="left"><p>1</p></td>
    <td align="left"><p>0</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>130 (16)</p></td>
    <td align="left"><p>1</p></td>
    <td align="left"><p>0</p></td>
    <td align="left"><p>2</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>131 (17)</p></td>
    <td align="left"><p>1</p></td>
    <td align="left"><p>0</p></td>
    <td align="left"><p>1</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>132 (18)</p></td>
    <td align="left"><p>1</p></td>
    <td align="left"><p>0</p></td>
    <td align="left"><p>0</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>133 (19)</p></td>
    <td align="left"><p>0</p></td>
    <td align="left"><p>2</p></td>
    <td align="left"><p>2</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>134 (20)</p></td>
    <td align="left"><p>0</p></td>
    <td align="left"><p>2</p></td>
    <td align="left"><p>1</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>135 (21)</p></td>
    <td align="left"><p>0</p></td>
    <td align="left"><p>2</p></td>
    <td align="left"><p>0</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>136 (22)</p></td>
    <td align="left"><p>0</p></td>
    <td align="left"><p>1</p></td>
    <td align="left"><p>2</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>137 (23)</p></td>
    <td align="left"><p>0</p></td>
    <td align="left"><p>1</p></td>
    <td align="left"><p>1</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>138 (24)</p></td>
    <td align="left"><p>0</p></td>
    <td align="left"><p>1</p></td>
    <td align="left"><p>0</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>139 (25)</p></td>
    <td align="left"><p>0</p></td>
    <td align="left"><p>0</p></td>
    <td align="left"><p>2</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>140 (26)</p></td>
    <td align="left"><p>0</p></td>
    <td align="left"><p>0</p></td>
    <td align="left"><p>1</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>141 (27)</p>
    <p>白色</p></td>
    <td align="left"><p>0</p></td>
    <td align="left"><p>0</p></td>
    <td align="left"><p>0</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>142 到 255</p>
    <p>白色</p></td>
    <td align="left"><p>0</p></td>
    <td align="left"><p>0</p></td>
    <td align="left"><p>0</p></td>
    </tr>
    </tbody>
    </table>

     

<!-- -->

-   如果请求的调色板是 CMY 模式调色板 (不 CMY\_结模式调色板)，然后针对的值*CMYMask*呈现每像素 8 位字节索引位 3 到 255 之间，具有以下含义。 在这种情况下，位模式表示可在直接未转换的墨水量。 这同样适用时 CMY\_结模式字节索引映射到 CMY 模式下使用的转换表**CMY332Idx**成员。 请参阅[转换 8 位的每像素的墨水量的半色调索引](translating-8-bit-per-pixel-halftone-indexes-to-ink-levels.md)有关详细信息。

```cpp
  Bit     7 6 5 4 3 2 1 0
          |   | |   | | |
          +---+ +---+ +-+
            |     |    |
            |     |    +-- Yellow 0-3 (Max. 4 levels)
            |     |
            |     +-- Magenta 0-7 (Max. 8 levels)
            |
            +-- Cyan 0-7 (Max. 8 levels)
```

 

 





