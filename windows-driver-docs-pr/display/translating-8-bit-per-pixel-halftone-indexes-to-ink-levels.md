---
title: 将每像素 8 位半色调索引转换为墨位
description: 将每像素 8 位半色调索引转换为墨位
ms.assetid: 5859b379-4e03-4cd8-836d-9a0b068b47c0
keywords:
- GDI WDK Windows 2000 显示，半色调
- 图形驱动程序 WDK Windows 2000 显示，半色调
- 绘制 WDK GDI，半色调
- 半色调 WDK GDI
- 8位每像素 CMY 掩码模式 WDK GDI
- GenerateInkLevels
- INKLEVELS
- 转换每像素8位半色调索引 WDK GDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4310c8fbf0e103bfbffd06f7a250b2bc25d752bc
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90717588"
---
# <a name="translating-8-bit-per-pixel-halftone-indexes-to-ink-levels"></a>将每像素 8 位半色调索引转换为墨位


## <span id="ddk_translating_8_bit_per_pixel_halftone_indexes_to_ink_levels_gg"></span><span id="DDK_TRANSLATING_8_BIT_PER_PIXEL_HALFTONE_INDEXES_TO_INK_LEVELS_GG"></span>


此处所示的 **GenerateInkLevels** 函数提供了一个示例，说明如何将每像素8位半色调索引转换为墨迹级别。 这些索引包含在 CMY 模式和 CMY \_ 反转模式调色板中，GDI 的 [**HT \_ Get8BPPMaskPalette**](/windows/win32/api/winddi/nf-winddi-ht_get8bppmaskpalette) 函数在其 *pPaletteEntry* 参数中返回。 **GenerateInkLevels** 生成 INKLEVELS 结构的256元素数组。

此函数可用于生成 Windows 2000 CMY 模式或 Windows 2000 CMY \_ 反转模式转换表。 此函数还可用于生成 Windows 2000 CMY 模式 CMY332 反向映射索引表。  (CMY332 使用三位，分别用于青色和洋红色，两位表示黄色 ) 。当 *CMYMask* 值介于3到255的范围内时，该函数的调用方可以使用此表将 WINDOWS 2000 CMY \_ 倒转索引映射到当前现有驱动程序的 windows 2000 CMY 索引。

### <a name="span-idinklevels_structurespanspan-idinklevels_structurespaninklevels-structure"></a><span id="inklevels_structure"></span><span id="INKLEVELS_STRUCTURE"></span>INKLEVELS 结构

```cpp
typedef struct _INKLEVELS {
   BYTE  Cyan;          // Cyan level from 0 to max
   BYTE  Magenta;       // Magenta level from 0 to max
   BYTE  Yellow;        // Yellow level from 0 to max
   BYTE  CMY332Idx;     // Original windows 2000 CMY332 Index
} INKLEVELS, *PINKLEVELS;
```

### <a name="span-idexample_generateinklevels_functionspanspan-idexample_generateinklevels_functionspanexample-generateinklevels-function"></a><span id="example_generateinklevels_function"></span><span id="EXAMPLE_GENERATEINKLEVELS_FUNCTION"></span>GenerateInkLevels 函数示例

**GenerateInkLevels**函数根据*CMYMask*和*CMYInverted 参数*中的值计算 INKLEVELS 结构的8位每像素转换表。 此函数为介于0到255范围内的有效 *CMYMask* 值生成 INKLEVELS 转换表。

调用此函数时， *pInkLevels* 参数必须指向 256 INKLEVELS 条目的有效内存位置。 如果函数返回 **TRUE**，则可以使用 *pInkLevels* 将每像素8位索引转换为墨迹级别，或映射到较旧的 CMY332 索引。 如果调用函数时将 *CMYMask* 设置为无效值 (从3到255的值，其中任何蓝绿色、品红或黄色级别为零) ，则函数返回 **FALSE**。

