---
title: 第二部分宏块控制命令结构
description: 第二部分宏块控制命令结构
ms.assetid: 94ef61d1-cd7d-4e73-8be8-01f7d23bb91d
keywords:
- 宏块 WDK DirectX VA，通用命令结构
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3d47b5d40cff5527e79e1ab2812c3a10998688d3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542483"
---
# <a name="second-part-of-macroblock-control-command-structure"></a>第二部分宏块控制命令结构


## <span id="ddk_second_part_of_macroblock_control_command_structure_gg"></span><span id="DDK_SECOND_PART_OF_MACROBLOCK_CONTROL_COMMAND_STRUCTURE_GG"></span>


泛型宏块控制命令结构的第二部分包含三个变体，具体取决于解码过程图片的配置：

1.  如果*HostResidDiff* (位 11 英寸**wMBtype**成员) 是等于 1，宏块控制命令的下一个元素是**全球合作伙伴大会\_Overflow**。 **全球合作伙伴大会\_溢出**成员，如果使用，指定哪些块宏块使用溢出残留的差异数据。 **全球合作伙伴大会\_Overflow**后跟一个 dword 值，等于零。

2.  如果*HostResidDiff* (位 11 英寸**wMBtype**成员) 等于零， **bChromaFormat**隶属[ **DXVA\_PictureParameters** ](https://msdn.microsoft.com/library/windows/hardware/ff564012)是等于 1，宏块控制命令的下一个元素是**bNumCoef，** 为六个元素的字节数组。 **BNumCoef**成员指示的残留的差异数据缓冲区的每个宏块的块中的系数。

3.  如果*HostResidDiff* (位 11 英寸**wMBtype**元素) 等于零， **bChromaFormat** DXVA 成员\_PictureParameters 不等于 1，宏块控制命令的下一个元素是**wTotalNumCoef**。 这一切后跟一个 dword 值，等于零。

### <a name="span-idwpcoverflowspanspan-idwpcoverflowspanspan-idwpcoverflowspanwpcoverflow"></a><span id="wPC_Overflow"></span><span id="wpc_overflow"></span><span id="WPC_OVERFLOW"></span>wPC\_Overflow

**全球合作伙伴大会\_溢出**结构成员指定的宏块使用溢出残留的差异数据的块。

使用基于主机的残留差异解码时 (当*HostResidDiff*等于 1) 与**bPicOverflowBlocks**的成员[ **DXVA\_PictureParameters** ](https://msdn.microsoft.com/library/windows/hardware/ff564012)等于 1 和*IntraMacroblock*等于零 （8-8 溢出方法）**全球合作伙伴大会\_溢出**包含模式代码中与相同的方式指定溢出块**wPatternCode**。 编码的溢出块的数据 (这些块具有位减去 11*我*等于 1) 在剩余编码相同的索引顺序中的缓冲区中找到 (增加*我*)。

### <a name="span-idbnumcoefspanspan-idbnumcoefspanspan-idbnumcoefspanbnumcoef"></a><span id="bNumCoef"></span><span id="bnumcoef"></span><span id="BNUMCOEF"></span>bNumCoef

**BNumCoef**结构成员是六个元素的数组。 *我*个元素**bNumCoef**数组包含的每个块的残留的差异数据缓冲区中的系数数*我*的宏块，其中*我*是中 mpeg-2 视频图 6-10，6-11，6 到 12 （Y，然后按 Cb 后, 跟 Cr 光栅扫描顺序） 指定宏块中的块的索引。 **bNumCoef**使用时，才*HostResidDiff*为零并且**bChromaFormat**隶属[ **DXVA\_PictureParameters**](https://msdn.microsoft.com/library/windows/hardware/ff564012)为 1 (4:2:0)。 如果在 4 中使用： 2:2 或 4:4:4 格式，它会增加的典型宏块控制命令过去关键的内存对齐边界，因此，只有在转换系数结构 EOB 用于确定在每个块中的系数的数字大小非-4:2:0 情况。 目的**bNumCoef**是指示为每个块中数据表示为个数的系数存在的残留的差异数据缓冲区的数量。 当**bConfig4GroupedCoefs**的成员[ **DXVA\_ConfigPictureDecode** ](https://msdn.microsoft.com/library/windows/hardware/ff563133)为 1， **bNumCoef**可能包含系数的实际数目的块发送或值舍入到最多为 4 的倍数。 按相同顺序的残留差异缓冲区中找到这些系数的数据。

### <a name="span-idwtotalnumcoefspanspan-idwtotalnumcoefspanspan-idwtotalnumcoefspanwtotalnumcoef"></a><span id="wTotalNumCoef"></span><span id="wtotalnumcoef"></span><span id="WTOTALNUMCOEF"></span>wTotalNumCoef

**WTotalNumCoef**结构成员指示整个宏块的残留的差异数据缓冲区中的系数的总数。 使用此成员时，才*HostResidDiff*为零并**bChromaFormat**的成员[ **DXVA\_PictureParameters** ](https://msdn.microsoft.com/library/windows/hardware/ff564012)不等于 1 (4:2:0)。

 

 





