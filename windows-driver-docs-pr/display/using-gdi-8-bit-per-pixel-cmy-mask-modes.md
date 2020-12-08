---
title: 使用 GDI 每像素 8 位 CMY 掩码模式
description: 使用 GDI 每像素 8 位 CMY 掩码模式
keywords:
- GDI WDK Windows 2000 显示，半色调
- 图形驱动程序 WDK Windows 2000 显示，半色调
- 绘制 WDK GDI，半色调
- 半色调 WDK GDI
- 8位每像素 CMY 掩码模式 WDK GDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 52a83f02a642ae99a6a18b556eeb6463e8820a34
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803895"
---
# <a name="using-gdi-8-bit-per-pixel-cmy-mask-modes"></a>使用 GDI 每像素 8 位 CMY 掩码模式


## <span id="ddk_using_gdi_8_bit_per_pixel_cmy_mask_modes_gg"></span><span id="DDK_USING_GDI_8_BIT_PER_PIXEL_CMY_MASK_MODES_GG"></span>


在 Microsoft Windows 2000 中， [**HT \_ Get8BPPMaskPalette**](/windows/win32/api/winddi/nf-winddi-ht_get8bppmaskpalette) 函数返回每像素8位单色或调色板。 在 Windows XP 和更高版本中，此函数已被修改，因此当 *Use8BPPMaskPal* 参数设置为 **TRUE** 时，它还会返回已反转索引的 CMY 调色板。 返回的调色板的类型取决于 *pPaletteEntry* \[ \] 调用 **HT \_ Get8BPPMaskPalette** 时存储在 pPaletteEntry 0 中的值。 如果 *pPaletteEntry* \[ 0 \] 设置为 "RGB0"，则返回一个反转索引调色板。 如果 *pPaletteEntry* \[ 0 \] 设置为0，则返回正常的 CMY 调色板。

此更改的 **\_ Get8BPPMaskPalette** 是因为当 Windows GDI 使用的 ROPs （基于调色板中的索引，而不是调色板颜色）时，它会假定调色板的索引0始终为黑色，最后一个索引始终为白色。 GDI 不检查调色板项。 此 **超线程 \_ Get8BPPMaskPalette** 中的这一更改可确保正确的 ROP 输出，而不是相反的结果。

若要更正 GDI ROP 行为，Windows XP 和更高版本中的 GDI 支持特殊的 CMY 调色板组合格式，在该格式中，CMY 掩码调色板项从索引255开始 (白色) 并向下移动到索引 0 (黑色) ，而不是从索引0开始，而不是从索引 255 0 开始 (黑色) 。 CMY 反转模式还会将所有 CMY 掩码颜色项移到完整256项调色板的中间，并且调色板的开头和结尾用相等的黑色和白色项进行填充。

**注意**   在下面的讨论中，术语 " *CMY" 模式* 是指在以前的 [**HT \_ Get8BPPMaskPalette**](/windows/win32/api/winddi/nf-winddi-ht_get8bppmaskpalette)实现中支持的模式。 术语 *CMY \_ 反转模式* 是指仅在 Windows XP 和更高版本的 GDI 上支持的模式，在此模式下，当 *pPaletteEntry* \[ 0 \] 设置为 "RGB0" 时，此函数将反转位掩码索引。

 

所有 Windows XP 和更高版本的驱动程序都需要以下步骤，这些驱动程序使用 Windows GDI 半色调8位每像素 CMY 掩码模式。 如果要开发适用于 Windows 2000 的驱动程序，应将驱动程序的使用限制为每像素8位单色调色板。

1.  将 [**GDIINFO**](/windows/win32/api/winddi/ns-winddi-gdiinfo)结构的 **flHTFlags** 成员设置为超线程 \_ 标志 \_ 反转 \_ 8BPP \_ 位掩码 \_ IDX，使 GDI 将以 CMY 反转模式之一呈现图像 \_ 。