```cpp
BOOL
GenerateInkLevels(
    PINKLEVELS  pInkLevels,  // Pointer to 256 INKLEVELS table
    BYTE        CMYMask,     // CMYMask mode
    BOOL        CMYInverted  // TRUE for CMY_INVERTED mode
    )

{
    PINKLEVELS  pILDup;
    PINKLEVELS  pILEnd;
    INKLEVELS   InkLevels;
    INT         Count;
    INT         IdxInc;
    INT         cC;  // Number of Cyan levels
    INT         cM;  // Number of Magenta levels
    INT         cY;  // Number of Yellow levels
    INT         xC;  // Max. number Cyan levels
    INT         xM;  // Max. number Magenta levels
    INT         xY;  // Max. number Yellow levels
    INT         iC;
    INT         iM;
    INT         iY;
    INT         mC;
    INT         mM;

    switch (CMYMask) {

    case 0:

        cC =
        cM =
        xC =
        xM = 0;
        cY =
        xY = 255;
        break;

    case 1:
    case 2:

        cC =
        cM =
        cY =
        xC =
        xM =
        xY = 3 + (INT)CMYMask;
        break;

    default:

        cC = (INT)((CMYMask >> 5) & 0x07);
        cM = (INT)((CMYMask >> 2) & 0x07);
        cY = (INT)( CMYMask       & 0x03);
        xC = 7;
        xM = 7;
        xY = 3;
        break;
    }   // end switch statement

    Count = (cC + 1) * (cM + 1) * (cY + 1);

    if ((Count < 1) || (Count > 256)) {
        return(FALSE);
    }

    InkLevels.Cyan      =
    InkLevels.Magenta   =
    InkLevels.Yellow    =
    InkLevels.CMY332Idx = 0;
    mC                  = (xM + 1) * (xY + 1);
    mM                  = xY + 1;
    pILDup              = NULL;
    if (CMYInverted) {

        //
        // Move the pInkLevels to the first entry following 
        // the centered embedded entries.
        // Skipped entries are set to white (zero). Because this 
        // is a CMY_INVERTED mode, entries start from back of the
        // table and move toward the beginning of the table.
        //

        pILEnd      = pInkLevels - 1;
        IdxInc      = ((256 - Count - (Count & 0x01)) / 2);
        pInkLevels += 255;

        while (IdxInc--) {

            *pInkLevels-- = InkLevels;
        }

        if (Count & 0x01) {

            //
            // If we have an odd number of entries, we need to
            // duplicate the center one for the XOR ROP to
            // operate correctly. pILDup will always be index
            // 127, and the duplicates are at indexes 127 and 128.
            //
            pILDup = pInkLevels - (Count / 2) - 1;
        }

        //
        // We are running from the end of table to the beginning,
        // because in CMY_INVERTED mode, index 0 is black and
        // index 255 is white. Since we generate only Count 
        // white, black, and colored indexes, and place them at
        // the center, we will change xC, xM, xY max. indexes 
        // to the same as cC, cM and cY
        // so we only compute cC*cM*cY entries.
        //

        IdxInc = -1;
        xC     = cC;
        xM     = cM;
        xY     = cY;

    } else {
        IdxInc = 1;
        pILEnd = pInkLevels + 256;
    }

    //
    // In the following composition of ink levels, the index
    // always runs from 0 ink level (white) to maximum ink 
    // levels (black).  With CMY_INVERTED mode, we compose ink
    // levels from index 255 to index 0 rather than from index 
    // 0 to 255.
    //

    if (CMYMask) {

        INT Idx332C;
        INT Idx332M;

        for (iC = 0, Idx332C = -mC; iC <= xC; iC++) {

            if (iC <= cC) {

                InkLevels.Cyan  = (BYTE)iC;
                Idx332C        += mC;
            }

            for (iM = 0, Idx332M = -mM; iM <= xM; iM++) {

                if (iM <= cM) {

                    InkLevels.Magenta  = (BYTE)iM;
                    Idx332M           += mM;
                }

                for (iY = 0; iY <= xY; iY++) {

                    if (iY <= cY) {

                        InkLevels.Yellow = (BYTE)iY;
                    }

                    InkLevels.CMY332Idx = (BYTE)(Idx332C + 
                                          Idx332M) +
                                          InkLevels.Yellow;
                    *pInkLevels         = InkLevels;

                    if ((pInkLevels += IdxInc) == pILDup) {

                        *pInkLevels  = InkLevels;
                        pInkLevels  += IdxInc;
                    }
                }
            }
        }

        //
        // Now, if we need to pad black at the other end of the
        // translation table, then do it here. Notice that
        // InkLevels are at cC, cM and cY here and CMY332Idx
        // is at black.
        //

        while (pInkLevels != pILEnd) {

            *pInkLevels  = InkLevels;
            pInkLevels  += IdxInc;
        }

    } else {

        //
        // Gray Scale case
        //

        for (iC = 0; iC < 256; iC++, pInkLevels += IdxInc) {

            pInkLevels->Cyan      =
            pInkLevels->Magenta   =
            pInkLevels->Yellow    =
            pInkLevels->CMY332Idx = (BYTE)iC;
        }
    }

    return(TRUE);
}
```

 

