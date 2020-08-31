---
title: 基于主机的 IDCT
description: 基于主机的 IDCT
ms.assetid: 9f44e734-8cbc-4317-bd72-66d4ac7cd4de
keywords:
- macroblocks WDK DirectX VA，IDCT
- 低级别 IDCT WDK DirectX VA
- 基于主机的 IDCT WDK DirectX VA
- 逆离散-余弦转换 WDK DirectX VA
- IDCT WDK DirectX VA
- 基于16位主机的 IDCT WDK DirectX VA
- 8-8 基于主机的 IDCT WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 451aed4d1cc605e09a96a87358b53193c657211f
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89064122"
---
# <a name="host-based-idct"></a>基于主机的 IDCT


## <span id="_host_based_idct"></span><span id="_HOST_BASED_IDCT"></span>


可以在主机上执行 IDCT，并通过空间域中的 DirectX VA API 传递结果。 可通过两种方法将结果从主机发送到加速器：16位和8-8 溢出。 [**DXVA \_ ConfigPictureDecode**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_configpicturedecode)结构的**bConfigSpatialResid8**成员指示所使用的方法。

### <a name="span-id16-bit_host-based_idct_processingspanspan-id16-bit_host-based_idct_processingspanspan-id16-bit_host-based_idct_processingspan16-bit-host-based-idct-processing"></a><span id="16-bit_Host-Based_IDCT_Processing"></span><span id="16-bit_host-based_idct_processing"></span><span id="16-BIT_HOST-BASED_IDCT_PROCESSING"></span>基于主机的16位 IDCT 处理

与基于主机的16位残留差别解码一起使用的宏块控制结构是 [**DXVA \_ MBctrl \_ I \_ HostResidDiff \_ 1**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_mbctrl_i_hostresiddiff_1) 和 [**DXVA \_ MBctrl \_ P \_ HostResidDiff \_ 1**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_mbctrl_p_hostresiddiff_1)。

使用16位方法发送空间域残留差异数据时，会按顺序发送16位数据块。 空间域数据的每个块都包含 64 16 位整数。

如果 *BPP*的派生自 [**DXVA \_ PictureParameters**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_pictureparameters) 结构，大于8，则只能使用16位方法。 如果 DXVA PictureParameters 结构的 **bPicIntra** 成员 \_ 为1，并且 *BPP* 为8，则使用8-8 溢出方法。 如果 *IntraMacroblock* 为零，则将16位残差样本发送为要添加到运动补偿预测值的已签名数量。 如果 *IntraMacroblock* 为1，则将按如下所示发送16位示例：

-   如果[**DXVA \_ ConfigPictureDecode**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_configpicturedecode)结构的**bConfigIntraResidUnsigned**成员为1，则示例将作为无符号数量（相对于常量引用值为零）发送。 例如，中间级灰色表示为 Y = 2<sup> (BPP-1) </sup>，Cb = 2<sup> (bpp-1) </sup>，CR = 2<sup> (bpp-1) </sup>。