2.  *pPaletteEntry* \[ \] 调用 **HT \_ Get8BPPMaskPalette** 之前，请将 pPaletteEntry 0 设置为以下内容：

    ```cpp
    pPaletteEntry[0].peRed   = 'R';
    pPaletteEntry[0].peGreen = 'G';
    pPaletteEntry[0].peBlue  = 'B';
    pPaletteEntry[0].peFlags = '0';
    ```

    为此，调用方应使用 *winddi*) 中定义 (的 **HT \_ SET \_ BITMASKPAL2RGB** 宏。 下面是演示如何使用此宏的示例：

    ```cpp
    HT_SET_BITMASKPAL2RGB(pPaletteEntry)
    ```

    此处的 *pPaletteEntry* 是指向在对 **HT \_ Get8BPPMaskPalette** 函数的调用中传递的 PALETTEENTRY 的指针。 此宏完成执行时， *pPaletteEntry* \[ 0 \] 将包含字符串 "RGB0"。

3.  [**使用 Get8BPPMaskPalette \_**](/windows/win32/api/winddi/nf-winddi-ht_get8bppmaskpalette)在 *winddi* 中定义的 **\_ \_ BITMASKPALRGB** 宏来检查从调用中返回的 *pPaletteEntry* 参数。 下面的示例演示如何使用此宏。

    ```cpp
    InvCMYSupported = HT_IS_BITMASKPALRGB(pPaletteEntry)
    ```

    在此表达式中， *pPaletteEntry* 是指向传递给 **HT \_ Get8BPPMaskPalette** 函数的 PALETTEENTRY 的指针。 如果此宏返回 **TRUE**， *则 GDI 支持* CMY 的每像素反位掩码模式反转。 调用方必须使用转换表将调色板索引转换为墨迹级别。 有关生成此转换表的函数的示例，请参阅 [将每像素8位半色调索引转换为墨迹级别](translating-8-bit-per-pixel-halftone-indexes-to-ink-levels.md) 。

    如果此宏返回 **FALSE**，则当前版本 *的 GDI 不* 支持反转 CMY 8 位每像素位掩码模式。 在这种情况下，GDI 仅支持较早的 CMY noninverted 模式。

对于支持每像素8位 CMY 反转模式的 GDI 版本 \_ ，传递到 [**HT \_ Get8BPPMaskPalette**](/windows/win32/api/winddi/nf-winddi-ht_get8bppmaskpalette)函数的 *CMYMask* 参数值的含义已更改。 下表概述了这些更改：

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
“值”</th>
<th align="left">CMY 模式索引
<div>
 
</div>
 (pPaletteEntry [0]！ = ' RGB0 ' ) </th>
<th align="left">CMY_INVERTED 模式索引
<div>
 
</div>
 (pPaletteEntry [0] = = ' RGB0 ' ) </th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0</p></td>
<td align="left"><p>0：白色</p>
<div>
 
</div>
1到254：浅灰色- &gt; 灰色灰色
<div>
 
</div>
255：黑色</td>
<td align="left"><p>0-黑色</p>
<div>
 
</div>
1到254：深色灰色- &gt; 浅灰色
<div>
 
</div>
255：白色</td>
</tr>
<tr class="even">
<td align="left"><p>1</p></td>
<td align="left"><p>0：白色</p>
<div>
 
</div>
1到123： 123 5x5x5 颜色
<div>
 
</div>
124到255：黑色</td>
<td align="left"><p>0到65：黑色</p>
<div>
 
</div>
66到189： 123 5x5x5 色加一个重复项。 索引127处的项将复制到索引128。
<div>
 
</div>
190到255：白色
<div>
 
</div>
<div>
 
</div>
索引为127和128的值是重复的，以确保 XOR ROP 工作正常。</td>
</tr>
<tr class="odd">
<td align="left"><p>2</p></td>
<td align="left"><p>0：白色</p>
<div>
 
</div>
1到214： 214 6x6x6 颜色
<div>
 
</div>
215到255：黑色</td>
<td align="left"><p>0到20：黑色</p>
<div>
 
</div>
21到234： 214 6x6x6 颜色
<div>
 
</div>
235到255：白色</td>
</tr>
<tr class="even">
<td align="left"><p>3到255</p></td>
<td align="left"><p>0：白色</p>
<div>
 
</div>
1到254： CxMxY 色阶
<div>
 
</div>
255：黑色
<div>
 
</div>
<div>
 
</div>
在上述产品中，C、M 和 Y 分别表示青色、洋红色和黄色的级别数。
<div>
 
</div>
<div>
 
</div>
<strong>注意</strong>：对于这些模式，有效的组合不得具有任何青色、洋红色或黄色墨迹级别等于零。 对于这种组合， <a href="/windows/win32/api/winddi/nf-winddi-ht_get8bppmaskpalette" data-raw-source="[&lt;strong&gt;HT_Get8BPPMaskPalette&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-ht_get8bppmaskpalette)"><strong>HT_Get8BPPMaskPalette</strong></a> 通过在其 <em>pPaletteEntry</em> 参数中返回一个零计数调色板来指示错误条件。</td>
<td align="left"><p>0：黑色</p>
<div>
 
</div>
1到254：在结尾处以黑色填充的居中 CxMxY 颜色
<div>
 
</div>
如果 CxMxY 是奇数，则索引128处的条目是索引127处的条目。
<div>
 
</div>
255：白色
<div>
 
</div>
<div>
 
</div>
在上述产品中，C、M 和 Y 分别表示青色、洋红色和黄色的级别数。
<div>
 
</div>
<div>
 
</div>
<strong>注意：</strong> (C x M x Y) 索引在256项调色板中居中。 也就是说，将在调色板的低端填充相同数量的黑色条目，并且空白条目会填充高端。
<div>
 
</div>
<div>
 
</div>
<strong>注意</strong>：对于这些模式，有效的组合不得具有任何青色、洋红色或黄色墨迹级别等于零。 对于这种组合， <a href="/windows/win32/api/winddi/nf-winddi-ht_get8bppmaskpalette" data-raw-source="[&lt;strong&gt;HT_Get8BPPMaskPalette&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-ht_get8bppmaskpalette)"><strong>HT_Get8BPPMaskPalette</strong></a> 通过在其 <em>pPaletteEntry</em> 参数中返回一个零计数调色板来指示错误条件。</td>
</tr>
</tbody>
</table>

 

-   对于 *CMYMask* 为 0 (灰色刻度) 的值，调用方可以处理 CMY 模式或 CMY \_ 反转模式。 但请注意，仅在 CMY 反转模式下正确处理 GDI ROPs \_ 。

    CMY 模式：索引0到255表示从白色到黑色的灰色刻度。

    CMY \_ 反转模式：索引0到255表示灰色刻度，范围为黑色到白色。

-   对于从1到255的任何有效值 *CMYMask* ，调用方应使用将 [8 位每像素半色调索引转换为墨迹级别](translating-8-bit-per-pixel-halftone-indexes-to-ink-levels.md) 中所示的示例函数，将索引转换为墨迹级别。

-   对于从1到255的任何有效值 *CMYMask* ，CMY \_ 反转模式使用数组开头的黑色条目填充调色板，并在数组的末尾插入相同数量的空白项。 数组的中间部分用其他颜色填充。 这可确保所有256的调色板项都以对称方式分发，以便基于索引的 GDI ROPs （而不是基于颜色的）能够正常工作。 当索引为 *N* 的颜色为索引 (256- *N*) 处的颜色反转时，颜色将对称分布。 当彩色及其逆色一起打印时，结果为黑色。 换而言之，对于给定颜色及其反转，两个青色墨迹级别将添加到最大蓝绿色墨迹级别，就是两个洋红色墨迹级别和两个黄色墨迹级别。 生成的墨迹级别对应于黑色。

    例如，每个绿色、洋红色和黄色都具有三个级别的 CMY 调色板总共有27个 (3 x 3 x 3) 的颜色（包括黑色和白色）索引。 因为27是奇数，并且因为 GDI 要求 \_ 使用相等的黑白项号填充 CMY 反转模式调色板，所以 gdi 会将中间索引处的条目复制 (第27种颜色) 的索引为13。 如果索引为13和14的条目现在相同，调色板现在将具有28种颜色。 为了填充调色板，GDI 会将调色板114上的黑色条目 (索引0到 113) ，将28个颜色置于索引 114 (黑色) 到 141 (白色) ，并使用白色 (索引) 到114来填充剩余的142条目。 这会生成256项， (114 + 28 + 114 = 256 项) 。 此索引布局可确保正确呈现所有 ROPs。 将 [每像素8位半色调索引转换为墨迹级别](translating-8-bit-per-pixel-halftone-indexes-to-ink-levels.md) 的示例函数说明了如何生成墨迹级别以及 WINDOWS 2000 CMY332 索引转换表。

    下表列出了上一段中所述的 3 x 3 x 3 调色板的青色、洋红色和黄色级别。 28个颜色 (27 个原始调色板颜色加上一个重复的) 嵌入在256调色板的中间，并在结尾处有相同的黑色填充量，最后空白填充。 调色板是对称的，这意味着，如果将索引为 *N* 的墨迹级别添加到索引 (256- *N*) ，则结果将为黑色 (青色、洋红色和黄色 = 2) 。

    <table>
    <colgroup>
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th align="left">调色板索引 (3x3x3 索引) </th>
    <th align="left">青色 Level0 为2</th>
    <th align="left">洋红色 Level0 为2</th>
    <th align="left">黄色 Level0 为2</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td align="left"><p>0到113</p>
    <p>黑色</p></td>
    <td align="left"><p>2</p></td>
    <td align="left"><p>2</p></td>
    <td align="left"><p>2</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>114 (0) </p>
    <p>黑色</p></td>
    <td align="left"><p>2</p></td>
    <td align="left"><p>2</p></td>
    <td align="left"><p>2</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>115 (1) </p></td>
    <td align="left"><p>2</p></td>
    <td align="left"><p>2</p></td>
    <td align="left"><p>1</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>116 (2) </p></td>
    <td align="left"><p>2</p></td>
    <td align="left"><p>2</p></td>
    <td align="left"><p>0</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>117 (3) </p></td>
    <td align="left"><p>2</p></td>
    <td align="left"><p>1</p></td>
    <td align="left"><p>2</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>118 (4) </p></td>
    <td align="left"><p>2</p></td>
    <td align="left"><p>1</p></td>
    <td align="left"><p>1</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>119 (5) </p></td>
    <td align="left"><p>2</p></td>
    <td align="left"><p>1</p></td>
    <td align="left"><p>0</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>120 (6) </p></td>
    <td align="left"><p>2</p></td>
    <td align="left"><p>0</p></td>
    <td align="left"><p>2</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>121 (7) </p></td>
    <td align="left"><p>2</p></td>
    <td align="left"><p>0</p></td>
    <td align="left"><p>1</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>122 (8) </p></td>
    <td align="left"><p>2</p></td>
    <td align="left"><p>0</p></td>
    <td align="left"><p>0</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>123 (9) </p></td>
    <td align="left"><p>1</p></td>
    <td align="left"><p>2</p></td>
    <td align="left"><p>2</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>124 (10) </p></td>
    <td align="left"><p>1</p></td>
    <td align="left"><p>2</p></td>
    <td align="left"><p>1</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>125 (11) </p></td>
    <td align="left"><p>1</p></td>
    <td align="left"><p>2</p></td>
    <td align="left"><p>0</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>126 (12) </p></td>
    <td align="left"><p>1</p></td>
    <td align="left"><p>1</p></td>
    <td align="left"><p>2</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>127 (13) </p>
    <p>已复制到索引128</p></td>
    <td align="left"><p>1</p></td>
    <td align="left"><p>1</p></td>
    <td align="left"><p>1</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>128 (14) </p>
    <p>索引127处的条目重复</p></td>
    <td align="left"><p>1</p></td>
    <td align="left"><p>1</p></td>
    <td align="left"><p>1</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>129 (15) </p></td>
    <td align="left"><p>1</p></td>
    <td align="left"><p>1</p></td>
    <td align="left"><p>0</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>130 (16) </p></td>
    <td align="left"><p>1</p></td>
    <td align="left"><p>0</p></td>
    <td align="left"><p>2</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>131 (17) </p></td>
    <td align="left"><p>1</p></td>
    <td align="left"><p>0</p></td>
    <td align="left"><p>1</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>132 (18) </p></td>
    <td align="left"><p>1</p></td>
    <td align="left"><p>0</p></td>
    <td align="left"><p>0</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>133 (19) </p></td>
    <td align="left"><p>0</p></td>
    <td align="left"><p>2</p></td>
    <td align="left"><p>2</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>134 (20) </p></td>
    <td align="left"><p>0</p></td>
    <td align="left"><p>2</p></td>
    <td align="left"><p>1</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>135 (21) </p></td>
    <td align="left"><p>0</p></td>
    <td align="left"><p>2</p></td>
    <td align="left"><p>0</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>136 (22) </p></td>
    <td align="left"><p>0</p></td>
    <td align="left"><p>1</p></td>
    <td align="left"><p>2</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>137 (23) </p></td>
    <td align="left"><p>0</p></td>
    <td align="left"><p>1</p></td>
    <td align="left"><p>1</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>138 (24) </p></td>
    <td align="left"><p>0</p></td>
    <td align="left"><p>1</p></td>
    <td align="left"><p>0</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>139 (25) </p></td>
    <td align="left"><p>0</p></td>
    <td align="left"><p>0</p></td>
    <td align="left"><p>2</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>140 (26) </p></td>
    <td align="left"><p>0</p></td>
    <td align="left"><p>0</p></td>
    <td align="left"><p>1</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>141 (27) </p>
    <p>白色</p></td>
    <td align="left"><p>0</p></td>
    <td align="left"><p>0</p></td>
    <td align="left"><p>0</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>142至255</p>
    <p>白色</p></td>
    <td align="left"><p>0</p></td>
    <td align="left"><p>0</p></td>
    <td align="left"><p>0</p></td>
    </tr>
    </tbody>
    </table>

     

<!-- -->

-   如果请求的调色板是 CMY 模式调色板 (不是 CMY \_ 反转模式调色板) ，则 *CMYMask* 的值从3到255，则呈现的8位每像素字节索引位具有以下含义。 在这种情况下，位模式表示无需转换即可直接使用的墨迹级别。 当 \_ 使用平移表的 **CMY332Idx** 成员将 CMY 反转模式字节索引映射到 CMY 模式时，这同样适用。 有关详细信息，请参阅 [将每像素8位半色调索引转换为墨迹级别](translating-8-bit-per-pixel-halftone-indexes-to-ink-levels.md) 。

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

