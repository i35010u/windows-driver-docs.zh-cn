---
title: 宏块控制命令结构的第二部分
description: 宏块控制命令结构的第二部分
ms.assetid: 94ef61d1-cd7d-4e73-8be8-01f7d23bb91d
keywords:
- macroblocks WDK DirectX VA，通用命令结构
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 07c96b5814b14597a8151748fa660a4166daa870
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89066000"
---
# <a name="second-part-of-macroblock-control-command-structure"></a>宏块控制命令结构的第二部分


## <span id="ddk_second_part_of_macroblock_control_command_structure_gg"></span><span id="DDK_SECOND_PART_OF_MACROBLOCK_CONTROL_COMMAND_STRUCTURE_GG"></span>


一般宏块控件命令结构的第二部分包含三种变体，具体取决于图片解码过程的配置：

1.  如果**wMBtype**成员中的*HostResidDiff* (位 11) 等于1，则宏块控件命令的下一个元素为**wPC \_ 溢出**。 **WPC \_ 溢出**成员（如果已使用）指定宏块的哪些块使用溢出残留差异数据。 **wPC \_溢出** 后跟一个 DWORD 等于零。

2.  如果**wMBtype**成员中的*HostResidDiff* (位 11) 等于零，并且[**DXVA \_ PictureParameters**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_pictureparameters)的**bChromaFormat**成员等于1，则宏块控件命令的下一个元素为**bNumCoef，** 这是一个由六个元素组成的字节数组。 **BNumCoef**成员指示宏块每个块的剩余差数据缓冲区中的系数数。

3.  如果**wMBtype**元素中的*HostResidDiff* (位 11) 等于零，并且 DXVA PictureParameters 的**bChromaFormat**成员 \_ 不等于1，则宏块控件命令的下一个元素为**wTotalNumCoef**。 后跟一个 DWORD 等于零的值。

### <a name="span-idwpc_overflowspanspan-idwpc_overflowspanspan-idwpc_overflowspanwpc_overflow"></a><span id="wPC_Overflow"></span><span id="wpc_overflow"></span><span id="WPC_OVERFLOW"></span>wPC \_ 溢出

**WPC \_ 溢出**结构成员指定宏块的哪些块使用溢出残留差异数据。

当 HostResidDiff 等于 1) 时使用基于主机的残留差异解码 (当*HostResidDiff*等于1并且[**DXVA \_ PictureParameters**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_pictureparameters)的**bPicOverflowBlocks**成员等于1且*IntraMacroblock*等于零时 (8-8 溢出方法) ， **wPC \_ 溢出**包含与**wPatternCode**相同的方式指定的溢出块的模式代码。 编码溢出块的数据 (这些块的第 11 *个减号等于* 1) 在残留编码缓冲区中找到相同的索引顺序， * () 增加* 。

### <a name="span-idbnumcoefspanspan-idbnumcoefspanspan-idbnumcoefspanbnumcoef"></a><span id="bNumCoef"></span><span id="bnumcoef"></span><span id="BNUMCOEF"></span>bNumCoef

**BNumCoef**结构成员是包含六个元素的数组。 **BNumCoef**数组的第*i*个元素包含宏块的每个块的剩余方差数据缓冲区中的系数数量，其中*i*是宏块中指定的*块的索引*，如 mpeg-2 视频图6-10、6-11 和 (6-12 中指定的块的索引，它是 Y 的 x 扫描顺序，后跟 Cb，再后跟 Cr) 。 仅当*HostResidDiff*为零时， [**DXVA \_ PictureParameters**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_pictureparameters)的**bChromaFormat**成员为 1 (4:2:0) 时，才使用**bNumCoef** 。 如果使用的是4:2:2 或4:4:4 格式，则它将增加典型的宏块控制命令的大小，超过了严重内存对齐边界，因此在非4:2:0 情况下，只会使用转换系数结构中的 EOB 来确定每个块中的系数数。 **BNumCoef**的目的是指出残留差数据缓冲区中的每个块的数据数量，表示为存在的系数数。 当[**DXVA \_ ConfigPictureDecode**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_configpicturedecode)的**bConfig4GroupedCoefs**成员为1时， **bNumCoef**可能包含为块发送的实际系数数，或该值向上舍入为4的倍数。 这些系数的数据是以相同顺序在残留差异缓冲区中找到的。

### <a name="span-idwtotalnumcoefspanspan-idwtotalnumcoefspanspan-idwtotalnumcoefspanwtotalnumcoef"></a><span id="wTotalNumCoef"></span><span id="wtotalnumcoef"></span><span id="WTOTALNUMCOEF"></span>wTotalNumCoef

**WTotalNumCoef**结构成员指示整个宏块的残留差数据缓冲区中的系数总数。 仅当*HostResidDiff*为零时， [**DXVA \_ PictureParameters**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_pictureparameters)的**bChromaFormat**成员不等于 1 (4:2:0) 时，才使用此成员。

 