-   如果 DXVA ConfigPictureDecode 结构的 **bConfigIntraResidUnsigned** 成员 \_ 为零，则示例将作为有符号数量（相对于<sup>)  (BPP-1 </sup>的常数引用值）发送。 例如，中间级灰色表示为 Y = 0，Cb = 0，Cr = 0。

数据块按指定顺序按指定顺序发送，其中的值为**wPatternCode** 1，从最高有效位到最低有效位。

除非[**DXVA \_ ConfigPictureDecode**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_configpicturedecode)结构的**bConfigSpatialHost8or9Clipping**成员为1，否则不会在主机上执行对剩余差值值的剪裁。 尽管只需使用 *BPP*+ 1 位范围才能充分地表示空间域差异数据，但某些 [IDCT](low-level-idct-processing-elements.md) 实现的输出将生成超出此范围的数字，除非已将其剪切。

**注意**   加速器必须使用至少一个15位的值范围。 尽管视频编码标准通常会在将差异值添加到预测值之前指定其剪裁值 (即，在8位样本视频) 中使用9位剪辑，但实际上不需要此剪辑阶段，因为它不会影响生成的解码输出图片。 不会假设此剪辑发生的原因是加速器硬件需要，如将 DXVA ConfigPictureDecode 结构的 **bConfigSpatialHost8or9Clipping** 成员 \_ 设置为1所示。

 

### <a name="span-id8-8_overflow_host-based_idct_processing_spanspan-id8-8_overflow_host-based_idct_processing_spanspan-id8-8_overflow_host-based_idct_processing_span8-8-overflow-host-based-idct-processing"></a><span id="8-8_Overflow_Host-Based_IDCT_Processing_"></span><span id="8-8_overflow_host-based_idct_processing_"></span><span id="8-8_OVERFLOW_HOST-BASED_IDCT_PROCESSING_"></span>8-8 基于主机的 IDCT 处理溢出

与8-8 溢出主机的残留差别解码一起使用的宏块控制结构包括 [**DXVA \_ MBctrl \_ I \_ HostResidDiff \_ 1**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_mbctrl_i_hostresiddiff_1) 和 [**DXVA \_ MBctrl \_ P \_ HostResidDiff \_ 1**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_mbctrl_p_hostresiddiff_1)。

如果从[**DXVA \_ PictureParameters**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_pictureparameters)结构派生的*BPP*变量是8，则可以使用8-8 溢出空间-域剩余差方法。 如果此结构的 **bPicIntra** 成员为1，并且 *BPP* 为8，则需要使用此成员。 在这种情况下，每个空间域差异值仅使用8位表示。 使用8-8 溢出方法发送数据时，将按顺序发送8位数据块。 每个8位空间为域残留差异数据块包含64字节，其中包含常规光栅扫描顺序中数据的值， (第一行的元素按顺序排列，后面是第二行的元素，依此类推) 。

如果宏块控制命令中的*IntraMacroblock*为零，则8位空间空间残留差异样本为要添加或减去的签名差异 (是从[**DXVA \_ ConfigPictureDecode**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_configpicturedecode)结构的**bConfigResid8Subtraction**成员中确定的，以及该样本是位于第一个传递块还是溢出块) 相对于运动补偿预测值。

如果宏块结构的**wMBtype**成员中的*IntraMacroblock* (位 0) 为零，并且要为块中的某个像素表示的差异太大，无法只使用8位，则会发送第二个溢出块的8位空间-域残留差异示例。

如果宏块结构的**wMBtype**成员中的*IntraMacroblock* (位 0) 为1，则会按如下所示设置8位空间-域残差示例：

-   如果 DXVA ConfigPictureDecode 结构的 **bConfigIntraResidUnsigned** 成员 \_ 为1，则8位样本将作为无符号数量（相对于常量引用值为零）发送。 例如，中间级灰色表示为 Y = 2<sup> (BPP-1) </sup>，Cb = 2<sup> (bpp-1) </sup>，CR = 2<sup> (bpp-1) </sup>。

-   如果[**DXVA \_ ConfigPictureDecode**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_configpicturedecode)结构的**bConfigIntraResidUnsigned**成员为零，则8位样本将作为有符号数量（相对于常量引用值 2<sup> (BPP-1) </sup>）发送。 例如，中间级灰色表示为 Y = 0，Cb = 0，Cr = 0。

如果 IntraMacroblock 为1，则不发送8位溢出块。

数据块按指定顺序按指定顺序发送，其中的值为1（从最重要到最不重要）的 **wPatternCode** 成员。 然后，所有必要的8位溢出块将按照宏块 control 命令的 **wPC \_ 溢出** 成员的指定发送。 如果[**DXVA \_ ConfigPictureDecode**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_configpicturedecode)结构的**bConfigResid8Subtraction**成员为1，则将减去此类溢出块，而不是添加。 将添加每个 nonintra 宏块的8位差异第一次。 如果[**DXVA \_ PictureParameters**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_pictureparameters)结构的**bPicOverflowBlocks**成员为零，或宏块 control 命令的*IntraMacroblock*成员为1，则没有第二次通过。 如果 **bPicOverflowBlocks** 为1，则 *IntraMacroblock* 为0， **bConfigResid8Subtraction** 为1，则将减去每个 nonintra 宏块的第二个8位差异。 如果 **bPicOverflowBlocks** 为1，则 *IntraMacroblock* 为0， **bConfigResid8Subtraction** 为零，则将添加每个 nonintra 宏块的第二个8位差异。

如果原始8位块和对应的8位溢出块中的任何示例均非零，则适用以下规则：

-   如果 **bConfigResid8Subtraction** 为零，则示例的符号在两个块中必须相同。

-   如果 **bConfigResid8Subtraction** 为1，则在原始的8位块中，该示例的符号必须与在相应的溢出块中的示例值为负1倍。

这些规则允许在两次传递后将示例添加到具有结果的8位剪辑的预测图片中。

**注意**   对**bConfigResid8Subtraction**等于零的溢出块使用8位差异 (这会导致为每个溢出块增加两个8位差异) 在*IntraMacroblock*为零时，不能表示 + 255 的残留差值。  (以这种方式表示的最大差值值为 127 + 127 = 254。 ) 这使得在 **bConfigResid8Subtraction** 为零时，基于主机的8-8 溢出 IDCT 方法不会与视频编码标准完全兼容。 但是，这种格式受支持，因为它在某些现有的实现中使用，比16位示例使用的更高效，而不是表示图片所需的数据量，并且通常不会导致视频质量下降。

 

 

