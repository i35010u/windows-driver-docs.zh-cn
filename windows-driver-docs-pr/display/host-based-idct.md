---
title: 基于主机的 IDCT
description: 基于主机的 IDCT
ms.assetid: 9f44e734-8cbc-4317-bd72-66d4ac7cd4de
keywords:
- 宏块 WDK DirectX va，因此 IDCT
- 低级别 IDCT WDK DirectX VA
- 基于主机的 IDCT WDK DirectX VA
- 逆变离散余弦 WDK DirectX VA
- IDCT WDK DirectX VA
- 16 位的基于主机的 IDCT WDK DirectX VA
- 8-8 溢出基于主机的 IDCT WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3f8a865f8ad315b3b41efb27b2611389e0b8a83b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563543"
---
# <a name="host-based-idct"></a>基于主机的 IDCT


## <span id="_host_based_idct"></span><span id="_HOST_BASED_IDCT"></span>


IDCT 可能在主机上，执行与通过空间的域中的 DirectX VA API 传递结果。 有两个用于将结果发送给快捷键主机从受支持的方法：16 位，8-8 溢出。 **BConfigSpatialResid8**的成员[ **DXVA\_ConfigPictureDecode**](https://msdn.microsoft.com/library/windows/hardware/ff563133)结构指示使用哪种方法。

### <a name="span-id16-bithost-basedidctprocessingspanspan-id16-bithost-basedidctprocessingspanspan-id16-bithost-basedidctprocessingspan16-bit-host-based-idct-processing"></a><span id="16-bit_Host-Based_IDCT_Processing"></span><span id="16-bit_host-based_idct_processing"></span><span id="16-BIT_HOST-BASED_IDCT_PROCESSING"></span>16 位的基于主机的 IDCT 处理

用于 16 位的基于主机的残留差异解码宏块控制结构是否[ **DXVA\_MBctrl\_我\_HostResidDiff\_1** ](https://msdn.microsoft.com/library/windows/hardware/ff563983)并[ **DXVA\_MBctrl\_P\_HostResidDiff\_1**](https://msdn.microsoft.com/library/windows/hardware/ff563993)。

发送使用 16 位方法的剩余空间域差异数据时，将按顺序发送的 16 位数据块。 每个空间域数据块包含，64 16 位整数。

如果*BPP*，如派生自[ **DXVA\_PictureParameters** ](https://msdn.microsoft.com/library/windows/hardware/ff564012)结构，大于 8，可以使用仅 16 位方法。 如果**bPicIntra** DXVA 成员\_PictureParameters 结构为 1 并且*BPP*为 8，8-8 溢出方法使用。 如果*IntraMacroblock*为零，示例发送为有符号的数量要添加到经过运动补偿预测值的 16 位残留差异。 如果*IntraMacroblock*为 1，16 位样本发送，如下所示：

-   如果**bConfigIntraResidUnsigned**的成员[ **DXVA\_ConfigPictureDecode** ](https://msdn.microsoft.com/library/windows/hardware/ff563133)结构为 1，这些示例发送作为无符号的数量相对于零的常量引用值。 例如，中级灰色将表示为 Y = 2<sup>(BPP-1)</sup>，Cb = 2<sup>(BPP-1)</sup>，Cr = 2<sup>(BPP-1)</sup>。

-   如果**bConfigIntraResidUnsigned** DXVA 成员\_ConfigPictureDecode 结构为零，则这些示例都将作为有符号的数量，相对于常量引用值为 2 发送<sup>(BPP-1)</sup>. 例如，中级灰色将表示为 Y = 0，Cb = 0，Cr = 0。

通过扫描指定的顺序按顺序发送的数据块**wPatternCode** 1 从最高有效位到最低有效位的值与成员的位的宏块控制结构。

剩余的差值不剪辑可以假设已执行的主机上，除非**bConfigSpatialHost8or9Clipping**的成员[ **DXVA\_ConfigPictureDecode** ](https://msdn.microsoft.com/library/windows/hardware/ff563133)结构为 1。 尽管唯一*BPP*+ 1 位范围需要来充分表示空间域差异数据，某些输出[IDCT](low-level-idct-processing-elements.md)实现将生成超出此范围内的数字，除非它们是剪辑。

**请注意**  快捷键必须使用至少一个 15 位范围的值。 尽管视频编码标准通常指定剪辑差异值，然后将其添加到预测值 （即，在视频中每个样本 8 位的 9 位剪辑），此剪辑阶段是实际不必要的因为它具有对生成没有影响解码的输出图片。 不假定此剪辑发生除非加速器硬件所示的必要条件**bConfigSpatialHost8or9Clipping** DXVA 成员\_ConfigPictureDecode 结构被设置为 1。

 

### <a name="span-id8-8overflowhost-basedidctprocessingspanspan-id8-8overflowhost-basedidctprocessingspanspan-id8-8overflowhost-basedidctprocessingspan8-8-overflow-host-based-idct-processing"></a><span id="8-8_Overflow_Host-Based_IDCT_Processing_"></span><span id="8-8_overflow_host-based_idct_processing_"></span><span id="8-8_OVERFLOW_HOST-BASED_IDCT_PROCESSING_"></span>8-8 溢出基于主机的 IDCT 处理

用于 8 8 溢出基于主机的残留差异解码宏块控制结构是否[ **DXVA\_MBctrl\_我\_HostResidDiff\_1** ](https://msdn.microsoft.com/library/windows/hardware/ff563983)并[ **DXVA\_MBctrl\_P\_HostResidDiff\_1**](https://msdn.microsoft.com/library/windows/hardware/ff563993)。

如果*BPP*变量派生自[ **DXVA\_PictureParameters** ](https://msdn.microsoft.com/library/windows/hardware/ff564012)结构为 8，8-8 溢出空间域残留差异方法可能是使用。 如果它的使用，则需要**bPicIntra**此结构的成员为 1 并*BPP*为 8。 在这种情况下，使用仅为 8 位表示每个空间域差异值。 发送数据使用 8 8 溢出方法时，将按顺序发送的 8 位数据块。 8 位空间域残留数据包含 64 个字节包含传统的光栅中的数据的值的差异的每个块扫描顺序 （按顺序后, 跟第二个行和等等的元素的第一行的元素）。

如果*IntraMacroblock*宏块控件中命令是零，8 位空间域残留差异示例包括已签名的差异，以增加或减少 (从确定**bConfigResid8Subtraction**的成员[ **DXVA\_ConfigPictureDecode** ](https://msdn.microsoft.com/library/windows/hardware/ff563133)结构以及该示例是在第一个传递模块或溢出块)相对于运动补偿预测值。

如果*IntraMacroblock* (第 0 中的位**wMBtype**宏块结构中的成员) 为零，并且计算差来在块中的某些像素是太大，无法表示使用仅为 8 位，表示第二个发送的 8 位空间域残留差异样本溢出块。

如果*IntraMacroblock* (第 0 中的位**wMBtype**宏块结构中的成员) 为 1，按如下所示设置示例的 8 位空间域残留差异：

-   如果**bConfigIntraResidUnsigned** DXVA 成员\_ConfigPictureDecode 结构为 1，8 位样本发送为无符号数量相对于常量引用值为零。 例如，中级灰色将表示为 Y = 2<sup>(BPP-1)</sup>，Cb = 2<sup>(BPP-1)</sup>，Cr = 2<sup>(BPP-1)</sup>。

-   如果**bConfigIntraResidUnsigned**的成员[ **DXVA\_ConfigPictureDecode** ](https://msdn.microsoft.com/library/windows/hardware/ff563133)结构为零，则将有符号的数量作为发送的 8 位示例相对于 2 的常量引用值<sup>(BPP-1)</sup>。 例如，中级灰色将表示为 Y = 0，Cb = 0，Cr = 0。

如果 IntraMacroblock 为 1，8 位溢出块不会发送。

通过扫描指定的顺序按顺序发送的数据块**wPatternCode**位宏块控制命令的值为 1，从最重要到最不重要的成员。 所有必要的 8 位溢出块随后会发送所指定的**全球合作伙伴大会\_溢出**宏块控制命令的成员。 此类溢出块而不是添加了如果减去**bConfigResid8Subtraction**的成员[ **DXVA\_ConfigPictureDecode** ](https://msdn.microsoft.com/library/windows/hardware/ff563133)结构1。 添加的每个 nonintra 宏块的 8 位区别第一次传递。 如果**bPicOverflowBlocks**的成员[ **DXVA\_PictureParameters** ](https://msdn.microsoft.com/library/windows/hardware/ff564012)结构为零或*IntraMacroblock*宏块控制命令的成员为 1，则没有第二个阶段。 如果**bPicOverflowBlocks**为 1， *IntraMacroblock*为零，并且**bConfigResid8Subtraction**为每个 nonintra 宏块为 1，第二步中的 8 位的差异相减。 如果**bPicOverflowBlocks**为 1， *IntraMacroblock*为零，并且**bConfigResid8Subtraction**为零，第二步中的 8 位差异为每个 nonintra 宏块添加。

如果非零，这两个原始 8 位块中和对应的 8 位溢出块中任何示例，以下规则适用：

-   如果**bConfigResid8Subtraction**为零，该示例的符号必须是相同的两个块中。

-   如果**bConfigResid8Subtraction**为 1，原始的 8 位块中的示例的符号必须是负 1 次的相应溢出块中的示例值的符号相同。

这些规则允许后将传递两个要添加到预测与结果的 8 位剪辑的图片示例。

**请注意**  使用 8 位差异用溢出块**bConfigResid8Subtraction**等于零 （中添加的每个溢出块的两个 8 位差异的结果） 不能表示一个剩余如果差异值 255 *IntraMacroblock*为零。 (可以按以下方式表示的最大差异值是 127 + 127 = 254。)这使得 8 8 溢出基于主机的 IDCT 方法不严格符合视频编码标准时**bConfigResid8Subtraction**为零。 但是，由于它在某些现有实现中使用，表示一张图片，所需的数据量方面的 16 位样本使用比效率更高，通常不产生任何有意义的视频质量下降，要支持此格式。

 

 

 





